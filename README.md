# SovrIT PTI 

SovrIT PTI (Personal/Private Technology Infrastructure) is a sovereign, self‑hosted personal IT infrastructure platform  local-first infrastructure designed to reclaim digital sovereignty. It replaces the **entire** suite of modern cloud-dependent services—identity, voice and text communication, productivity, media, and more —with a unified, encrypted, and self-hosted ecosystem. SovrIT replaces reliance on third‑party cloud services with a modular ecosystem you operate yourself — built to be used, understood and maintained by anyone in your home.

This repository defines the SovrIT Platform: the architecture, design philosophy, and long‑term principles that guide the entire SovrIT ecosystem. All SovrIT modules follow the patterns established here.

For a visual overview of the SovrIT architecture, see **[Architecture.md](Architecture.md)**.

---

## 🌱 Purpose

Most personal data today lives inside third‑party clouds you do not control — and is routinely inspected, analyzed, monetized, retained, and used in an attempt to track and manipulate you by the companies that store it, as well as by government agencies that increasingly disregard the spirit and intent of constitutional privacy protections. SovrIT exists to break that dependency by providing a stable, sovereign foundation for identity, authentication, communication, storage, automation, and daily digital routines — engineered and maintained with the same safeguards, discipline, and mission‑critical mindset found in enterprise IT environments.

Self‑hosting isolated services is not enough. True digital sovereignty requires that your data, your communications, and your daily digital operations be protected end‑to‑end. SovrIT establishes patterns for running essential services — authentication and MFA, file and photo storage and sharing, document management and editing, financial, health, and legal records, messaging, media, and more — with enterprise‑grade security, redundancy, and high availability. These services are encrypted, backed up regularly, and routed through personal, self‑hosted VPNs to ensure absolute privacy. The servers that host them are patched, monitored, and incrementally hardened regularly to defend against ransomware, intrusion attempts, and evolving threats.

But SovrIT goes further. It provides the architectural patterns and mechanisms needed to bring basic voice and text communication under your control as well. Mobile devices can operate on data‑only plans, with encrypted phone calls, video calls, messages, and email routed through your own sovereign VPN infrastructure — shielded from carriers, ISPs, and any entity that would log, inspect, monetize, or surveil your communications.

In essence, SovrIT enables you to become your own ISP and your own mobile carrier — while still paying traditional providers only for the raw bandwidth required to move encrypted data. Your information should belong and be visible only to you — not to the companies that move and store it, nor to the government agencies that oversee them.

---

## 🧱 What This (SovrIT Platform) Repo Provides

- The mission, philosophy, and guiding principles of SovrIT  
- Architectural patterns for building sovereign, long‑lived services  
- Naming conventions, repo structure, and documentation standards  
- Expectations for reliability, privacy, and long‑term stewardship  
- Patterns for reducing reliance on third‑party providers  
- Sovereign communication and VPN design principles  
- Human‑centered documentation guidelines for a non‑technical spouse/partner  

SovrIT is not a single application. It is the blueprint for a personal digital infrastructure.

---

## 🧩 SovrIT Ecosystem Overview

### SovrIT Core (runtime substrate)
The sovereign execution environment that all SovrIT modules run on.  
Core includes:

- **SovrIT SecureNet** — encrypted overlay network and sovereign VPN  
- **SovrIT Fortitude** — the resilience engine of SovrIT (backups, disaster recovery, monitoring, self‑healing, hardware redundancy)  
- Provisioning and hardening  
- Encrypted storage foundations  
- LLM‑guided maintenance and household operability  
- Bootstrap, patching, and lifecycle management  

### **SovrIT Modules**

- **SovrIT Access** — authentication, MFA, and account stewardship  
- **SovrIT Vault** — secrets, passwords, and encrypted storage  
- **SovrIT Ledger** — financial records  
- **SovrIT Med** — medical records  
- **SovrIT Legal** — legal and estate records  
- **SovrIT Handbook** — AI/auto-updated system documentation and manuals  
- **SovrIT Notify** — notifications and cross‑system messaging  
- **SovrIT Carrier** — sovereign voice, text, and messaging  

### **Integrations (optional)**

- Home Assistant  
- Media servers  
- Other self‑hosted applications  

---

## 🛡️ SovrIT Brand Pillars

### **Sovereignty by Design**
Your data, your systems, your rules.

### **Enterprise‑Grade Reliability**
Predictable, quiet, and steady.

### **Modular, Composable Architecture**
Each SovrIT module is independent but interoperable.

### **Human‑Centered Clarity**
Documentation (with annotated screenshots) is written for a non-technical spouse/partner to operate confidently.

### **Craftsmanship and Transparency**
Every configuration is intentional, annotated, and inspectable.

### **Longevity and Stewardship**
SovrIT is designed to outlive any single device or trend.

---

## 📐 Architecture Principles

- Small, focused services instead of monoliths  
- Clear boundaries between modules  
- Declarative configuration wherever possible  
- Idempotent provisioning for predictable rebuilds  
- Documented interfaces between components  
- Local‑first design with cloud as an optional extension  
- Self‑hosted VPN and communication layers  
- Preference for open standards and long‑term maintainability  
- Continuous hardening, monitoring, and patching  

---

## 🔒 Sovereign Communication and Connectivity

- **Data‑only mobile plans** routed through a sovereign VPN  
- **Self‑hosted VPN infrastructure** (WireGuard, NetBird, Pangolin‑style)  
- **Encrypted, self‑hosted voice and messaging**  
- **Carrier‑independent communication**  
- **End‑to‑end encrypted routing** for all mobile and household communication  

---

## 📘 Documentation Standards

- Plain language, short paragraphs, and clear steps  
- Liberal use of Visuals and diagrams 
- Glossaries for technical terms  
- Procedures that assume the reader may be stressed or tired  
- A tone that is calm, respectful, and empowering  

---

## 🔭 Roadmap

- Additional architectural diagrams  
- SovrIT glossary and terminology guide  
- Documentation style guide  
- Versioning and lifecycle policies  
- Templates for new SovrIT modules  
- Sovereign mobile workflows  
- Self‑hosted VPN migration paths  
- Expanded hardening and monitoring patterns  

---

## 📜 License

SovrIT is released under the MIT License. See `LICENSE` for details.



---

---

---

# SovrIT PTI: Personal Technology Infrastructure

**SovrIT PTI** is a high-performance,= 

The goal is to build a "Digital Fortress" that is as easy to use as a smartphone, but where every byte of data remains under the physical control of the user.

---

## 🛡️ The Five Pillars of SovrIT

1.  **Digital Sovereignty:** Zero-trust architecture. No third party holds the keys to your data, identity, or mesh network.
2.  **Functional Resiliency:** High availability through local-first design and remote "Ghost Mirroring" for critical services.
3.  **Encrypted Substrate:** All data is protected by filesystem-level encryption (ZFS) and encrypted P2P mesh tunnels.
4.  **Operational Continuity:** Comprehensive "Human-Centric" documentation ensures the system can be maintained and recovered by anyone in the household.
5.  **Invisible Security:** Security is integrated into the user flow via biometrics (FaceID/TouchID), eliminating the friction of traditional passwords.

---

## 🛠️ Functional Requirements Matrix

This matrix specifies the 30 core capabilities of the SovrIT PTI, mapped to their respective self-hosted modules.

| ID | Feature Name | Priority | Requirement Description |
| :--- | :--- | :--- | :--- |
| **FR-01** | **Mesh Networking** | High | Establish an encrypted P2P mesh network ([Netbird](https://netbird.io/)) to facilitate secure node communication without public port exposure. |
| **FR-02** | **Universal Identity** | High | Provide a centralized Identity Provider ([Authentik](https://goauthentik.io/)) for OIDC/SAML authentication across all system modules. |
| **FR-03** | **Biometric Gatekeeper** | High | Mandate WebAuthn (FaceID/TouchID) as the primary MFA via [Authentik](https://goauthentik.io/) to ensure high security with zero daily user friction. |
| **FR-04** | **Edge Traffic Control** | High | Implement an edge proxy ([Traefik](https://traefik.io/)) supporting gRPC and automated SSL management for mesh-wide routing. |
| **FR-05** | **Universal Sovereign Search** | High | Deploy a centralized, lightning-fast indexer ([Meilisearch](https://www.meilisearch.com/)) that provides exhaustive, real-time search across mail, messages, files, notes, and web history. |
| **FR-06** | **Local AI Assistant** | High | Replace cloud assistants with local AI ([Ollama](https://ollama.com/), [Whisper](https://github.com/SYSTRAN/faster-whisper), [Piper](https://github.com/rhasspy/piper)) for voice commands, deep context queries, and hands-free data entry. |
| **FR-07** | **Unified Messenger Hub** | High | Bridge external networks (WhatsApp, Signal, iMessage) into a [Matrix](https://matrix.org/) homeserver using [Mautrix](https://mautrix.net/) bridges to maintain a single local chat history. |
| **FR-08** | **Integrated Virtual Office** | High | Provide a high-speed file explorer ([FileBrowser](https://filebrowser.org/)) with integrated collaborative document, spreadsheet, and presentation editing ([OnlyOffice](https://www.onlyoffice.com/)). |
| **FR-09** | **Sovereign Mail Engine** | High | Host a modern, memory-safe email server ([Stalwart](https://stalwart.io/)) to ensure total ownership of personal and professional correspondence. |
| **FR-10** | **At-Rest Encryption** | High | Secure all user data using filesystem-level encryption ([ZFS](https://openzfs.org/)) with keys decoupled from physical boot media for maximum protection. |
| **FR-11** | **Immutable Backups** | High | Execute hourly encrypted client-side backups ([Kopia](https://kopia.io/)) to offsite S3-compatible storage to ensure data recoverability. |
| **FR-12** | **Remote Failover Mirror** | High | Maintain a minimal "Ghost Mirror" on a remote VPS to ensure access to Identity, Password Vault, and Vital Records during local hardware or internet outages. |
| **FR-13** | **Graceful Power Safety** | High | Integrate UPS monitoring to trigger clean shutdowns of virtual machines and storage pools during sustained power failures. |
| **FR-14** | **Internal Time Server** | High | Host a local NTP server to maintain synchronization for MFA tokens and filesystem timestamps during total internet outages. |
| **FR-15** | **Financial Auditor (Money)** | Medium | Integrate receipt capture ([QuickScan](https://www.quickscanapp.com/)) and OCR ([Paperless-ngx](https://docs.paperless-ngx.com/)) with spending analysis ([Actual Budget](https://actualbudget.org/)), including voice-based transaction logging. |
| **FR-16** | **Vital Records (Med/Legal)** | Medium | Automate the indexing and OCR of medical and legal documents ([Paperless-ngx](https://docs.paperless-ngx.com/)) for instant retrieval via the universal search interface. |
| **FR-17** | **AI Photo Management** | Medium | Host a gallery ([Immich](https://immich.app/)) with ML-driven deduplication and automated purging of low-value media (e.g., screenshots, blurry photos, pocket shots) after a set period. |
| **FR-18** | **End-to-End Notes** | Medium | Provide encrypted note-taking ([Notesnook](https://notesnook.com/)) with local synchronization and automated ingestion into the universal search index. |
| **FR-19** | **Web Memory & History** | Medium | Index and archive every web page visited ([ArchiveBox](https://archivebox.io/), [Promnesia](https://github.com/karlicoss/promnesia)) to create a private, exhaustive, and searchable history of personal research. |
| **FR-20** | **Permanent Bookmarking** | Medium | Provide a "Read-it-Later" service ([Readeck](https://readeck.org/)) that archives web content as searchable PDFs and supports Pinterest-style visual pinning. |
| **FR-21** | **Schedules & People** | Medium | Host synchronized calendars and contact directories via CalDAV/CardDAV ([Radicale](https://radicale.org/)) with native mobile integration. |
| **FR-22** | **The Living Handbook** | Medium | Maintain internal system documentation in a database-less format ([Dokuwiki](https://www.dokuwiki.org/)) to ensure readability during extreme system degradation. |
| **FR-23** | **Private Geolocation** | Medium | Host a private location tracking server ([Traccar](https://www.traccar.org/)) and vector tile server ([MapLibre](https://maplibre.org/)) to provide map services without third-party tracking. |
| **FR-24** | **Smart Home (Habitat)** | Medium | Centrally manage lights, climate, and sensors via a local-only hub ([Home Assistant](https://www.home-assistant.io/)) completely isolated from the public internet. |
| **FR-25** | **AI Handbook Auditor** | Medium | Employ a local agent to audit service UIs and update the Knowledge Base with annotated screenshots for visual and instructional parity. |
| **FR-26** | **Network Segmentation** | Medium | Isolate IoT and automation hardware into dedicated VLANs with zero outbound internet access to prevent lateral network attacks. |
| **FR-27** | **Sovereign Social Feed** | Low | Deploy private social networking and photo sharing ([Pixelfed](https://pixelfed.org/), [GoToSocial](https://gotosocial.org/)) to facilitate communication without metadata harvesting. |
| **FR-28** | **Media & YouTube Hub** | Low | Provide streaming of movies and music ([Jellyfin](https://jellyfin.org/)) with automated local archiving of relevant YouTube content ([TubeArchivist](https://tubearchivist.com/)). |
| **FR-29** | **Digital Library (Books)** | Low | Centralize e-books and audiobooks ([Kavita](https://www.kavitareader.com/), [Audiobookshelf](https://www.audiobookshelf.org/)) into a unified, cross-device accessible library. |
| **FR-30** | **Physical Security (Sentinel)** | Low | Utilize local AI object detection ([Frigate](https://frigate.video/)) for camera feeds to ensure no metadata or video streams are sent to third-party clouds. |

---

## 🏗️ Hardware Architecture: The "Divide & Conquer" Strategy

To ensure a high-performance experience without excessive heat or power consumption, the SovrIT infrastructure is split into two specialized roles:

### 1. The Storage Node (The Heart)
* **Focus:** Reliability, Data Integrity, and Basic Services.
* **Operating System:** Proxmox or TrueNAS Scale.
* **Responsibilities:** ZFS Pool management, Identity (Authentik), Proxy (Traefik), and Lightweight Services.
* **Mirroring:** This node is mirrored to a low-resource VPS (The Ghost Mirror) for emergency failover.

### 2. The Compute Node (The Brain)
* **Focus:** AI Inference, Transcription, and Indexing.
* **Recommended Hardware:** Apple Silicon (Early-gen MacBook or Mac Mini with 16GB+ Unified Memory).
* **Why Apple Silicon?** The Unified Memory Architecture allows Large Language Models (LLMs) and Speech-to-Text engines to stay "hot" in memory, providing instant voice responses and fast file indexing while drawing as little as 30W. 
* **Responsibilities:** Local AI Assistant (Ollama/Whisper), Sovereign Search (Meilisearch), and Messaging Bridges (Mautrix).

---

## 🚀 The User Experience

1.  **Seamless Access:** Netbird maintains a persistent, encrypted tunnel. Whether at home or in a café, your devices are always "inside" the fortress.
2.  **Biometric Gate:** To access any service, you simply glance at your phone. WebAuthn (FaceID) validates your identity via Authentik, granting access to the entire stack.
3.  **Unified Search:** A single search bar allows you to find a WhatsApp message, a scanned medical receipt, or a note from your Knowledge Base in under a second.
4.  **Hands-Free Finance:** Record expenses by voice. The local AI assistant parses your speech and logs the transaction directly into your private ledger.

---

## 📜 License & Ethical Usage
The SovrIT PTI blueprint is provided for individual sovereignty. By deploying this stack, you assume total responsibility for your data security and the legal implications of hosting your own communication and encryption services.
