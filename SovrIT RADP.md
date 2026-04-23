# SovrIT Physical Security Architecture: Protecting Sovereign Personal Data From Theft And Asset Seizure

## Introduction

This document describes an optional but highly recommended security architecture for SovrIT PTI deployments. It addresses a fundamental quandary: you want your servers' encrypted disks/datasets to be (conveniently) decrypted automatically on reboots, but you also need them to protect your data in cases of theft and physical seizure. Standard "encryption at rest" fails here—if a server is stolen and booted, a Trusted Platform Module (TPM) will quietly hand over the key.

This architecture solves that problem by splitting the decryption key across multiple factors, binding the server’s ability to unlock itself to:

- The physical presence of a specific device in your home.
- The consent of an authorized user (via an actionable notification on a mobile phone).
- A secondary “friend” node elsewhere on the internet.

The result is a system that can heal itself during routine outages but becomes a digital brick under seizure.

**Important:** This entire layer is optional. SovrIT can be built with simple manual passphrase decryption or TPM‑only auto‑unlock. However, for users facing physical risk (raids, border seizures, hostile authorities, theft), this architecture provides defense in depth.

---

## Core Concepts (Defined for a General Audience)

Before diving into components, let’s define the technical terms used throughout.

| Term | Plain‑language definition |
|------|----------------------------|
| **Encryption at rest** | Data on a disk is scrambled. Without the correct **decryption key**, the data is unreadable garbage. |
| **Decryption key** | A secret (like a very long password) that unscrambles the disk. |
| **LUKS** | Linux Unified Key Setup – a standard for disk encryption. Works with ZFS, ext4, or any filesystem. (Even if you use ZFS native encryption, the same principles apply.) |
| **TPM (Trusted Platform Module)** | A chip on the server's motherboard that can store a decryption key and release it only if the system’s firmware and bootloader haven’t been tampered with. |
| **Tang server** | A network service that *helps* a client reconstruct a decryption key. The Tang server never knows the key itself – it only provides a cryptographic puzzle piece. |
| **Clevis** | A client that talks to a Tang server. During boot, Clevis asks the Tang server for its piece and combines it with a local piece to unlock the disk. |
| **Network‑Bound Disk Encryption (NBDE)** | Using a Tang server on the network to automatically unlock a disk. The server will only unlock if it can reach that specific Tang server. |
| **Shamir’s Secret Sharing (SSS)** | A way to split a secret into N pieces, requiring any M of them (e.g., 2 out of 3) to rebuild the original. |
| **initrd (initial RAM disk)** | A tiny, temporary filesystem loaded before your main system starts. It’s where decryption happens. |
| **Tor Onion Service** | A hidden service on the Tor network that can be reached without knowing the server’s IP address. Works through firewalls and NAT. |
| **ntfy.sh** | A simple, self‑hostable push notification service. Your server can send notifications to your phone, and your phone can reply with buttons or text. |
| **Duress passphrase** | A special password that *appears* to unlock the system but actually triggers a self‑destruct (wiping the encryption headers). |

---

## The Four‑Factor Model (Threshold = Any 2 of 3)

Instead of requiring *all* factors (which would break during any outage), the system is configured to unlock automatically when **any two of three** independent factors are available.

| Factor | Name | What it is | Where it lives |
|--------|------|------------|----------------|
| **A** | Home Proximity Beacon | A smart light bulb (ESP32‑based) that runs a Tang server. It provides a key piece only if it has not been violently unplugged. | Your home |
| **B** | Friend Node | A tiny ESP32 or travel router running a Tang server, plugged into a trusted friend’s router (powered by the router’s USB port). | Friend’s home |
| **C** | Mobile Authorizer | Your phone, running the SovrIT Assistant app. It can send an approval or a one‑time code via push notification. | Your pocket |

**Why 2‑of‑3?**  
- If your home internet goes down, Factor A disappears. But Factors B and C can still unlock the system (Friend Node + your phone).  
- If your phone is lost, Factors A and B (Home Beacon + Friend Node) still work.  
- If the server and your home are both seized, the attacker has Factors A (poisoned) and the server – but not B or C. They cannot unlock.  

---

## Component Details & How They Work

### 1. The Poisoned Home Beacon (Smart Bulb)

**What it is:** An ESP32 microcontroller flashed with custom firmware that runs a Tang server. It is installed inside a standard smart‑compatible light bulb (or hidden inside an old router, as originally brainstormed). It draws power from the light socket or USB.

**How it works (normal operation):**  
- The bulb continuously serves a valid cryptographic key piece over the local network.  
- It also monitors for a “planned shutdown” signal from your Core Node (CN).  
- If the bulb loses power **without** having received that signal, it assumes it has been seized. On next power‑up, it replaces the valid key piece with a **poisoned key piece**.

**The poisoned key’s effect:**  
When the server tries to unlock using the poisoned key, the decryption process fails – but more importantly, a script in the server’s initrd detects the poisoned signature and **triggers a self‑destruct** (wiping the disk’s encryption headers). The data becomes irrecoverable.

**Creating it (technical overview):**  
1. Buy an ESP32‑based smart bulb (or an ESP32 dev board + relay to control an ordinary bulb).  
2. Flash firmware using `esp32‑tang` (an open source Tang implementation).  
3. Generate a static key pair for the Tang service.  
4. Write a small state‑keeping routine in the firmware: store a `planned_shutdown` flag in non‑volatile memory (RTC memory or flash).  
5. On boot, if the flag is false, serve the poisoned key. If true, serve the real key.  
6. Provide an authenticated HTTP endpoint that the Core Node calls before a clean shutdown to set the flag to true.

### 2. The Friend Node (Remote Tang Server)

**What it is:** A second Tang server running on ultra‑low‑power hardware (ESP32 or a GL.iNet travel router). It is given to a friend, relative, or employer and plugged into their router – both for power (via USB) and network (Ethernet or WiFi).

**Why it’s safe for the friend:**  
Tang never sees the actual disk encryption key. It only participates in a cryptographic handshake (like a puzzle piece). Even if the friend’s device is seized, the attacker gains only one piece of a 2‑of‑3 threshold – useless alone.

**How it works:**  
- The Friend Node joins your private mesh network (NetBird) or exposes a Tor Onion Service.  
- Your remote servers (RFNs) are configured to contact this Friend Node as one of the unlock factors.  
- It runs 24/7, always answering handshake requests.

**Creating it (technical overview):**  
1. Obtain an ESP32‑S3 or a GL.iNet GL‑MT300N.  
2. Install a minimal Linux (OpenWrt on the travel router) or use `esp32-tang` on the ESP32.  
3. Configure a Tang server (for OpenWrt: `tang` package; for ESP32: the same firmware as the Home Beacon but without the poisoning logic).  
4. Generate a long‑lived key pair.  
5. Set up automatic joining of your NetBird network (or configure Tor Onion Service).  

### 3. Mobile Authorizer (Push Notification + TOTP)

**What it is:** A small companion app (or a webhook that integrates with ntfy.sh) that allows an authorized user to approve a boot without using SSH.

**How it works:**  
- When a server reboots and cannot gather 2 factors automatically, it enters a waiting state in initrd.  
- The server sends an actionable push notification to the user’s phone (via ntfy.sh):  
  *“Server RFN‑02 needs unlock. Approve?”* with **[APPROVE]** and **[DENY]** buttons.  
- Tapping **[APPROVE]** sends an HTTP POST back to a tiny “Auth Webhook” service (hosted on the mesh or on the Friend Node).  
- The server, which has been polling the webhook, receives the approval and proceeds to unlock.

**Optional TOTP mode:**  
The notification can include a text input field. The user opens their TOTP app (e.g., Aegis, Google Authenticator), copies the 6‑digit code, pastes it into the notification, and submits. The server verifies the code.

**Why this is “Krista‑proof” (simple enough for any non‑technical user):**  
- No terminal, no SSH client, no command line.  
- All interactions happen inside the phone’s notification shade.

### 4. Tor Onion Services (NAT‑Bypass Layer)

**Problem:** If your home internet is down, your phone cannot reach the Auth Webhook at home. If both the server and the Friend Node are behind firewalls, they cannot find each other.

**Solution:** Run a Tor Onion Service on:
- The Friend Node
- The Auth Webhook (which can be co‑located on the Friend Node or a cheap VPS)

**How it works:**  
- Each service gets a `.onion` address (e.g., `friendnode123456.onion`).  
- Servers in initrd use a tiny Tor client (embedded in NixOS initrd) to connect to these `.onion` addresses.  
- No port forwarding, no dynamic DNS, no public IP required.  
- Even if the attacker seizes the server, they cannot easily discover the Friend Node’s location.

**Implementation overview:**  
1. Install `tor` on the Friend Node.  
2. Configure a hidden service pointing to the Tang port (e.g., 80).  
3. On the server side, include `tor` in the initrd (NixOS option `boot.initrd.network.tor.enable`).  
4. Configure Clevis to use the `.onion` address instead of a raw IP.

---

## How It Works (Step‑by‑Step, Normal Boot)

1. The server powers on and boots into the initrd environment.  
2. The Clevis client attempts to contact the two Tang servers:  
   - Home Beacon (via local IP or Tor)  
   - Friend Node (via Tor)  
3. If both are reachable, Clevis gets two key pieces. The decryption key is reconstructed (any 2 of 3 threshold – but here we have 2).  
4. The main disk unlocks. The server continues booting normally.  
5. No human intervention. Total time: ~10–30 seconds.

---

## Scenario Analysis (The Critical Factors)

### Scenario 1: Seizure of Home Equipment (CN, Home Beacon, etc.)

**Attacker actions:** Raid your home. They unplug the Home Beacon (smart bulb) without a planned shutdown signal. They take the Core Node (CN) and the bulb.

**What happens:**  
- The bulb loses power → `planned_shutdown` flag remains `false`.  
- When the attacker later powers up the bulb in their lab, it serves the **poisoned key**.  
- If they also boot the seized CN, the CN’s initrd contacts the bulb, receives the poisoned key, and triggers the self‑destruct routine (wipes LUKS/ZFS encryption headers).  
- The CN’s data becomes permanently unrecoverable.

**Attacker’s alternative:** They try to boot the CN without the bulb. Then the CN has 0 factors (Friend Node unreachable because the home network is gone). The CN waits forever for a manual approval that never comes.

**Outcome:** Data is lost to the attacker. You, the owner, also lose data unless you have offline backups.

### Scenario 2: Seizure of Remote Failover Node (RFN – VPS)

**Attacker actions:** Law enforcement seizes the VPS server (the RFN) but does not seize your home or your friend’s node.

**What happens:**  
- The RFN is powered off and moved. When rebooted in the lab, it tries to contact the Home Beacon and the Friend Node.  
- Home Beacon is still in your home (not seized). It serves a valid key piece – but the RFN cannot reach it because the lab network cannot route to your home (no VPN, no Tor .onion address unless the attacker also controls the Tor network).  
- Friend Node is also still at your friend’s house. The RFN cannot reach it either.  
- The RFN has 0 factors. It goes into waiting mode, sending push notifications to your phone (which the attacker does not possess).  
- The disk remains locked. The attacker sees only encrypted garbage.

**Outcome:** The RFN’s data is safe.

### Scenario 3: Duress Passphrase (Coercion)

**Attacker actions:** They hold you at gunpoint and demand the decryption passphrase.

**What you do:** You provide the **duress passphrase** – a special password you configured in advance for a specific LUKS keyslot (or ZFS key location).

**What happens:**  
- The system appears to unlock. The boot process continues.  
- In reality, a background script detects that the duress slot was used and executes `cryptsetup luksErase` (or `zfs change-key -i` to destroy the key).  
- The encryption headers are overwritten with random data.  
- After a short delay (to fool the attacker into thinking it worked), the system panics or shuts down.  
- The data is now mathematically impossible to recover – even by you.

**Recovery for you:** You must restore from offline backups. This is a scorched‑earth response, not a reversible lock.

### Scenario 4: Non‑Seizure, User Away from Home Needs Access

**Situation:** You are traveling. Your RFN reboots automatically (e.g., power glitch at the data center). Your home internet is working normally.

**What happens automatically:**  
- The RFN contacts the Home Beacon (Factor A) and the Friend Node (Factor B). Both are reachable.  
- 2 factors are present → RFN unlocks and boots without any action from you.

**If instead the home internet is down** (see Scenario 5 below), the system will wait for you. But because home is working, you have zero interruption.

### Scenario 5: Internet Outage at Home (Comcast Down)

**Situation:** Your home internet is offline, but the RFN reboots. You are away and need access to medical records on the RFN.

**What happens automatically:**  
- The RFN attempts to contact the Home Beacon → fails (no route).  
- It contacts the Friend Node → succeeds.  
- It has only 1 of 2 required factors. It enters a waiting state in initrd.

**Your action (via phone):**  
1. You receive a push notification: *“RFN needs second factor. Approve?”*  
2. You tap **[APPROVE]**.  
3. Your phone sends an approval to the Auth Webhook (hosted on the Friend Node or a cheap VPS).  
4. The RFN polls the webhook, sees approval, and treats that as Factor C (Mobile Authorizer).  
5. It now has 2 factors (Friend Node + Mobile Approval) and unlocks.

**Total time:** ~30 seconds. No SSH, no typing long passphrases.

### Scenario 6: The Nuclear Option Triggered Mistakenly

**Situation:** A false alarm – e.g., a power surge causes the Home Beacon to lose power without a planned shutdown, or you accidentally unscrew the bulb.

**Result:** The bulb is now in “poisoned” mode. The next time any server tries to use it, that server will self‑destruct (wipe its encryption headers).

**How to recover:**  
1. **First, prevent further damage:** Immediately disconnect any server that might boot and contact the poisoned bulb.  
2. **Reset the bulb:** Connect to the bulb via its serial console or a dedicated recovery Wi‑Fi AP. Clear the `poisoned` flag and regenerate a fresh Tang key pair.  
3. **Restore server data from backup:** Because the headers were wiped, the disk is now random noise. You must:  
   - Reinstall the base OS.  
   - Restore data from your offline backups (e.g., external USB drive, Backblaze B2, or a second RFN with delayed replication).  
4. **Re‑enroll the server:** Reconfigure LUKS/ZFS with new keys and re‑bind to the (now reset) Home Beacon and Friend Node.

**Prevention:** Always send a “planned shutdown” signal from the Core Node before any maintenance that involves power‑cycling the bulb. This sets the `planned_shutdown` flag and avoids poisoning.

---

## Implementation Notes (Without Tying to a Specific Encryption System)

Although the discussion originally assumed LUKS, the architecture works equally well with **ZFS native encryption** or any other dm‑crypt based system. The key insight is that you can have multiple independent ways to unlock the same master key (LUKS keyslots, or ZFS’s multiple passphrases via `zfs change-key`). For ZFS, the “poisoned key” approach would involve a script that runs `zfs set keylocation=prompt ...` followed by `zfs load-key -r` and then immediately overwrites the key in memory – less clean than LUKS’s `luksErase`, but still feasible.

For the purposes of this white paper, the term “encryption header wipe” means destroying the metadata that allows the encrypted data to be decrypted, regardless of the underlying technology.

---

## Why This Architecture Is Optional (But Recommended)

SovrIT is designed for a wide range of threat models. A small business backing up family photos does not need a poisoned smart bulb. A journalist fleeing a repressive regime may.

Therefore, the build guide will present two paths:  
- **Standard Path:** TPM‑only auto‑unlock or manual passphrase.  
- **High‑Security Path:** The full anti‑seizure stack described here, with all components (Poisoned Bulb, Friend Node, Mobile Authorizer, Tor onions).

The high‑security path adds approximately $30–$50 in hardware (ESP32 bulbs, a Friend Node device) and about 2–3 hours of configuration. For users facing physical threats, that trade‑off is trivial.

---

## Conclusion

This architecture resolves the “paranoia paradox” – a system that is secure against physical seizure yet remains available during everyday outages. By splitting authority across three independent factors (Home Beacon, Friend Node, Mobile Authorizer) and requiring only two of them, the server can heal itself automatically when the network is healthy, and still be unlocked remotely by a non‑technical user via a single tap on a phone.

The poisoned Home Beacon ensures that even if an attacker seizes your entire home lab, the act of unplugging the beacon triggers a self‑destruct. The Friend Node, hidden on a trusted person’s network and accessible only via Tor, provides a secondary automatic factor that resists geolocation and seizure. And the mobile push approval provides a human‑in‑the‑loop safety valve for the remaining corner cases.

This is not Hollywood security. It is practical, low‑cost, and built on proven open source tools (Tang, Clevis, Tor, ntfy.sh, ESP32). It is the closest thing to a “digital fortress” that can still let you fetch medical records from a hotel room.
