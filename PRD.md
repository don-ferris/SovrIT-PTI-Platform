# SovrIT PTI (Personal /Private Technology Infrastructure) - Product Requirements Document

## 1. Header & Metadata
* **Status:** Draft 
* **Owner:** @don-ferris
* **Stakeholders:** @TBD
* **Target Release:** Version 1.0

---

## 2. Executive Summary
### Objective


### The Problem
[Describe the pain point. Why does this need to exist? What is broken or missing?]

### Business Value
[How does this impact the bottom line or user growth? Specify targets, e.g., "Reduce support tickets by 15%".]

---

## 3. Target Audience
### User Personas
* **[Persona A]:** [Brief description of user type and their specific need.]
* **[Persona B]:** [Brief description.]

### User Stories
| ID | As a... | I want to... | So that... |
| :--- | :--- | :--- | :--- |
| US-1 | [User type] | [Action] | [Benefit/Value] |
| US-2 | [User type] | [Action] | [Benefit/Value] |

---

## 4. Functional Requirements
| ID | Feature Name | Priority | Requirement Description |
| :--- | :--- | :--- | :--- |
| FR-1 | [Feature] | **P0** | [Must-have functionality] |
| FR-2 | [Feature] | **P1** | [Should-have functionality] |
| FR-3 | [Feature] | **P2** | [Nice-to-have / Future polish] |

---

## 5. User Flow & Design
* **Workflow:** [Link to flow diagram or step-by-step text description]
* **Figma/Design Link:** https://proto.io/
* **UI Constraints:** [e.g., Dark mode support required, Mobile-first layout]

---

## 6. Non-Functional Requirements
* **Performance:** [e.g., API response time < 200ms]
* **Security:** [e.g., Multi-factor authentication, end-to-end encryption]
* **Availability:** [e.g., 99.9% uptime requirement]

---

## 7. Analytics & Success Metrics
### Key Performance Indicators (KPIs)
* **Primary Metric:** [e.g., % of users who complete the checkout flow]
* **Secondary Metric:** [e.g., Average time spent on page]

### Tracking Plan
* [Event Name]: [Trigger Condition]
* [Event Name]: [Trigger Condition]

---

## 8. Out of Scope
* [Feature or functionality specifically excluded from this version.]
* [Integration with third-party platform X.]

---

## 9. Appendix & Risks
* **Technical Risks:** [Potential blockers or dependencies]
* **Glossary:** [Definition of internal terms or acronyms]









===============================
===============================
===============================











# Executive Summary: The SovrIT Project
**Mission:** Total Digital Independence
**Vision:** A world where individuals own their data, their history, and their future — with absolute sovereignty.
## 1. The Problem: Data Serfdom
We currently live our digital lives on "rented land." Our family photos, medical records, and private conversations are stored on servers owned by a handful of corporations. This isn't just a privacy issue; it’s a dependency issue. If a provider changes their terms, raises prices, or discontinues the service, you lose your history and must scramble to find an acceptable replacement. You are a tenant in a digital ecosystem where you don't own the dirt, the walls, or the locks.
## 2. The Solution: SovrIT PTI
**SovrIT PTI (Personal/Private Technology Infrastructure)** is a blueprint for independence. It is a "Digital Fortress" built on hardware you own, running software you control. It replaces the "Cloud" with a private, invisible network that is accessible globally — to you and only you.
## 3. The Pillars of Sovereignty
 * **Encryption at Rest:** All data is mathematically unreadable without your specific encryption keys. Even if the physical hardware is seized, the information remains a secret.
 * **Global Redundancy:** SovrIT utilizes a remote VPS acting as a "Ghost Mirror" with automatic failover. If the home system goes offline due to power or internet outages, your critical services and documentation remain live and accessible from anywhere in the world.
 * **Functional Resiliency:** Through automated backups, "One-Click" restorations, and human-centric procedures for when automated disaster recovery isn’t possible, your digital life is impervious to hardware failures, hackers, ransomware, and evolving threats.
 * **The Human Factor:** SovrIT incorporates a physical "Operating Manual" with procedures consisting of always-up-to-date annotated screenshots that anyone can follow — even if the family IT person is unavailable.
## 4. The 10-Phase Roadmap to Independence
The journey to sovereignty is a methodical transition from a fragile digital existence to a robust, self-sustaining legacy:
 * **Phase 0 (The Substrate):** Establishing the encrypted mesh and unreadable storage foundation.
 * **Phase 1 (The Gatekeeper):** Centralizing identity with physical security keys and biometrics.
 * **Phase 2 (Daily Essentials):** Migrating files, passwords, and calendars to your private vault.
 * **Phase 3 (The Searchable Life):** Digitizing life’s paper trail into a secure, searchable archive.
 * **Phase 4 (The iCloud Killer):** Local AI photo galleries and private social feeds.
 * **Phase 5 (The Personal AI):** A local AI assistant that audits the system and updates the Operating Manual.
 * **Phase 6 (The Unkillable System):** High-availability clusters and automated cloud-restoration.
 * **Phase 7 (Sovereign Carrier):** Becoming your own phone company with unified messaging.
 * **Phase 8 (SovrIT Habitat):** Local-only home automation that works without an internet connection.
 * **Phase 9 (SovrIT Sentinel):** Private surveillance that big tech and insurance companies cannot see.
### 🛡️ Ownership Starts Here
By the end of this roadmap, the "Cloud" isn't someone else's computer—it's yours. SovrIT PTI ensures that your data remains where it belongs: under your roof and under your control.



























===============================
===============================
===============================












# ProjectPlan.md: SovrIT PTI (Personal Technology Infrastructure)

## 🏛️ Vision & Architectural Pillars
**SovrIT PTI** is a permanent, sovereign extension of the user's life. It is built on three non-negotiable pillars:
1. **Zero-Trust Sovereignty:** No third-party (Apple, Google, Insurance Co.) has access to data or metadata.
2. **Encryption at Rest (The Fortress Protocol):** All data is encrypted via **AES-256-GCM** at the filesystem level. Keys are decoupled from physical hardware, requiring remote mesh-auth or manual passphrases to unlock. If hardware is seized, the data is unreadable noise.
3. **Operational Continuity (The Krista Test):** The system is documented in a physical, AI-audited **Handbook** ensuring a "Zero-Power" recovery path for family members.

---

## 🗺️ The 10-Phase Roadmap

### Phase 0: The Substrate & Fortress Protocol
**Goal:** Establish the encrypted mesh and physical data protection.
* **OS:** [Ubuntu 26.04 LTS](https://ubuntu.com/) Minimal on all nodes.
* **SecureNet:** [Netbird](https://netbird.io/) P2P mesh overlay; all public ports closed via UFW.
* **Storage:** [OpenZFS](https://openzfs.org/) with native encryption. Remote key loading via the VPS/Netbird tunnel.
* **Logbook:** [Dokuwiki](https://www.dokuwiki.org/) (Flat-file) for as-built documentation.
* **Gateway:** [Caddy](https://caddyserver.com/) for internal mesh SSL and automated proxying.

### Phase 1: Sovereignty Foundation (Identity)
**Goal:** Centralized, memory-safe identity managed via GitOps.
* **Core IdP:** [Kanidm](https://kanidm.github.io/kanidm/) (Rust-based) Identity Provider.
* **MFA:** [WebAuthn](https://webauthn.io/) (Passkeys/Biometrics) for daily use; [Yubikeys](https://www.yubico.com/products/yubikey-5-series/) for physical recovery.
* **Management:** [Forgejo](https://forgejo.org/) hosted `users.yml` synced via [Ansible](https://www.ansible.com/).

### Phase 2: User Assets & Gateway (Daily Driver)
**Goal:** The human interface and primary cloud replacement.
* **Gateway:** [Flame Dashboard](https://github.com/pawelmalak/flame) (Internal Mesh only).
* **Vault:** [Vaultwarden](https://github.com/dani-garcia/vaultwarden) (SQLite-based Bitwarden API).
* **Sync:** [Syncthing](https://syncthing.net/) for encrypted P2P file transport.
* **PIM:** [Radicale](https://radicale.org/) (Flat-file) for private Contacts/Calendars.
* **Web Office:** [FileBrowser](https://filebrowser.org/) + [OnlyOffice](https://www.onlyoffice.com/) for document management.

### Phase 3: Vital Records (The Searchable Life)
**Goal:** Digitizing medical, legal, and financial history.
* **Archive:** [Paperless-ngx](https://docs.paperless-ngx.com/) (SQLite) with OCR indexing.
* **SpendTracker:** [QuickScan](https://getquickscan.app/) (iOS) ➔ Syncthing ➔ Paperless matching.
* **Ledger:** [Actual Budget](https://actualbudget.org/) (SQLite) for private finance.
* **Legacy:** [Aeterna](https://github.com/reallibreboard/aeterna) (Dead Man's Switch) for info handover.

### Phase 4: Sovereign Media & Presence (The iCloud Killer)
**Goal:** Cancellation of all big-tech media subscriptions.
* **Photos:** [Immich](https://immich.app/) for auto-backup and local AI facial recognition.
* **Social:** [GoToSocial](https://gotosocial.org/) (SQLite) for private microblogging.
* **Visual Blog:** [Pixelfed](https://pixelfed.org/) (Instagram replacement).
* **Email:** [Stalwart Mail](https://stalwart.io/) (Rust/SQLite) JMAP/IMAP/SMTP server.

### Phase 5: SovrIT Assistant (AI Handbook Auditor)
**Goal:** A local AI that keeps the documentation and the user in sync.
* **Brain:** [Ollama](https://ollama.com/) hosting local LLMs (Llama 3 / Llava).
* **Auditor:** [Playwright](https://playwright.dev/) for automated UI screenshot auditing.
* **Chat:** [LibreChat](https://www.librechat.ai/) interface for mobile system queries.

### Phase 6: SovrIT Fortitude (Resiliency & Insta-Restore)
**Goal:** Functional immortality via HA clusters and S3 cold storage.
* **HA Cluster:** [Proxmox VE](https://www.proxmox.com/) High-Availability environment.
* **Offsite Vault:** [Kopia](https://kopia.io/) encrypted backups to [Cloudflare R2](https://www.cloudflare.com/developer-platform/r2/).
* **Restore Logic:** [n8n](https://n8n.io/) + Ansible for "couple-click" service rebuilding.
* **Watchman:** [Uptime Kuma](https://uptime.kuma.pet/) for health monitoring and failover triggers.

### Phase 7: Sovereign Carrier (Communication)
**Goal:** Own your phone number and unify your messaging.
* **Voice PBX:** [VitalPBX](https://www.vitalpbx.com/) with SIP-TLS/SRTP encryption.
* **Messaging:** [Matrix](https://matrix.org/) unified via [Beeper Bridge Manager (bbctl)](https://github.com/beeper/bridge-manager).
* **Identity:** [JMP.chat](https://jmp.chat/) for portable phone identity via XMPP/Matrix.

### Phase 8: SovrIT Habitat (The Local IoT)
**Goal:** A home that works without the internet and respects your privacy.
* **Smart Brain:** [Home Assistant](https://www.home-assistant.io/) (Core VM).
* **Radios:** [Zigbee](https://csa-iot.org/all-solutions/zigbee/) 3.0 / [Z-Wave](https://z-wavealliance.org/) 800-series (Local only).
* **Voice:** [Home Assistant Assist](https://www.home-assistant.io/voice_control/) for local voice processing.

### Phase 9: SovrIT Sentinel (Private Surveillance)
**Goal:** Intelligent monitoring invisible to third parties.
* **NVR:** [Frigate](https://frigate.video/) with [Local AI Object Detection](https://coral.ai/products/accelerator/).
* **Cameras:** Non-cloud PoE Hardware (Firewalled via VLAN).

---

## 🛠️ Maintenance & Lifecycle
1. **The Binder Rule:** Every AI-detected revision change in Phase 5 must be printed and filed in the physical binder.
2. **The Key Protocol:** ZFS Encryption passphrases must never be stored on the same physical node as the data.
3. **The Audit:** Monthly "Insta-Restore" tests to verify S3 backup integrity.
