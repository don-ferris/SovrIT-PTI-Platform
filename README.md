# SovrIT PTI

**SovrIT PTI** (Personal/Private Technology Infrastructure) is a high-performance, local-first infrastructure designed to reclaim digital sovereignty. It replaces the _**entire**_ suite of modern cloud-dependent services—identity, authentication, email/text communication, calendar, contacts, productivity, office/documents, medical/legal/financial records, media, even telephony and location services (and more) - with a unified, encrypted, and self-hosted ecosystem. 

SovrIT replaces reliance on ISP, mobile carrier, and third-party cloud services with a modular ecosystem you operate yourself —engineered to be used, understood, and maintained by anyone in your home.

---

## 🌱 Purpose & Mission

Most personal data today lives inside third‑party clouds you do not control. It is routinely inspected, analyzed, monetized, and used by the companies that store it, as well as by government agencies that increasingly disregard the spirit and intent of constitutional privacy protections. SovrIT exists to break that dependency by providing a stable, sovereign foundation for digital life—engineered and maintained with the same safeguards, discipline, and mission‑critical mindset found in enterprise IT environments.

Self‑hosting isolated services is not enough. True digital sovereignty requires that your data, your communications, and your daily digital operations be protected end‑to‑end. SovrIT enables you to become your own ISP and mobile carrier, paying traditional providers only for the raw bandwidth required to move encrypted data. Your information should belong to and be visible only to you.

---

## 5. The Seven Architectural Pillars of SovrIT PTI
### 1. Absolute Sovereignty & Zero-Trust Privacy
No third party holds the keys or has access to your data, identity, or mesh network. Where your data passes through servers that are not under your control (e.g. phone calls from a mobile device), they do so in encrypted form.
### 2. Autonomous Functional Resiliency
The system is _self-healing_. Continuous uptime monitoring is tethered to automated recovery pipelines that detect service degradation and trigger immediate rebuilds or relaunches. This ensures that the infrastructure maintains its own integrity without requiring manual intervention for routine failures.
### 3. Global High Availability & Failover Redundancy
SovrIT utilizes a geographically distant VPS Ghost Mirror to provide Ultra High Availability. Through automatic failover orchestration, critical services and data remain accessible even during local power outages, ISP failures, or catastrophic physical events like fire or theft.
### 4. Invisible Security
Security is integrated into the user flow via biometrics (FaceID/TouchID), eliminating the friction of traditional passwords. 
### 5. Sovereign Voice/AI Assistance
The SovrIT Assistant serves as the primary gateway to the system's intelligence, serving as  both a voice and chat-based AI assistant. By utilizing local Large Language Models (LLMs) and high-fidelity speech-to-text engines, the assistant processes complex intents, performs multi-step research, and executes system automations entirely within the private network. This sovereign intelligence is natively integrated with the universal search index, allowing the SovrIT Assistant to provide context-aware insights from personal records while remaining 100% private and immune to third-party data collection
### 6. Decoupled Encryption at Rest
All data is secured using hardware-agnostic, filesystem-level encryption (AES-256-GCM). By decoupling encryption keys from physical hardware, the system ensures that data remains mathematically indistinguishable from noise if the servers are physically seized or compromised.
### 7. Operational Continuity - The Living Handbook
Comprehensive "Human-Centric" documentation walks users through procedures consisting of annotated screenshots. "Click the gear icon shown circled in red." An AI agent regularly reviews, autonomously updates, increments the revision number, and alerts the user when a new revision is available to be printed. This ensures the Handbook always matches precisely what the user sees on-screen- layout, menus, and dialog options - ensuring stress-free success and future confidence. This provides non-technical family members with a clear, visual roadmap to maintain and operate the system if the family IT person is unavailable.



---

## 🧩 SovrIT Ecosystem Overview

### SovrIT Core (Runtime Substrate)
The sovereign execution environment and foundational services:
- **SovrIT SecureNet:** Encrypted overlay network and sovereign VPN ([Netbird](https://netbird.io/)).
- **SovrIT Access:** Centralized identity, biometric gatekeeping ([WebAuthn](https://webauthn.guide/)), and OIDC/SAML authentication ([Authentik](https://goauthentik.io/)).
- **SovrIT Fortitude:** Resilience engine providing immutable backups ([Kopia](https://kopia.io/)), automated recovery ([n8n](https://n8n.io/)), and uptime monitoring ([Uptime Kuma](https://github.com/louislam/uptime-kuma)).
- **Core Ops:** Provisioning and lifecycle management ([Ansible](https://www.ansible.com/)), declarative configuration ([NixOS](https://nixos.org/)), private state tracking ([Forgejo](https://forgejo.org/)), and encrypted storage foundations ([ZFS](https://openzfs.org/)).

### SovrIT Modules
The user-facing applications that fulfill the functional requirements:

* **Intelligence & Discovery:**
    * **SovrIT Assistant:** Local voice/chat AI ([Ollama](https://ollama.com/)), transcription ([Whisper](https://github.com/SYSTRAN/faster-whisper)), and speech synthesis ([Piper](https://github.com/rhasspy/piper)).
    * **SovrIT Search:** Lightning-fast universal discovery across all system data ([Meilisearch](https://www.meilisearch.com/)).
    * **SovrIT Sentinel:** Intelligent local security and AI NVR ([Frigate](https://frigate.video/)).
* **Communication & Social:**
    * **SovrIT Messenger:** Unified chat hub (WhatsApp/Signal/iMessage) via ([Matrix](https://matrix.org/)) and ([Mautrix](https://mautrix.net/)) bridges.
    * **SovrIT Carrier:** Sovereign voice and telephony ([VitalPBX](https://www.vitalpbx.com/)) using SIP-TLS and SRTP for encrypted signaling and media.
    * **SovrIT Notify:** Unified cross-system notification gateway ([ntfy](https://ntfy.sh/)).
    * **SovrIT Social:** Private photo sharing and social networking ([Pixelfed](https://pixelfed.org/)) / ([GoToSocial](https://gotosocial.org/)).
* **Productivity & Office:**
    * **SovrIT Office:** File management ([FileBrowser Quantum](https://filebrowser.org/)) and collaborative editing ([OnlyOffice](https://www.onlyoffice.com/)).
    * **SovrIT Notes:** E2EE synchronized note-taking ([Notesnook](https://notesnook.com/)).
    * **SovrIT Calendar / Contacts:** Sovereign schedules and people ([Radicale](https://radicale.org/)).
    * **SovrIT Bookmarks:** Permanent article archiving and visual pinning ([Readeck](https://readeck.org/)).
    * **SovrIT History:** Searchable web memory ([ArchiveBox](https://archivebox.io/)) / ([Promnesia](https://github.com/karlicoss/promnesia)).
* **Vital Archives:**
    * **SovrIT Money:** Financial auditing ([Actual Budget](https://actualbudget.org/)) with mobile receipt capture ([QuickScan](https://www.quickscanapp.com/)) / ([OpenScan](https://github.com/OpenScan-App/OpenScan)) and document OCR ([Paperless-ngx](https://docs.paperless-ngx.com/)).
    * **SovrIT Photos:** AI gallery and media management with ML-driven pruning ([Immich](https://immich.app/)).
    * **SovrIT Med / Legal:** OCR-indexed health and estate records ([Paperless-ngx](https://docs.paperless-ngx.com/)).
    * **SovrIT Handbook:** AI-audited documentation and manuals ([Dokuwiki](https://www.dokuwiki.org/)).
    * **SovrIT Maps:** Private location services ([Traccar](https://www.traccar.org/)) and private vector mapping ([MapLibre](https://maplibre.org/)).
* **Identity & Vault:**
    * **SovrIT Vault:** Secrets, passwords, and MFA recovery stewardship ([Vaultwarden](https://github.com/dani-garcia/vaultwarden)).
* **Media & Lifestyle:**
    * **SovrIT Media:** Streaming and YouTube archiving ([Jellyfin](https://jellyfin.org/))/([TubeArchivist](https://tubearchivist.com/)).
    * **SovrIT Books:** Digital and audiobook library ([Kavita](https://www.kavitareader.com/))/([Audiobookshelf](https://www.audiobookshelf.org/)).
    * **SovrIT Habitat:** Local-only smart home automation ([Home Assistant](https://www.home-assistant.io/)).

---

## 🏗️ Hardware Architecture: "Divide & Conquer"

### 1. The Storage Node (The Heart)
* **Substrate:** Proxmox or TrueNAS Scale.
* **Responsibilities:** [ZFS] Pool management, Identity ([Authentik]), Proxy ([Traefik]), and Core Modules.
* **Mirroring:** Mirrored to a low-resource VPS (The Ghost Mirror) for emergency failover.

### 2. The Compute Node (The Brain)
* **Recommended Hardware:** Apple Silicon (Early-gen MacBook or Mac Mini with M1 or M2 Pro or Max CPU and 16GB+ Unified Memory).
* **Benefit:** Unified Memory Architecture allows LLMs and Speech-to-Text engines to stay "hot" in memory, providing instant responses while drawing as little as 30W.

---

## 🧩 SovrIT PTI: Functionality Map

### 🛡️ Core Infrastructure & Security
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Mesh Networking** | Encrypted P2P overlay network via ([Netbird](https://netbird.io/)) for secure inter-node communication. |
| **Universal Identity** | Centralized OIDC/SAML authentication and account brokering via ([Authentik](https://goauthentik.io/)). |
| **Biometric Gatekeeper** | Zero-friction MFA utilizing ([WebAuthn](https://webauthn.guide/)) (Face ID/TouchID) for all system access. |
| **Edge Traffic Control** | High-performance routing and automated SSL management via ([Traefik](https://traefik.io/)). |
| **At-Rest Encryption** | Hardware-agnostic filesystem encryption using ([ZFS](https://openzfs.org/)) with decoupled master keys. |
| **Secure Remote Access** | Mesh-only administrative management of server substrates via ([Netbird](https://netbird.io/)). |
| **Local Certificate Authority** | Trusted internal SSL certificate issuance for mesh-only domains via ([Step-CA](https://smallstep.com/certificates/)). |
| **Internal Time Server** | Local high-stratum NTP server for MFA and ([ZFS](https://openzfs.org/)) synchronization during outages. |
| **Network Segmentation** | Isolation of IoT hardware into dedicated VLANs with zero outbound access. |
| **Air-Gapped IoT Radio** | Local-only sensor communication via physical Zigbee/Z-Wave protocols. |
| **MFA Recovery Vault** | Physical "Break-Glass" recovery procedure using paper-stored codes. |
| **Encryption Key Rotation** | Procedure for rotating ([ZFS](https://openzfs.org/)) master keys and identity signing keys. |
| **Mobile Device Hardening** | Routing of all mobile traffic through the mesh with "Always-On" VPN logic. |
| **Physical Asset Tracking** | Encrypted inventory of all physical hardware within the ([Dokuwiki](https://www.dokuwiki.org/)) Handbook. |

### 🔄 Resilience & Maintenance
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Insta-Restore Engine** | Automated rebuild pipelines for core services using ([n8n](https://n8n.io/)) and ([Ansible](https://www.ansible.com/)). |
| **Immutable Backups** | Hourly, encrypted client-side backups to offsite storage via ([Kopia](https://kopia.io/)). |
| **Remote Failover Mirror** | High-availability "Ghost Mirror" on a remote VPS for Identity and Vault access. |
| **Graceful Power Safety** | Automated UPS-triggered shutdown sequences for storage and compute nodes. |
| **Versioned Infrastructure** | State reproducibility using configurations stored in a private ([Forgejo](https://forgejo.org/)) instance. |
| **The Living Handbook** | Database-less, human-centric documentation maintained in ([Dokuwiki](https://www.dokuwiki.org/)). |
| **Database Atomic Snapshots** | Coordinated filesystem snapshots for consistent point-in-time recovery. |
| **Digital Dead-Man Switch** | Automated information handover to beneficiaries if heartbeat is not detected. |
| **Automated Health Reports** | Weekly reporting on disk wear, backup integrity, and authentication attempts. |
| **Log Aggregation** | Centralized, encrypted log management for auditing and troubleshooting. |
| **Snapshot Pruning Logic** | Automated thinning of ([ZFS](https://openzfs.org/)) snapshots to optimize space. |
| **Gateway Dashboard** | Unified web interface for all services using ([Flame](https://github.com/pawelmalak/flame)). |
| **Resource Quotas** | Strict CPU/RAM limits to ensure Identity and Resilience responsiveness. |
| **Zero-Log App Config** | Disabling of identifiable debug logs to disk in favor of central aggregation. |
| **Bandwidth QoS** | Prioritization of mesh-failover and telephony traffic over media sync. |
| **Hardware Wear Monitoring** | S.M.A.R.T. data monitoring to trigger alerts when drive life is critical. |

### 🧠 Sovereign Intelligence
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Local AI Assistant** | Private voice and chat intelligence using ([Ollama](https://ollama.com/)), ([Whisper](https://github.com/SYSTRAN/faster-whisper)), and ([Piper](https://github.com/rhasspy/piper)). |
| **Universal Sovereign Search** | Exhaustive, real-time discovery across all system data via ([Meilisearch](https://www.meilisearch.com/)). |
| **AI Handbook Auditor** | Automated agent that audits UIs to keep documentation screenshots in parity. |
| **Local AI NVR** | Hardware-accelerated object detection for feeds via ([Frigate](https://frigate.video/)). |

### 📞 Communication & Social
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Unified Messenger Hub** | Centralized chat bridging WhatsApp, Signal, and iMessage into ([Matrix](https://matrix.org/)). |
| **Encrypted Telephony** | Private voice communication via ([VitalPBX](https://www.vitalpbx.com/)) using SIP-TLS and SRTP. |
| **SovrIT Notify** | Unified cross-system notification gateway powered by ([ntfy](https://ntfy.sh/)). |
| **Sovereign Mail Engine** | Modern, high-performance email hosting and ownership via ([Stalwart](https://stalwart.io/)). |
| **Sovereign Social Feed** | Privacy-focused social networking via ([Pixelfed](https://pixelfed.org/)) and ([GoToSocial](https://gotosocial.org/)). |

### 📂 Productivity & The Virtual Office
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Integrated Virtual Office** | File management via ([FileBrowser Quantum](https://filebrowser.org/)) and editing via ([OnlyOffice](https://www.onlyoffice.com/)). |
| **End-to-End Notes** | Encrypted note-taking and synchronization via ([Notesnook](https://notesnook.com/)). |
| **Permanent Bookmarking** | Article archiving as searchable PDFs via ([Readeck](https://readeck.org/)). |
| **Web Memory & History** | Comprehensive web archiving via ([ArchiveBox](https://archivebox.io/)) and ([Promnesia](https://github.com/karlicoss/promnesia)). |
| **Schedules & People** | Sovereign calendar and contact synchronization via ([Radicale](https://radicale.org/)). |
| **Encrypted Temp-Sharing** | Mechanism for sharing large files via auto-expiring, protected links. |
| **P2P Asset Sync** | Direct, encrypted synchronization between mobile devices and the home node. |

### 🗄️ Vital Archives & Records
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Financial Auditor** | Receipt capture via ([QuickScan](https://www.quickscanapp.com/)) and spend analysis via ([Actual Budget](https://actualbudget.org/)). |
| **Vital Records** | OCR-indexed medical and legal archives utilizing ([Paperless-ngx](https://docs.paperless-ngx.com/)) / ([Tika](https://tika.apache.org/)). |
| **AI Photo Management** | High-performance gallery with ML deduplication via ([Immich](https://immich.app/)). |
| **Digital Library** | Hosting for e-books and audiobooks via ([Kavita](https://www.kavitareader.com/)) and ([Audiobookshelf](https://www.audiobookshelf.org/)). |
| **Private Geolocation** | Location tracking via ([Traccar](https://www.traccar.org/)) with private mapping via ([MapLibre](https://maplibre.org/)). |
| **OCR Record Archive** | Automated full-text indexing of all uploaded PDFs for instant retrieval. |
| **Media & YouTube Hub** | Streaming via ([Jellyfin](https://jellyfin.org/)) and local YouTube archiving via ([TubeArchivist](https://tubearchivist.com/)). |

---

## 📜 License & Ethical Usage
The SovrIT PTI blueprint is provided for individual sovereignty. By deploying this stack, you assume total responsibility for your data security and the legal implications of hosting your own communication and encryption services.

## 🙏 Acknowledgements
SovrIT stands firmly on the shoulders of giants. It would not exist without the incredible work of the open‑source communities whose tools and ideas form its foundation.

- [**Docker**] — containerization and modular service deployment
- [**Python**] — scripting, tooling, and automation logic
- [**NetBird**] / [**WireGuard**] — encrypted overlay networking and sovereign VPNs
- [**ZFS**] — resilient, hardware-agnostic, and encrypted storage foundations
- [**Proxmox**] — enterprise-grade virtualization and orchestration
- [**Authentik**] — centralized identity provider and biometric authentication gateway
- [**Ansible**] — declarative provisioning and automated infrastructure configuration
- [**n8n**] — low-code workflow automation and service integration
- [**Dokuwiki**] — lightweight, database-less documentation for maximum resiliency
- [**WebAuthn**] — biometric MFA standard for secure, passwordless access
- [**Traefik**] — cloud-native edge proxy and automated traffic management
- [**Step-CA**] — internal certificate authority for private mesh encryption
- [**Kopia**] — fast, secure, and incremental encrypted backups
- [**Forgejo**] — lightweight self-hosted git service for infrastructure-as-code
- [**Ollama**] — local large language model (LLM) orchestration
- [**Whisper**] — high-fidelity local speech-to-text transcription
- [**Piper**] — fast, local text-to-speech synthesis
- [**Meilisearch**] — lightning-fast local search engine for all personal data
- [**Home Assistant**] — the heart of local-only, cloud-independent smart home automation
- [**Frigate**] — AI-powered local NVR and intelligent object detection
- [**Matrix**] / [**Mautrix**] — decentralized communication hub and bridge architecture
- [**VitalPBX**] — sovereign voice-over-IP (VoIP) and telephony
- [**ntfy**] — unified, lightweight notification gateway
- [**Stalwart**] — modern, memory-safe sovereign email server
- [**Pixelfed**] / [**GoToSocial**] — privacy-focused, federated social networking
- [**FileBrowser Quantum**] — web-based file management and remote access
- [**OnlyOffice**] — collaborative document editing and office suite
- [**Notesnook**] — end-to-end encrypted note-taking and sync
- [**Readeck**] — permanent article archiving and visual bookmarking
- [**ArchiveBox**] / [**Promnesia**] — comprehensive web history archiving and exploration
- [**Radicale**] — lightweight CalDAV/CardDAV for calendars and contacts
- [**QuickScan**] / [**OpenScan**] — mobile document capture with local processing
- [**Actual Budget**] — privacy-first personal finance and envelope budgeting
- [**Paperless-ngx**] — powerful document management and OCR indexing
- [**Immich**] — high-performance, AI-driven photo and video management
- [**Tika**](https://tika.apache.org) — extracts metadata and text from over a thousand different file types
- [**Uptime Kuma**] — self-hosted uptime monitoring and service alerts
- [**NixOS**] — declarative and reproducible operating system configuration- [**Flame**] — aesthetic, protected dashboard for all sovereign services
- [**Kavita**] / [**Audiobookshelf**] — decentralized digital libraries for books and audio
- [**Traccar**] / [**MapLibre**] — private location tracking and sovereign mapping
- [**Jellyfin**] — high-performance personal media streaming
- [**TubeArchivist**] — sovereign YouTube archiving and metadata management
- [**Hugging Face**] — LLM/AI frameworks for guided operations and documentation auditing
