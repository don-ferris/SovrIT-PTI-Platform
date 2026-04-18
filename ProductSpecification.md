# SovrIT PTI: Product Specification

## 1. Introduction
### 1.1 Purpose
To reclaim digital autonomy by establishing a local-first, zero-trust infrastructure that replaces cloud-dependent services with a unified, encrypted ecosystem. It is engineered to ensure that your data, communications, and identity remain under your exclusive control, providing a stable and sovereign foundation for digital life that is immune to third-party surveillance or monetization.
### 1.2 Scope
This specification defines the technical boundaries and operational standards for the SovrIT PTI ecosystem. It encompasses the physical hardware architecture, logical network segmentation (VLANs), and the Runtime Substrate—specifically identity, ingress, and storage layers. The scope extends to the integration of sovereign modules for communication, productivity, and intelligence, as well as the "Ghost Mirror" failover and "Living Handbook" documentation systems. It does not cover the maintenance of third-party ISP bandwidth or the internal development of the open-source engines utilized.
### 1.3 Target Audience
Privacy advocates, advanced self-hosters, technical administrators, and contributors to the SovrIT project.

---

## 2. Technical Objectives (The Seven Pillars in Practice)

These objectives define the "Definition of Done" for the SovrIT ecosystem. Every service, script, and hardware choice must align with these seven core requirements.

### 2.1 Absolute Sovereignty & Zero-Trust Privacy
The system ensures that all identity, data, and communication assets are owned and controlled exclusively by the user, with zero exposure to third-party intermediaries.
* **Objective:** Establish a "Digital Fortress" where third parties act only as blind transport pipes for encrypted data.
* **Standard (Identity):** Centralize all access through a self-hosted identity provider (**Authentik**) using biometric-first verification (**WebAuthn**). External "Sign-in with Google/Apple" is strictly prohibited.
* **Standard (Connectivity):** All administrative and inter-node traffic must be encapsulated within a private, peer-to-peer mesh network (**NetBird**). No service ports are exposed directly to the public internet.
* **Standard (Comms):** Data in transit through non-sovereign servers (e.g., mobile carriers or ISPs) must utilize end-to-end encryption. This includes **SIP-TLS/SRTP** for telephony and **GPG/S/MIME** for sensitive mail, ensuring that carriers see only "mathematical noise," never the payload.

### 2.2 Autonomous Functional Resiliency
Data survival must be ensured by employing redundant backups; up-time for critical system services must be considered "mission critical", utilizing automated "self-healing" workflows wherever possible to minimize manual intervention.
* **Objective (Operational):** Deploy automated health checks via **Uptime Kuma** and **n8n**.
* **Objective (Data):** Automate the **3-2-1 Backup Rule** (3 copies, 2 media types, 1 off-site).
* **Standard (The "Self-Healing" Rule):** If a service degrades, the system must attempt an autonomous restart or rebuild. 
* **Standard (The "Off-site Archive" Rule):** Encrypted, incremental backups (via **Kopia**) must be pushed at regular (1-4 hour) intervals to an **S3-compatible provider**. Encryption must happen *client-side* before the data leaves the network.

### 2.3 Global High Availability & Failover Redundancy
Power and internet outages at home must be mitigated to preserve critical services and access to data.
* **Objective:** Maintain a geographically distant **VPS Ghost Mirror**.
* **Standard:** In the event of a local ISP or power failure, critical "Life-Line" services (Identity, Vault, and Communications) must automatically failover to the VPS to ensure zero downtime for remote users.

### 2.4 Invisible & Active Security
Security should be a silent partner, not a series of annoying pop-ups.
* **Objective:** Orchestrate a "Defense-in-Depth" stack overseen by the **SovrIT NetSentinel** (Security SLM).
* **Standard:** Utilize **NetAlertX** for intrusion awareness and **CrowdSec** for behavioral blocking. The NetSentinel correlates these signals to autonomously isolate threats and notify the user only when human judgment is required.

### 2.5 Sovereign Voice/AI Assistance
Intelligence must be private, local, and context-aware, utilizing a tiered model approach for different tasks.
* **Objective:** Process all AI requests (LLM, STT, TTS) on the local **Compute/LLM Node**.
* **Standard (Reasoning):** Utilize **Phi-4-mini** for high-speed, real-time voice interaction and **Qwen3-8B** for complex, long-context document analysis (RAG).
* **Standard (Privacy):** No prompt data or personal records shall ever leave the network. The assistant has "Read-Only" access to the universal search index, providing insights from medical/financial documents without exposing raw data to external APIs.

### 2.6 Decoupled Encryption at Rest
Physical possession of a server should not equal access to its data.
* **Objective:** Implement **ZFS-native encryption** where the master keys are never stored on the physical substrate.
* **Standard:** Encryption keys must be "injected" from a trusted mesh device during the boot sequence. If the server is powered down or removed from the premises, the data remains mathematically inaccessible noise.

### 2.7 Operational Continuity: The Living Handbook
The system must be maintainable by non-technical users through a perfectly synchronized physical-digital documentation bridge.
* **Objective:** Maintain a "Human-Centric" documentation vault in **Dokuwiki**.
* **Standard (The Procedure Rule):** Documentation consists of step-by-step procedures built around **annotated screenshots** (e.g., "Click the gear icon shown circled in red").
* **Standard (The Parity Rule):** A dedicated **Visual Agent** (e.g., **Qwen2.5-VL**) regularly audits all system UIs. When a software update changes a layout, menu, or dialog, the agent autonomously:
    1. Re-captures the affected UI element.
    2. Re-annotates the image to match the existing visual style.
    3. Updates the Handbook page and increments the revision number.
    4. Triggers an **ntfy** alert to the user to print the updated page for the physical binder.

---

## 3. Logical Network Architecture

The SovrIT network is a hybrid architecture combining physical isolation (VLANs), an encrypted overlay (NetBird), and a geographically distant (VPS) failover node (The Ghost Mirror).

### 3.1 Physical Segmentation (VLAN Schema)
The local substrate utilizes a "Default Deny" posture between five distinct security zones:

| VLAN ID | Name | Description & Policy |
| :--- | :--- | :--- |
| **10** | **MGMT** | 10.10.10.x - Infrastructure management (IPMI, Controllers). No WAN access. |
| **20** | **CORE** | 10.10.20.x - The Runtime Substrate (Identity, DNS, Ingress). Restricted WAN. |
| **30** | **TRUSTED** | 10.10.30.x - Primary user devices. Full mesh access. |
| **40** | **IOT** | 172.16.40.x - Isolated hardware (Cameras/Sensors). Zero outbound/inter-VLAN access. |
| **50** | **GUEST** | 192.168.0.x - Internet-only access. Total client isolation. |

### 3.2 The Sovereign Mesh & Ghost Mirror (Hybrid Topology)
The network relies on **NetBird** (WireGuard) to bridge the home infrastructure with the remote VPS.
* **The SecureNet Mesh:** All administrative and inter-node traffic is encapsulated in a peer-to-peer overlay. No service ports are opened on the local home router.
* **The Ghost Mirror (VPS):** Acts as a hardened, secondary node in the mesh.
    * **Ingress Role:** Acts as the "Front Porch" for public-facing traffic, proxying requests to the home node via the mesh.
    * **Failover Role (Life-Line Services):** The VPS hosts a "Warm Standby" of critical services (Authentik, Vaultwarden, Actual Budget, Radicale, and Paperless-ngx). 
    * **Data Sync:** Encrypted data stores for these services are synchronized from the Home Node to the VPS at regular intervals (via **Kopia** or **ZFS send** over the mesh). 
    * **Zero-Knowledge Hosting:** Data resides on the VPS in an encrypted state. It is only accessible through the Sovereign Identity gate, ensuring that the VPS provider has zero visibility into your financial or medical records.

### 3.3 DNS, Discovery & Internal Trust (Step-CA)
This layer handles how services are found and how they prove their identity to your devices.

1. **Filtering Layer:** **AdGuard Home** intercepts all queries to strip tracking, telemetry, and malware domains.
2. **Resolution Layer:** **Unbound** performs recursive resolution directly from Root Nameservers, bypassing ISP logging.
3. **Internal Trust Anchor (Step-CA):** Operates a private Certificate Authority (PKI) within the mesh. 
    * **Sovereign SSL:** Issues internal TLS certificates for all `.lan` and mesh services.
    * **Privacy:** This removes the need to use public ACME/Let's Encrypt challenges for internal services, ensuring that your internal domain names and service structures are never leaked to public transparency logs.
    * **Requirement:** All trusted devices must have the SovrIT Root Certificate installed to ensure seamless, warning-free HTTPS across the entire substrate.

### 3.4 Ingress & Traffic Orchestration (Traefik)
**Traefik** manages all inbound traffic across both the Home and VPS nodes:
* **Sovereign Gatekeeping:** Every request is challenged by the **Authentik** Forward Auth middleware. 
* **Protocol Enforcement:** All traffic is forced to HTTPS. Traefik coordinates with **Step-CA** to ensure certificates are valid and automatically rotated.

---

## 4. Storage & Filesystem Infrastructure

SovrIT utilizes **ZFS** as the mandatory filesystem for all persistent data. The architecture supports a tiered storage model, allowing high-performance system data and high-capacity media to coexist under a unified management standard.

### 4.1 Storage Tiering & Pool Standards
To balance performance and capacity, the storage substrate is divided into two functional tiers:
* **The Core Tier (System/Apps):** Configured as a **ZFS Mirror** (RAID-1 equivalent). This tier provides maximum IOPS and fast recovery for the operating system, identity databases, and service configurations.
* **The Archive Tier (Media/Bulk):** Configured as **RAIDZ2 or RAIDZ3** (allowing 2-3 drive failures). This tier is optimized for sequential read/write and maximum storage efficiency for large media libraries.
* **Verification:** Monthly **ZFS Scrubs** are mandatory across all tiers to detect and repair latent bit-rot.

### 4.2 Logical Dataset Strategy
Data is organized into logical **Datasets** rather than simple directories. This allows for granular control over encryption, snapshots, and performance tuning without the complexity of per-service management.
* **Categorical Grouping:** Instead of per-service datasets, data is grouped by functional requirements (e.g., `tank/core-services`, `tank/media-vault`, `tank/backups`).
* **Recordsize Optimization:**
    * **System/Database Datasets:** Fixed at **16k** for high-frequency small-block writes.
    * **General Storage Datasets:** Set to **128k** (Default).
    * **Media Datasets:** Set to **1M** to reduce metadata overhead and fragmentation for large files.

### 4.3 Decoupled Encryption & Key Management
Following Pillar 6, encryption is handled at the filesystem level, ensuring the physical substrate holds no usable data without active authorization.
* **Algorithm:** AES-256-GCM (Hardware accelerated).
* **The "Blind Server" Policy:** Master encryption keys are never stored on the local boot drive or pool metadata. 
* **Key Injection:** Pools remain locked at boot. Keys must be "injected" from a trusted mesh device over the **SecureNet** mesh before datasets are mounted. If the hardware is powered down or removed from the premises, the data remains mathematical noise.

### 4.4 Resilience: The 3-2-1-0 Strategy
* **Snapshots (Local Persistence):** Atomic, read-only snapshots are taken hourly and pruned according to a 24-hour / 30-day / 1-year retention policy.
* **Mirroring (Hardware Persistence):** Real-time redundancy via Mirrored (Core) or Parity-based (Archive) vdevs.
* **Off-site Archive (Global Persistence):** Encrypted, incremental backups via **Kopia** are pushed to S3-compatible storage.

### 4.5 Evolution Path: Compute/Storage Separation
To maintain simplicity while allowing for multi-node growth:
* **Phase 1 (Converged):** A single node acts as both the Core and Storage host.
* **Phase 2 (Distributed):** As the environment moves to a multi-node NixOS Cluster, storage is migrated to a dedicated node (NixOS or TrueNAS). 
* **Protocol:** Datasets are shared with the cluster nodes via high-speed, local VLAN-restricted NFS or SMB. This maintains simplicity while providing high-availability storage to the entire cluster.

---

## 5. The Security Substrate (Defense in Depth)

The security substrate is designed to provide proactive defense, isolation, and intelligent oversight. It follows the principle that "Hardening is a process, not a state."

### 5.1 Host-Level Hardening & Auditing
The underlying OS must be hardened to minimize the attack surface of the physical hardware.
* **Declarative Hardening (NixOS):** System state is defined in code, disabling unnecessary kernel modules and services by default.
* **Service Sandboxing (AppArmor):** Mandatory Access Control (MAC) profiles are applied to all high-risk services (e.g., Traefik, Matrix, Stalwart). This ensures that even if a service is compromised, it cannot read the root filesystem or access other service datasets.
* **Continuous Auditing (Lynis):** Automated security scans run weekly to identify configuration drift, outdated packages, or weak permissions. The "Hardening Index" from Lynis is reported directly to the NetSentinel for health tracking.

### 5.2 Intrusion Awareness & Proactive Defense
This layer monitors the "Wire" and the "Logs" for behavioral anomalies.
* **Network Sentry (NetAlertX):** Monitors the physical network substrate. It triggers immediate alerts for unauthorized MAC addresses or unrecognized device pings within the trusted VLANs.
* **Behavioral IPS (CrowdSec):** Acts as the "Immune System." It parses logs across all services to identify distributed brute-force attacks or L7 "scans" and blocks them at the firewall level.
* **Local Brute-Force Shield (Fail2Ban):** Provides high-speed, local banning for repeated authentication failures on critical infrastructure (SSH, Core Ops).

### 5.3 The SovrIT NetSentinel (Security SLM)
The NetSentinel is a dedicated Security Small Language Model (SLM) that acts as the intelligent "Overseer" of the substrate.
* **The Intelligence Engine:** Utilizes local, security-tuned models (e.g., **VaultGemma** or **Cyber-Llama**) running on the Compute/LLM Node.
* **Role: Alert Triage & Correlation:** Instead of flooding the user with raw logs, NetSentinel correlates disparate events. 
    * *Example:* Correlating a blocked SSH attempt (Fail2Ban) with a new device on the network (NetAlertX) to elevate the threat level.
* **Role: Autonomous Remediation (SOAR):** NetSentinel executes automated playbooks via **n8n**. 
    * *Action:* If a service exhibits compromised behavior, NetSentinel can autonomously "Quarantine" the container by dropping its mesh connection and notifying the user via **ntfy**.
* **Role: Log Summarization:** Provides a daily "Security Heartbeat" summary, translating technical log spikes into plain English for the user.

---

## 6. The Intelligence Layer
### 6.1 Assistant Architecture
* GPU/NPU acceleration requirements for real-time inference.
* Speech-to-Text (Whisper) and Text-to-Speech (Piper) latency targets.
### 6.2 Universal Search (Meilisearch)
* Scraping and indexing logic for decentralized file structures.

## 7. Resilience & High Availability
### 7.1 The Ghost Mirror (VPS)
* Minimum specs and hardening requirements.
* Failover orchestration logic for Identity (Authentik) and Vault services.
### 7.2 Automated Recovery Pipelines
* Use cases for n8n-driven container redeployment and state restoration.

## 8. Operational Continuity (The Living Handbook)
### 8.1 Documentation Standards
* Dokuwiki structure: Technical Docs vs. Human-Centric Procedures.
### 8.2 The AI Auditor Logic
* How the AI agent compares current Web UI DOM trees to existing handbook screenshots to detect "documentation drift."

## 9. Hardware Tiers & Performance Benchmarks
### 9.1 Infrastructure Tier (Core)
* Minimum CPU/RAM requirements for substrate stability.
### 9.2 Compute Tier (AI)
* Memory bandwidth requirements (M-series Pro/Max tiers).
### 9.3 Storage Tier
* Drive longevity targets and S.M.A.R.T. monitoring thresholds.

## 10. Service Directory & Engine Selection
*(Detailed technical justification for every tool listed in the README Acknowledgements—e.g., "Why Silverbullet over Obsidian?" or "Why Stalwart over Mailcow?").*



# SovrIT PTI

**SovrIT PTI** (Personal/Private Technology Infrastructure) is a high-performance, local-first infrastructure designed to reclaim digital sovereignty. It replaces the _**entire**_ suite of modern cloud-dependent services - identity, authentication, email/text communication, calendar, contacts, office/documents, medical/legal/financial records, media, even telephony and location services (and more) - with a unified, encrypted, and self-hosted ecosystem. 

SovrIT replaces reliance on ISP, mobile carrier, and third-party cloud services with a modular ecosystem you operate yourself - engineered to be used, understood, and maintained by anyone in your home.

---

## 🌱 Purpose & Mission

Most personal data today lives inside third‑party clouds you do not control. It is routinely inspected, analyzed, monetized, and used by the companies that store it, as well as by government agencies that increasingly disregard the spirit and intent of constitutional privacy protections. SovrIT exists to break that dependency by providing a stable, sovereign foundation for digital life — engineered and maintained with the same safeguards, discipline, and mission‑critical mindset found in enterprise IT environments.

Self‑hosting isolated services is not enough. True digital sovereignty requires that your data, your communications, and your daily digital operations be protected end‑to‑end. SovrIT enables you to become your own ISP and mobile carrier, paying traditional providers only for the raw bandwidth required to move encrypted data. Your information should belong to and be visible only to you.

---

## 5. The Seven Architectural Pillars of SovrIT PTI
### 1. Absolute Sovereignty & Zero-Trust Privacy
No third party holds the keys or has access to your data, identity, or mesh network. Where your data passes through servers that are not under your control (e.g. phone calls from a mobile device), they do so in encrypted form.
### 2. Autonomous Functional Resiliency
The system is _self-healing_. Continuous uptime monitoring is tethered to automated recovery pipelines that detect service degradation and trigger immediate rebuilds or relaunches. This ensures that the infrastructure maintains its own integrity without requiring manual intervention for routine failures.
### 3. Global High Availability & Failover Redundancy
SovrIT utilizes a geographically distant VPS Ghost Mirror to provide Ultra High Availability. Through automatic failover orchestration, critical services and data remain accessible even during local power outages, ISP failures, or catastrophic physical events like fire or theft.
### 4. Invisible & Active Security
Security is integrated into the user flow via biometrics (**WebAuthn**) and self-auditing,  proactive defense by SovrIT NetSentinel- a dedicated security-focused Small Language Model (SLM) that monitors system logs and NetAlertX heartbeats to identify and autonomously remediate complex threats.
### 5. Sovereign Voice/AI Assistance
The SovrIT Assistant serves as the primary gateway to the system's intelligence, serving as  both a voice and chat-based AI assistant. By utilizing local Large Language Models (LLMs) and high-fidelity speech-to-text engines, the assistant processes complex intents, performs multi-step research, and executes system automations entirely within the private network. This sovereign intelligence is natively integrated with the universal search index, allowing the SovrIT Assistant to provide context-aware insights from personal records while remaining 100% private and immune to third-party data collection
### 6. Decoupled Encryption at Rest
All data is secured using hardware-agnostic, filesystem-level encryption (AES-256-GCM). By decoupling encryption keys from physical hardware, the system ensures that data remains mathematically indistinguishable from noise if the servers are physically seized or compromised.
### 7. Operational Continuity - The Living Handbook
Comprehensive "Human-Centric" documentation walks users through procedures consisting of annotated screenshots. "Click the gear icon shown circled in red." An AI agent regularly reviews, autonomously updates, increments the revision number, and alerts the user when a new revision is available to be printed. This ensures the Handbook always matches precisely what the user sees on-screen-layout, menus, and dialog options - ensuring stress-free success and future confidence. This provides non-technical family members with a clear, visual roadmap to maintain and operate the system if the family IT person is unavailable.

---

## 🧩 SovrIT Ecosystem Overview

### SovrIT Core (Runtime Substrate)

The sovereign execution environment and foundational services:

* **SovrIT SecureNet:** Encrypted overlay network and sovereign VPN ([Netbird](https://netbird.io/)), paired with private, recursive DNS resolution ([AdGuard Home](https://github.com/AdguardTeam/AdGuardHome) + [Unbound](https://www.nlnetlabs.nl/projects/unbound/about/)) to eliminate third-party tracking at the query level.
* **SovrIT NetSentinel (The Security Substrate):** A dedicated, security-focused SLM that orchestrates active defense and employs automated remediation (with logging and user notifications) using:
    * **Network Intrusion Awareness:** [NetAlertX](https://github.com/jpsenior/netalertx) provides real-time monitoring of the network substrate, alerting immediately to unauthorized or unrecognized devices.
    * **Brute-Force Shield:** [Fail2Ban](https://github.com/fail2ban/fail2ban) provides local, signature-based protection by monitoring log files (SSH, Auth, etc.) and instantly banning IPs that exhibit aggressive login behavior.
    * **Behavioral IPS/IDS:** [CrowdSec](https://www.crowdsec.net/) monitors for malicious patterns across all services and blocks threats at the firewall level.
    * **Process Sandboxing:** [AppArmor](https://gitlab.com/apparmor/apparmor/-/wikis/home) isolates individual services, ensuring that a compromise in one module cannot move laterally through the infrastructure.
    * **Automated Hardening Audits:** [Lynis](https://cisofy.com/lynis/) performs regular security scans of the underlying host, identifying configuration drift and potential vulnerabilities before they can be exploited.
    * **Automated Security Countermeasues:** [n8n](https://n8n.io/) workflows to autonomously block/isolate threats, logging actions taken and notifying the user.

* **SovrIT Access:** Centralized identity and biometric gatekeeping ([WebAuthn](https://webauthn.guide/)), OIDC/SAML authentication ([Authentik](https://goauthentik.io/)), and private PKI ([Step-CA](https://smallstep.com/docs/step-ca/)). All traffic is orchestrated via sovereign ingress ([Traefik](https://traefik.io/)) for local SSL termination.
* **SovrIT Fortitude:** Resilience engine providing immutable backups ([Kopia](https://kopia.io/)), automated recovery ([n8n](https://n8n.io/)), and uptime monitoring ([Uptime Kuma](https://github.com/louislam/uptime-kuma)).
* **SovrIT Time:** Internal high-stratum time authority ([chrony](https://chrony-project.org/)) to ensure cryptographic and MFA synchronization during outages.
* **Core Ops:** Provisioning and lifecycle management utilizing NixOS for declarative system state, [TrueNAS CE](https://www.truenas.com/) for mission-critical encrypted storage (**ZFS**). Active defense is maintained via behavioral IP blocking (**CrowdSec**), mandatory access control (**AppArmor**), and automated security auditing (**Lynis**).

### SovrIT Modules
The user-facing applications that fulfill the functional requirements:

#### Intelligence & Discovery:
- **SovrIT Assistant:** Local voice/chat AI ([Ollama](https://ollama.com/)), transcription ([Whisper](https://github.com/SYSTRAN/faster-whisper)), and speech synthesis ([Piper](https://github.com/rhasspy/piper)).
- **SovrIT Search:** Lightning-fast universal discovery across all system data ([Meilisearch](https://www.meilisearch.com/)).
#### Communication & Social:
- **SovrIT Messenger:** Unified chat hub (WhatsApp/Signal/iMessage) via [Matrix](https://matrix.org/) and [Mautrix](https://mautrix.net/) bridges.
- **SovrIT Carrier:** Sovereign voice and telephony ([VitalPBX](https://www.vitalpbx.com/)) using SIP-TLS and SRTP for encrypted signaling and media.
- **SovrIT Mail:** Self-hosted email engine ([Stalwart](https://stalwart.io/)) utilizing an SMTP relay ([Mailgun](https://www.mailgun.com/)) to ensure global deliverability and a webmail client ([SnappyMail](https://snappymail.eu/)).
- **SovrIT Notify:** Unified cross-system notification gateway ([ntfy](https://ntfy.sh/)).
- **SovrIT Social:** Private social networking and photo blogging ([GoToSocial](https://gotosocial.org/)/[Pixelfed](https://pixelfed.org/)).
#### Productivity & Office:
- **SovrIT Office:** File management ([FileBrowser Quantum](https://filebrowser.org/)) and collaborative editing ([OnlyOffice](https://www.onlyoffice.com/)).
- **SovrIT Notes:** synchronized note-taking ([Silverbullet](https://silverbullet.md/)).
- **SovrIT Calendar/Contacts:** Sovereign schedules and people ([Radicale](https://radicale.org/)).
- **SovrIT Bookmarks:** Permanent article archiving and visual pinning ([Readeck](https://readeck.org/)).
- **SovrIT History:** Searchable web memory ([ArchiveBox](https://archivebox.io/)/[Promnesia](https://github.com/karlicoss/promnesia)).
#### Vital Archives:
- **SovrIT Money:** Financial auditing ([Actual Budget](https://actualbudget.org/)) with mobile receipt capture ([QuickScan](https://www.quickscanapp.com/)/[OpenScan](https://github.com/OpenScan-App/OpenScan)) and document OCR ([Paperless-ngx](https://docs.paperless-ngx.com/)/[Tika](https://tika.apache.org/)).
- **SovrIT Photos:** AI gallery and media management with ML-driven pruning ([Immich](https://immich.app/)).
- **SovrIT Med/Legal:** OCR-indexed health and estate records ([Paperless-ngx](https://docs.paperless-ngx.com/)/[Tika](https://tika.apache.org/)).
- **SovrIT Mobile:** Local, tethered device imaging and full data extraction via [libimobiledevice](https://libimobiledevice.org/) and [adb](https://developer.android.com/tools/adb).
- **SovrIT Eternal:** Digital dead-man switch for automated information handover ([Aeterna](https://alpyxn.github.io/aeterna/)).
- **SovrIT Handbook:** AI-audited documentation and manuals ([Dokuwiki](https://www.dokuwiki.org/)).
- **SovrIT Maps:** Private location services ([Traccar](https://www.traccar.org/)) and private vector mapping ([MapLibre](https://maplibre.org/)).
#### Passwords:
- **SovrIT Vault:** Secrets, passwords, and MFA recovery stewardship ([Vaultwarden](https://github.com/dani-garcia/vaultwarden)).
#### Media:
- **SovrIT Media:** Streaming and YouTube archiving ([Jellyfin](https://jellyfin.org/)/[TubeArchivist](https://tubearchivist.com/)).
- **SovrIT Books:** Ebook ([Kavita](https://www.kavitareader.com/)) and audiobook ([Audiobookshelf](https://www.audiobookshelf.org/)) library.
#### Home/Lifestyle
- **SovrIT Home:** Local-only smart home automation ([Home Assistant](https://www.home-assistant.io/)).
- **SovrIT Sentinel:** Intelligent local security/surveillance and AI NVR ([Alarmo](https://github.com/nielsfaber/alarmo)/[Frigate](https://frigate.video/)).

---

## 🏗️ Hardware Architecture

SovrIT PTI is designed to be hardware-agnostic but is currently optimized for a high-performance, low-wattage distributed model.

### 1. The Network
* **Substrate:** Router/Firewall & Wireless Access Points
* **Responsibilities:** WAN/Internet andd Wired/Wireless LAN connectivity, security, and VLAN-based network segmentation.

### 2. The Core/Storage Node
* **Substrate:** [NixOS](https://nixos.org/) (non-clustered) or [Proxmox VE](https://www.proxmox.com/en/products/proxmox-virtual-environment/overview) (high availability cluster); ([TrueNAS](https://www.truenas.com/) may be deployed as a separate/standalone NAS.)
* **Responsibilities:** [ZFS] Pool management, Identity ([Authentik]), Proxy ([Traefik]), and Core Modules.

### 3. Compute Node (Local LLM)
* **Recommended Hardware:** Apple Silicon - M1 or greater Pro or Max CPU with 16GB+ Unified Memory.
* **Benefit:** Unified Memory Architecture allows LLMs and Speech-to-Text engines to stay "hot" in memory, providing instant responses while drawing as little as 30W.

### 4. VPS (Ghost Mirror)
* **Recommended Configuration:** 4+ VCores, 6+ GB RAM, 100+ GB Disk space, 10+ TB Bandwidth, NixOS.
* **Benefit:** Hardened failover node for critical service continuity.

### 5. Mobile Endpoints
* **Biometric-Capable Devices:** Trusted nodes for secure remote access and identity verification.

### 6. Off-site Archive (S3 Storage)
* **Substrate:** S3-Compatible Object Storage (e.g., [Backblaze B2](https://www.backblaze.com/cloud-storage), [Wasabi](https://wasabi.com/), or remote [MinIO](https://min.io/) instance).
* **Responsibilities:** Immutable encrypted snapshots and geographical data redundancy.
* **Benefit:** Ensures data survival against local catastrophic events (fire, theft, or total hardware failure) by providing a "last resort" recovery target.

---

## 🗺️ Functionality Map
The following table outlines the specific capabilities of the SovrIT platform and the open-source engines that power them.

### 🛡️ Core Infrastructure & Security
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Identity & Access** | Centralized OIDC/SAML provider with biometric MFA (WebAuthn) via **Authentik**. |
| **Secure Mesh** | Peer-to-peer encrypted overlay network via **NetBird** (WireGuard) for zero-trust access. |
| **Active Mesh Defense** | Behavioral log analysis and automated IP banning via **CrowdSec**. |
| **Service Sandboxing** | Mandatory Access Control (MAC) using **AppArmor** to isolate service processes. |
| **Security Health Audit** | Automated periodic hardening assessments via **Lynis** with **ntfy** alerting. |
| **Network Entry Sentry** | Real-time discovery and alerting of new local network clients via **Home Assistant**. |
| **Credential Breach Audit** | Client-side monitoring for leaked vault credentials via **Vaultwarden** (HIBP integration). |
| **SovrIT NetSentinel** | AI-driven SecOps agent (Local SLM) that triages alerts and executes automated SOAR playbooks via **n8n**. |
| **Resiliency Engine** | Automated state backups, service monitoring, and self-healing via **Fortitude** (**Kopia** / **n8n**). |

### 🧠 Sovereign Intelligence
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Assistant** | Local, private Large Language Model (LLM) orchestration via **Ollama**. |
| **Knowledge Index** | High-performance full-text search across all sovereign data via **Meilisearch**. |
| **Sentinel** | AI-powered local NVR and intelligent object detection via **Frigate**. |

### 💬 Communication & Social
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Messenger** | Unified, bridged chat (WhatsApp/iMessage/Signal) via **Matrix** and **Mautrix**. |
| **Carrier** | Sovereign SMTP mail (**Stalwart**) and SIP-TLS voice telephony (**VitalPBX**). |
| **Social** | Privacy-focused, federated social networking via **Pixelfed** and **GoToSocial**. |

### 📅 Productivity & Knowledge
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **SovrIT Notes** | Lightweight, flat-file Markdown note-taking and documentation via **SilverBullet**. |
| **Office** | Collaborative document, spreadsheet, and presentation editing via **OnlyOffice**. |
| **History & Reading** | Permanent web archiving (**ArchiveBox**) and visual bookmarking (**Readeck**). |

### 📂 Vital Archives
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Money** | Privacy-first personal finance and envelope budgeting via **Actual Budget**. |
| **Records** | Long-term document management and OCR indexing via **Paperless-ngx**. |
| **Mobile** | Local Android/iOS data extraction and management via **adb** and **libimobiledevice**. |
| **Eternal** | Digital dead-man switch and automated legacy handover via **Aeterna**. |

### 🎬 Sovereign Media
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Cinema** | High-performance personal media streaming via **Jellyfin**. |
| **Library** | Digital management for books (**Kavita**) and audiobooks (**Audiobookshelf**). |
| **TubeArchivist** | Sovereign YouTube archiving and metadata management via **TubeArchivist**. |


## 🧩 SovrIT PTI: Functionality Map

### 🛡️ Core Infrastructure & Security
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Mesh Networking** | Encrypted P2P overlay network via [Netbird](https://netbird.io/) for secure inter-node communication. |
| **Universal Identity** | Centralized OIDC/SAML authentication and account brokering via [Authentik](https://goauthentik.io/). |
| **Biometric Gatekeeper** | Zero-friction MFA utilizing [WebAuthn](https://webauthn.guide/) (Face ID/TouchID) for all system access. |
| **Edge Traffic Control** | High-performance routing and automated SSL management via [Traefik](https://traefik.io/). |
| **At-Rest Encryption** | Hardware-agnostic filesystem encryption using [ZFS](https://openzfs.org/) with decoupled master keys. |
| **Secure Remote Access** | Mesh-only administrative management of server substrates via [Netbird](https://netbird.io/). |
| **Local Certificate Authority** | Trusted internal SSL certificate issuance for mesh-only domains via [Step-CA](https://smallstep.com/certificates/). |
| **Internal Time Server** | Local high-stratum NTP server for MFA and [ZFS](https://openzfs.org/) synchronization via [chrony](https://chrony-project.org/). |
| **Network Segmentation** | Isolation of IoT hardware into dedicated VLANs with zero outbound access. |
| **Air-Gapped IoT Radio** | Local-only sensor communication via physical Zigbee/Z-Wave protocols. |
| **MFA Recovery Vault** | Physical "Break-Glass" recovery procedure using paper-stored codes. |
| **Encryption Key Rotation** | P* **rocedure for rotating ([ZFS](https://openzfs.org/)) master keys and identity signing keys. |
| **Mobile Device Hardening** | Routing of all mobile traffic through the mesh with "Always-On" VPN logic. |
| **Physical Asset Tracking** | Encrypted inventory of all physical hardware within the ([Dokuwiki](https://www.dokuwiki.org/)) Handbook. |

### 🔄 Resilience & Maintenance
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Insta-Restore Engine** | Automated rebuild pipelines for core services using [n8n](https://n8n.io/) and [Ansible](https://www.ansible.com/). |
| **Immutable Backups** | Hourly, encrypted client-side backups to offsite storage via [Kopia](https://kopia.io/). |
| **Remote Failover Mirror** | High-availability "Ghost Mirror" on a remote VPS for Identity and Vault access. |
| **Graceful Power Safety** | Automated UPS-triggered shutdown sequences for storage and compute nodes. |
| **Versioned Infrastructure** | State reproducibility using configurations stored in a private ([Forgejo](https://forgejo.org/)) instance. |
| **The Living Handbook** | Database-less, human-centric documentation maintained in [Dokuwiki](https://www.dokuwiki.org/). |
| **Database Atomic Snapshots** | Coordinated filesystem snapshots for consistent point-in-time recovery. |
| **Digital Dead-Man Switch** | Automated information handover to beneficiaries via [Aeterna](https://alpyxn.github.io/aeterna/) if system heartbeat is not detected for 30 days. |
| **Automated Health Reports** | Weekly reporting on disk wear, backup integrity, and authentication attempts. |
| **Log Aggregation** | Centralized, encrypted log management for auditing and troubleshooting. |
| **Snapshot Pruning Logic** | Automated thinning of ([ZFS](https://openzfs.org/)) snapshots to optimize space. |
| **Gateway Dashboard** | Unified web interface for all services using [Flame](https://github.com/pawelmalak/flame). |
| **Resource Quotas** | Strict CPU/RAM limits to ensure Identity and Resilience responsiveness. |
| **Zero-Log App Config** | Disabling of identifiable debug logs to disk in favor of central aggregation. |
| **Bandwidth QoS** | Prioritization of mesh-failover and telephony traffic over media sync. |
| **Hardware Wear Monitoring** | S.M.A.R.T. data monitoring to trigger alerts when drive life is critical via [Uptime Kuma](https://github.com/louislam/uptime-kuma). |

### 🧠 Sovereign Intelligence
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Local AI Assistant** | Private voice and chat intelligence using [Ollama](https://ollama.com/), [Whisper](https://github.com/SYSTRAN/faster-whisper), and [Piper](https://github.com/rhasspy/piper). |
| **Universal Sovereign Search** | Exhaustive, real-time discovery across all system data via [Meilisearch](https://www.meilisearch.com/). |
| **AI Handbook Auditor** | Automated agent that audits UIs to keep documentation screenshots in parity. |
| **Local AI NVR** | Hardware-accelerated object detection for feeds via [Frigate](https://frigate.video/). |

### 📞 Communication & Social
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Unified Messenger Hub** | Centralized chat history bridging external networks into [Matrix](https://matrix.org/) via [Mautrix](https://mautrix.net/) bridges. |
| **Encrypted Telephony** | Private voice communication via [VitalPBX](https://www.vitalpbx.com/) using SIP-TLS and SRTP. |
| **SovrIT Notify** | Unified cross-system notification gateway powered by ([ntfy](https://ntfy.sh/)). |
| **Sovereign Mail Engine** | Self-hosted email engine ([Stalwart](https://stalwart.io/)) utilizing a web-based mail client ([SnappyMail](https://snappymail.eu/)) and SMTP relay ([Mailgun](https://www.mailgun.com/)). |
| **Sovereign Social Feed** | Privacy-focused social networking via [GoToSocial](https://gotosocial.org/) and [Pixelfed](https://pixelfed.org/). |

### 📂 Productivity & The Virtual Office
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Integrated Virtual Office** | File management via [FileBrowser Quantum](https://filebrowser.org/) and collaborative editing via [OnlyOffice](https://www.onlyoffice.com/). |
| **Notes** | Note-taking and synchronization via [Silverbullet](https://silverbullet.md/). |
| **Permanent Bookmarking** | Article archiving as searchable PDFs via [Readeck](https://readeck.org/). |
| **Web Memory & History** | Comprehensive web archiving via [ArchiveBox](https://archivebox.io/) and [Promnesia](https://github.com/karlicoss/promnesia). |
| **Schedules & People** | Sovereign calendar and contact synchronization via [Radicale](https://radicale.org/). |
| **Encrypted Temp-Sharing** | Mechanism for sharing large files via auto-expiring, protected links. |
| **P2P Asset Sync** | Direct, encrypted synchronization between mobile devices and the home node. |

### 🗄️ Vital Archives & Records
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Financial Auditor** | Receipt capture via [QuickScan](https://www.quickscanapp.com/)/[OpenScan](https://github.com/OpenScan-App/OpenScan) and analysis via [Actual Budget](https://actualbudget.org/). |
| **Vital Records** | OCR-indexed medical and legal archives utilizing [Paperless-ngx](https://docs.paperless-ngx.com/)/[Tika](https://tika.apache.org/). |
| **AI Photo Management** | High-performance gallery with ML deduplication via [Immich](https://immich.app/). |
| **SovrIT Mobile** | Local, tethered device imaging and full data extraction via [libimobiledevice](https://libimobiledevice.org/) and [adb](https://developer.android.com/tools/adb). |
| **Digital Library** | Hosting for e-books and audiobooks via [Kavita](https://www.kavitareader.com/) and [Audiobookshelf](https://www.audiobookshelf.org/). |
| **Private Geolocation** | Location tracking via [Traccar](https://www.traccar.org/) with private mapping via [MapLibre](https://maplibre.org/). |
| **OCR Record Archive** | Automated full-text indexing of all uploaded PDFs for instant retrieval via [Paperless-ngx](https://docs.paperless-ngx.com/)/[Tika](https://tika.apache.org/). |
| **Media & YouTube Hub** | Streaming via [Jellyfin](https://jellyfin.org/) and local YouTube archiving via [TubeArchivist](https://tubearchivist.com/). |

---

## 💰 Cost of Sovereignty: Financial Impact

It is a common misconception that self-hosting is a "budget-saving" endeavor. While SovrIT PTI can eventually eliminate hundreds of dollars in monthly "subscription creep," it is not designed to save money. You build a Digital Fortress because you value privacy, data integrity, and security — not to find a bargain.

### 1. Initial Capital Expenditure (The Setup)
A setup guide with equipment selection considerations is forthcoming but for a **Ballpark Estimate:** A 2-node (1 x Core/Storage, 1 x Compute/LLM) SovrIT setup could be assembled for as little as **$600**. For a robust, high-availability (HA) cluster with at least three cluster nodes, and an upgraded AI compute node, the entry-level price typically starts at **$800 to $1,000**.

* **The Proxmox Cluster:** For high availability, you need at least three nodes. This can be achieved with three inexpensive mini-PCs or used thin clients. Alternatively, you can use two main nodes and a low-powered device like a Raspberry Pi acting as a [Corosync Quorum Device](https://pve.proxmox.com/pve-docs/chapter-pvecm.html#_corosync_external_vote_support) to maintain quorum if one node fails.

* **The Storage Node:** A ZFS mirror (2 drives) is the minimum for data integrity. 
    * **Budget:** 2x 4-8TB NAS-grade drives (~$160–$220 total).
    * **Scale:** High-capacity 12TB+ drives remain the largest expense for media-heavy users.

* **The AI Compute Node (Apple Silicon):** Apple Silicon is the gold standard for high-performance, low-wattage AI. RAM capacity (at least 16GB, preferably 32GB+) is more critical than chip generation but bandwidth is king so the chip tier matters a lot for performance:

| Chip Tier | Memory Bandwidth (Est.) | LLM Performance (2026) |
| :--- | :--- | :--- |
| **Base (M1/M2/M3)** | **68 – 100 GB/s** | Small models (3B–8B) only. Feels sluggish on anything larger. |
| **Pro (M1–M5 Pro)** | **200 – 307 GB/s** | **The Sweet Spot.** Instant response (30+ tokens per second) on 8B–14B models. |
| **Max (M1–M5 Max)** | **400 – 614 GB/s** | **High Performance.** Runs 30B–70B models at human reading speeds. |

### 2. Operational Expenditure (The Ongoing Cost)
* **The Ghost Mirror:** A remote VPS is required for failover orchestration. While monthly plans from providers like Hostinger or DigitalOcean typically run **$5–$15**, bargain nodes (2vCPU/4GB RAM) can be found via annual promotional deals for as little as **$45–$60/year**.
* **Immutable Backups:** Offsite S3-compatible storage ([Backblaze B2](https://www.backblaze.com/cloud-storage) or [Wasabi](https://wasabi.com/)) costs roughly **$0.005/GB**. To model costs including ingress and egress fees, consult [The 2026 Cloud Storage Pricing Guide](https://www.cloudzero.com/blog/cloud-storage-pricing/).
* **Electricity:** A 4-node stack idles at **50W–70W**, typically costing **less than $10/month**.

### 3. Comparison to Third-Party Services
Cloud subscriptions (Google Workspace, iCloud+, Dropbox, Netflix, Spotify, and AI) typically cost households **$50–$200/month**. 

| Service Type | Cloud Monthly Cost | SovrIT Equivalent |
| :--- | :--- | :--- |
| **Identity/Storage** | $10 - $30 | SovrIT Access / Office (ZFS) |
| **Premium AI** | $20 - $30 | SovrIT Assistant (Local) |
| **Media/Music** | $15 - $40 | SovrIT Media / Books |
| **Privacy/VPN** | $10 - $15 | SovrIT SecureNet ([Netbird](https://netbird.io/)) |

### 4. Strategy for Minimizing Costs
* **Used Enterprise Gear:** Thin clients like the Dell Wyse 5070 or HP T640 are designed for 24/7 operation and are much more efficient than consumer PCs. Ranging in price from $60 – $150, these high efficiency devices are perfect for core substrate services with an excellent balance of modern CPU and low idle power.
* **"Cracked" Brains:** Search for M1 Pro MacBooks with "cracked screens" or "broken LCDs." In 2026, these sell for **$300–$400**, providing enterprise-grade AI compute at a 60% discount. As a bonus, they have their own built in UPS!
* **Start Small:** Launch the **SovrIT Core** on two nodes (Core/Storage + Compute/LLM) first. Add the Ghost Mirror once you have the Core up. High Availability is a great goal but not a Day 1 requirement.

---

## 📜 License & Ethical Usage
The SovrIT PTI blueprint is provided for individual sovereignty. By deploying this stack, you assume total responsibility for your data security and the legal implications of hosting your own communication and encryption services.


## 🙏 Acknowledgements
SovrIT stands firmly on the shoulders of giants. It would not exist without the incredible work of the open‑source communities whose tools and ideas form its foundation.

- [**Actual Budget**](https://actualbudget.org/) — privacy-first personal finance and envelope budgeting
- [**adb**](https://developer.android.com/tools/adb) — versatile command-line tool for Android device communication
- [**Aeterna**](https://github.com/alpyxn/aeterna) — digital dead-man switch logic for automated information handover
- [**Ansible**](https://www.ansible.com/) — declarative provisioning and automated infrastructure configuration
- [**AppArmor**](https://gitlab.com/apparmor/apparmor/-/wikis/home) — mandatory access control and kernel-level process sandboxing
- [**ArchiveBox**](https://archivebox.io/) / [**Promnesia**](https://github.com/karlicoss/promnesia) — comprehensive web history archiving and exploration
- [**Authentik**](https://goauthentik.io/) — centralized identity provider and biometric authentication gateway
- [**chrony**](https://chrony-project.org/) — versatile implementation of the Network Time Protocol (NTP)
- [**CrowdSec**](https://www.crowdsec.net/) — behavior-based security engine and automated IP bouncer
- [**Cyber-Llama / VaultGemma**](https://huggingface.co/models) — specialized small language models (SLM) tuned for local security operations and log triage
- [**Docker**](https://www.docker.com/) — containerization and modular service deployment
- [**Dokuwiki**](https://www.dokuwiki.org/) — lightweight, database-less documentation for maximum resiliency
- [**FFmpeg**](https://ffmpeg.org/) — the "Swiss Army knife" of media processing powering Jellyfin, Frigate, and TubeArchivist
- [**FileBrowser Quantum**](https://filebrowser.org/) — web-based file management and remote access
- [**Flame**](https://github.com/pawelmalak/flame) — aesthetic, protected dashboard for all sovereign services
- [**Forgejo**](https://forgejo.org/) — lightweight self-hosted git service for infrastructure-as-code
- [**Frigate**](https://frigate.video/) — AI-powered local NVR and intelligent object detection
- [**Home Assistant**](https://www.home-assistant.io/) — the heart of local-only, cloud-independent smart home automation
- [**Hugging Face**](https://huggingface.co/) — LLM/AI frameworks for guided operations and documentation auditing
- [**Immich**](https://immich.app/) — high-performance, AI-driven photo and video management
- [**Jellyfin**](https://jellyfin.org/) — high-performance personal media streaming
- [**Kavita**](https://www.kavitareader.com/) / [**Audiobookshelf**](https://www.audiobookshelf.org/) — decentralized digital libraries for books and audio
- [**Kopia**](https://kopia.io/) — fast, secure, and incremental encrypted backups
- [**libimobiledevice**](https://libimobiledevice.org/) — cross-platform protocol library for native iOS communication
- [**llama.cpp**](https://github.com/ggerganov/llama.cpp) — foundational inference engine enabling local LLMs on consumer hardware
- [**Lynis**](https://cisofy.com/lynis/) — battle-tested security auditing tool for hardening Linux systems
- [**Mailgun**](https://www.mailgun.com/) — high-reputation SMTP relay for sovereign mail invisibility
- [**Matrix**](https://matrix.org/) / [**Mautrix**](https://mautrix.net/) — decentralized communication hub and bridge architecture
- [**Meilisearch**](https://www.meilisearch.com/) — lightning-fast local search engine for all personal data
- [**n8n**](https://n8n.io/) — low-code workflow automation and service integration
- [**NetBird**](https://netbird.io/) / [**WireGuard**](https://www.wireguard.com/) — encrypted overlay networking and high-performance VPN protocols
- [**NixOS**](https://nixos.org/) — declarative and reproducible operating system configuration
- [**ntfy**](https://ntfy.sh/) — unified, lightweight notification gateway
- [**Ollama**](https://ollama.com/) — local large language model (LLM) orchestration
- [**OnlyOffice**](https://www.onlyoffice.com/) — collaborative document editing and office suite
- [**Paperless-ngx**](https://docs.paperless-ngx.com/) — powerful document management and OCR indexing
- [**Piper**](https://github.com/rhasspy/piper) — fast, local text-to-speech synthesis
- [**Pixelfed**](https://pixelfed.org/) / [**GoToSocial**](https://gotosocial.org/) — privacy-focused, federated social networking
- [**Proxmox**](https://www.proxmox.com/en/products/proxmox-virtual-environment/overview) — enterprise-grade virtualization and orchestration
- [**Python**](https://www.python.org/) — scripting, tooling, and automation logic
- [**QuickScan**](https://www.quickscanapp.com/) / [**OpenScan**](https://github.com/OpenScan-App/OpenScan) — mobile document capture with local processing
- [**Radicale**](https://radicale.org/) — lightweight CalDAV/CardDAV for calendars and contacts
- [**Readeck**](https://readeck.org/) — permanent article archiving and visual bookmarking
- [**SilverBullet**](https://silverbullet.md/) — extensible, flat-file Markdown personal knowledge base
- [**SnappyMail**](https://snappymail.eu/) — modern, privacy-focused web-based email client
- [**Stalwart**](https://stalwart.io/) — modern, memory-safe sovereign email server
- [**Step-CA**](https://smallstep.com/certificates/) — internal certificate authority for private mesh encryption
- [**Tika**](https://tika.apache.org) — metadata and text extraction from complex file types
- [**Traccar**](https://www.traccar.org/) / [**MapLibre**](https://maplibre.org/) — private location tracking and sovereign mapping
- [**Traefik**](https://traefik.io/) — cloud-native edge proxy and automated traffic management
- [**TubeArchivist**](https://tubearchivist.com/) / [**yt-dlp**](https://github.com/yt-dlp/yt-dlp) — sovereign YouTube archiving and the underlying download engine
- [**Uptime Kuma**](https://github.com/louislam/uptime-kuma) — self-hosted uptime monitoring and service alerts
- [**Vaultwarden**](https://github.com/dani-garcia/vaultwarden) — lightweight secret management and MFA recovery stewardship
- [**VitalPBX**](https://www.vitalpbx.com/) — sovereign voice-over-IP (VoIP) and telephony
- [**WebAuthn**](https://webauthn.guide/) — biometric MFA standard for secure, passwordless access
- [**Whisper**](https://github.com/SYSTRAN/faster-whisper) — high-fidelity local speech-to-text transcription
- [**ZFS**](https://openzfs.org/) — resilient, hardware-agnostic, and encrypted storage foundations


## 🙏 Acknowledgements
SovrIT stands firmly on the shoulders of giants. It would not exist without the incredible work of the open‑source communities whose tools and ideas form its foundation.

- [**Actual Budget**](https://actualbudget.org/) — privacy-first personal finance and envelope budgeting
- [**adb**](https://developer.android.com/tools/adb) — versatile command-line tool for Android device communication and data extraction
- [**Aeterna**](https://github.com/alpyxn/aeterna) — digital dead-man switch logic for automated information handover
- [**Ansible**](https://www.ansible.com/) — declarative provisioning and automated infrastructure configuration
- [**AppArmor**](https://gitlab.com/apparmor/apparmor/-/wikis/home) isolates individual services, preventing a compromise in one module from compromising others.
- [**ArchiveBox**](https://archivebox.io/) / [**Promnesia**](https://github.com/karlicoss/promnesia) — comprehensive web history archiving and exploration
- [**Authentik**](https://goauthentik.io/) — centralized identity provider and biometric authentication gateway
- [**CrowdSec**](https://www.crowdsec.net/) monitors network for malicious patterns across all services and blocks threats at the firewall level.
- [**chrony**](https://chrony-project.org/) — versatile implementation of the Network Time Protocol (NTP) for local synchronization
- [**Docker**](https://www.docker.com/) — containerization and modular service deployment
- [**Dokuwiki**](https://www.dokuwiki.org/) — lightweight, database-less documentation for maximum resiliency
- [**Fail2Ban**](https://github.com/fail2ban/fail2ban) - bans attackers that cause multiple authentication errors
- [**FFmpeg**](https://ffmpeg.org/) — the "Swiss Army knife" of media processing powering Jellyfin, Frigate, and TubeArchivist
- [**FileBrowser Quantum**](https://filebrowser.org/) — web-based file management and remote access
- [**Flame**](https://github.com/pawelmalak/flame) — aesthetic, protected dashboard for all sovereign services
- [**Forgejo**](https://forgejo.org/) — lightweight self-hosted git service for infrastructure-as-code
- [**Frigate**](https://frigate.video/) — AI-powered local NVR and intelligent object detection
- [**Home Assistant**](https://www.home-assistant.io/) — the heart of local-only, cloud-independent smart home automation
- [**Hugging Face**](https://huggingface.co/) — LLM/AI frameworks for guided operations and documentation auditing
- [**Immich**](https://immich.app/) — high-performance, AI-driven photo and video management
- [**Jellyfin**](https://jellyfin.org/) — high-performance personal media streaming
- [**Kavita**](https://www.kavitareader.com/) / [**Audiobookshelf**](https://www.audiobookshelf.org/) — decentralized digital libraries for books and audio
- [**Kopia**](https://kopia.io/) — fast, secure, and incremental encrypted backups
- [**libimobiledevice**](https://libimobiledevice.org/) — cross-platform protocol library to communicate with iOS devices natively
- [**llama.cpp**](https://github.com/ggerganov/llama.cpp) — the foundational inference engine enabling local LLMs on consumer hardware
- [**Lynis**](https://cisofy.com/lynis/) performs regular security scans to identify potential vulnerabilities.
- [**Mailgun**](https://www.mailgun.com/) — high-reputation SMTP relay to prevent outbound mail from being flagged as spam
- [**Matrix**](https://matrix.org/) / [**Mautrix**](https://mautrix.net/) — decentralized communication hub and bridge architecture
- [**Meilisearch**](https://www.meilisearch.com/) — lightning-fast local search engine for all personal data
- [**n8n**](https://n8n.io/) — low-code workflow automation and service integration
- [**NetAlertX**](https://github.com/jpsenior/netalertx) provides real-time monitoring and  immediate alerting to unauthorized network devices.
- [**NetBird**](https://netbird.io/) / [**WireGuard**](https://www.wireguard.com/) — encrypted overlay networking and the high-performance protocol powering sovereign VPNs
- [**NixOS**](https://nixos.org/) — declarative and reproducible operating system configuration
- [**ntfy**](https://ntfy.sh/) — unified, lightweight notification gateway
- [**Ollama**](https://ollama.com/) — local large language model (LLM) orchestration
- [**OnlyOffice**](https://www.onlyoffice.com/) — collaborative document editing and office suite
- [**Paperless-ngx**](https://docs.paperless-ngx.com/) — powerful document management and OCR indexing
- [**Piper**](https://github.com/rhasspy/piper) — fast, local text-to-speech synthesis
- [**Pixelfed**](https://pixelfed.org/) / [**GoToSocial**](https://gotosocial.org/) — privacy-focused, federated social networking
- [**Proxmox**](https://www.proxmox.com/en/products/proxmox-virtual-environment/overview) — enterprise-grade virtualization and orchestration
- [**Python**](https://www.python.org/) — scripting, tooling, and automation logic
- [**QuickScan**](https://www.quickscanapp.com/) / [**OpenScan**](https://github.com/OpenScan-App/OpenScan) — mobile document capture with local processing
- [**Radicale**](https://radicale.org/) — lightweight CalDAV/CardDAV for calendars and contacts
- [**Readeck**](https://readeck.org/) — permanent article archiving and visual bookmarking
- [**Silverbullet**](https://silverbullet.md/) — PWA note-taking and sync
- [**SnappyMail**](https://snappymail.eu/) — modern, privacy-focused web-based email client
- [**Stalwart**](https://stalwart.io/) — modern, memory-safe sovereign email server
- [**Step-CA**](https://smallstep.com/certificates/) — internal certificate authority for private mesh encryption
- [**Tika**](https://tika.apache.org) — metadata and text extraction from complex file types
- [**Traccar**](https://www.traccar.org/) / [**MapLibre**](https://maplibre.org/) — private location tracking and sovereign mapping
- [**Traefik**](https://traefik.io/) — cloud-native edge proxy and automated traffic management
- [**TubeArchivist**](https://tubearchivist.com/) / [**yt-dlp**](https://github.com/yt-dlp/yt-dlp) — sovereign YouTube archiving and the underlying engine that makes it possible
- [**Uptime Kuma**](https://github.com/louislam/uptime-kuma) — self-hosted uptime monitoring and service alerts
- [**Vaultwarden**](https://github.com/dani-garcia/vaultwarden) — lightweight secret management and MFA recovery stewardship
- [**VitalPBX**](https://www.vitalpbx.com/) — sovereign voice-over-IP (VoIP) and telephony
- [**WebAuthn**](https://webauthn.guide/) — biometric MFA standard for secure, passwordless access
- [**Whisper**](https://github.com/SYSTRAN/faster-whisper) — high-fidelity local speech-to-text transcription
- [**ZFS**](https://openzfs.org/) — resilient, hardware-agnostic, and encrypted storage foundations
