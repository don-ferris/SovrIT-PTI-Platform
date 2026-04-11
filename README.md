# SovrIT PTI

**SovrIT PTI** (Personal/Private Technology Infrastructure) is a high-performance, local-first infrastructure designed to reclaim digital sovereignty. It replaces the _**entire**_ suite of modern cloud-dependent services—identity, authentication, email/text communication, productivity, office/documents, medical/legal/financial records, media, even telephony and location services (and more) - with a unified, encrypted, and self-hosted ecosystem. 

SovrIT replaces reliance on ISP, mobile carrier, and third-party cloud services with a modular ecosystem you operate yourself —engineered to be used, understood, and maintained by anyone in your home.

---

## 🌱 Purpose & Mission

Most personal data today lives inside third‑party clouds you do not control. It is routinely inspected, analyzed, monetized, and used by the companies that store it, as well as by government agencies that increasingly disregard the spirit and intent of constitutional privacy protections. SovrIT exists to break that dependency by providing a stable, sovereign foundation for digital life—engineered and maintained with the same safeguards, discipline, and mission‑critical mindset found in enterprise IT environments.

Self‑hosting isolated services is not enough. True digital sovereignty requires that your data, your communications, and your daily digital operations be protected end‑to‑end. SovrIT enables you to become your own ISP and mobile carrier, paying traditional providers only for the raw bandwidth required to move encrypted data. Your information should belong to and be visible only to you.

---

## 🛡️ The Seven Architectural Pillars

### 1. Absolute Sovereignty & Zero-Trust Privacy
No third party holds the keys to your data, identity, or mesh network. All data passing through external carriers is strictly encrypted.
### 2. Autonomous Functional Resiliency
The system is *self-healing*. Automated recovery pipelines detect service degradation and trigger immediate rebuilds to ensure integrity without manual intervention.
### 3. Global High Availability & Failover Redundancy
A geographically distant VPS "Ghost Mirror" provides failover orchestration, ensuring critical data remains accessible during local outages or catastrophic physical events.
### 4. Invisible Security
Security is integrated into the user flow via biometrics (FaceID/TouchID), eliminating the friction of traditional passwords.
### 5. Sovereign Voice/AI Assistance
The **SovrIT Assistant** serves as the primary gateway to the system's intelligence, providing both voice and chat-based local AI. By utilizing local LLMs and speech-to-text engines, it processes complex intents and research entirely within the private network, integrated with a universal search index for context-aware insights.
### 6. Decoupled Encryption at Rest
All data is secured using hardware-agnostic, filesystem-level encryption (AES-256-GCM). Encryption keys are decoupled from physical hardware to ensure data remains unreadable if servers are physically seized.
### 7. **Operational Continuity (The Living Handbook)
Comprehensive "Human-Centric" documentation ensures the system can be maintained by anyone in the household. AI-audited instructions match real-time UIs to provide non-technical users with a clear visual roadmap.

---

## 🧩 SovrIT Ecosystem Overview

### SovrIT Core (Runtime Substrate)
- **SovrIT SecureNet:** Encrypted overlay network and sovereign VPN [Netbird].
- **SovrIT Fortitude:** Resilience engine (backups, disaster recovery, monitoring, self-healing).
- **Core Ops:** Provisioning, hardening, encrypted [ZFS] storage foundations, and lifecycle management.

### SovrIT Modules
* **Intelligence & Discovery:**
    * **SovrIT Assistant:** Local voice and chat-based AI [Ollama]/[Whisper].
    * **SovrIT Search:** Lightning-fast universal discovery [Meilisearch].
    * **SovrIT Sentinel:** Intelligent local security and AI NVR [Frigate].
* **Communication & Social:**
    * **SovrIT Messenger:** Unified chat hub (WhatsApp/Signal/iMessage) via [Matrix].
    * **SovrIT Carrier:** Sovereign voice and telephony [VitalPBX].
    * **SovrIT Notify:** Unified notification gateway [ntfy].
    * **SovrIT Social:** Private photo sharing and social networking [Pixelfed] / [GoToSocial].
* **Productivity & Office:**
    * **SovrIT Office:** File management [FileBrowser Quantum] and collaborative editing [OnlyOffice].
    * **SovrIT Notes:** E2EE synchronized note-taking [Notesnook].
    * **SovrIT Calendar / Contacts:** Sovereign schedules and people [Radicale].
    * **SovrIT Bookmarks:** Permanent article archiving [Readeck].
    * **SovrIT History:** Searchable web memory [ArchiveBox]/[Promnesia].
* **Vital Archives:**
    * **SovrIT Money:** Financial auditor and receipt capture [Actual Budget].
    * **SovrIT Photos:** AI gallery and media management [Immich].
    * **SovrIT Med / Legal:** OCR-indexed health and estate records [Paperless-ngx].
    * **SovrIT Handbook:** AI-audited documentation [Dokuwiki].
    * **SovrIT Maps:** Private location services [Traccar]/[MapLibre].
* **Identity & Vault:**
    * **SovrIT Access:** Authentication and biometric gatekeeper [Authentik].
    * **SovrIT Vault:** Secrets and password stewardship [Vaultwarden].
* **Media & Lifestyle:**
    * **SovrIT Media:** Streaming and YouTube archiving [Jellyfin]/[TubeArchivist].
    * **SovrIT Books:** Digital and audiobook library [Kavita]/[Audiobookshelf].
    * **SovrIT Habitat:** Local-only smart home automation [Home Assistant].

---

## 🏗️ Hardware Architecture: The "Divide & Conquer" Strategy

### 1. The Storage Node (The Heart)
* **Substrate:** Proxmox or TrueNAS Scale.
* **Responsibilities:** [ZFS] Pool management, Identity [Authentik], Proxy [Traefik], and Core Modules.
* **Mirroring:** Mirrored to a low-resource VPS (The Ghost Mirror) for emergency failover.

### 2. The Compute Node (The Brain)
* **Recommended Hardware:** Apple Silicon (Early-gen MacBook or Mac Mini with 16GB+ Unified Memory).
* **Benefit:** Unified Memory Architecture allows LLMs and Speech-to-Text engines to stay "hot" in memory, providing instant responses while drawing as little as 30W.

---

## 🧩 SovrIT PTI: Functionality Map

### 🛡️ Core Infrastructure & Security
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Mesh Networking** | Encrypted P2P overlay network via [Netbird] for secure inter-node communication. |
| **Universal Identity** | Centralized OIDC/SAML authentication and account brokering via [Authentik]. |
| **Biometric Gatekeeper** | Zero-friction MFA utilizing [WebAuthn] for all system access. |
| **Edge Traffic Control** | High-performance routing and automated SSL management via [Traefik]. |
| **At-Rest Encryption** | Hardware-agnostic filesystem encryption using [ZFS] with decoupled master keys. |
| **Secure Remote Access** | Mesh-only administrative management of server substrates via [Netbird]. |
| **Local Certificate Authority** | Trusted internal SSL certificate issuance for mesh-only domains via [Step-CA]. |
| **Internal Time Server** | Local high-stratum NTP server for MFA and [ZFS] synchronization during outages. |
| **Network Segmentation** | Isolation of IoT hardware into dedicated VLANs with zero outbound access. |
| **Air-Gapped IoT Radio** | Local-only sensor communication via physical Zigbee/Z-Wave protocols. |
| **MFA Recovery Vault** | Physical "Break-Glass" recovery procedure using paper-stored codes. |
| **Encryption Key Rotation** | Procedure for rotating [ZFS] master keys and identity signing keys. |
| **Mobile Device Hardening** | Routing of all mobile traffic through the mesh with "Always-On" VPN logic. |
| **Physical Asset Tracking** | Encrypted inventory of all physical hardware within the [Dokuwiki] Handbook. |

### 🔄 Resilience & Maintenance
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Insta-Restore Engine** | Automated rebuild pipelines for core services using [n8n] and [Ansible]. |
| **Immutable Backups** | Hourly, encrypted client-side backups to offsite storage via [Kopia]. |
| **Remote Failover Mirror** | High-availability "Ghost Mirror" on a remote VPS for Identity and Vault access. |
| **Graceful Power Safety** | Automated UPS-triggered shutdown sequences for storage and compute nodes. |
| **Versioned Infrastructure** | State reproducibility using configurations stored in a private [Forgejo] instance. |
| **The Living Handbook** | Database-less, human-centric documentation maintained in [Dokuwiki]. |
| **Database Atomic Snapshots** | Coordinated filesystem snapshots for consistent point-in-time recovery. |
| **Digital Dead-Man Switch** | Automated information handover to beneficiaries if heartbeat is not detected. |
| **Automated Health Reports** | Weekly reporting on disk wear, backup integrity, and authentication attempts. |
| **Log Aggregation** | Centralized, encrypted log management for auditing and troubleshooting. |
| **Snapshot Pruning Logic** | Automated thinning of [ZFS] snapshots to optimize space. |
| **Gateway Dashboard** | Unified web interface for all services using [Flame]. |
| **Resource Quotas** | Strict CPU/RAM limits to ensure Identity and Resilience responsiveness. |
| **Zero-Log App Config** | Disabling of identifiable debug logs to disk in favor of central aggregation. |
| **Bandwidth QoS** | Prioritization of mesh-failover and telephony traffic over media sync. |
| **Hardware Wear Monitoring** | S.M.A.R.T. data monitoring to trigger alerts when drive life is critical. |

### 🧠 Sovereign Intelligence
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Local AI Assistant** | Private voice and chat intelligence using [Ollama], [Whisper], and [Piper]. |
| **Universal Sovereign Search** | Exhaustive, real-time discovery across all system data via [Meilisearch]. |
| **AI Handbook Auditor** | Automated agent that audits UIs to keep documentation screenshots in parity. |
| **Local AI NVR** | Hardware-accelerated object detection for feeds via [Frigate]. |

### 📞 Communication & Social
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Unified Messenger Hub** | Centralized chat bridging WhatsApp, Signal, and iMessage into [Matrix]. |
| **Encrypted Telephony** | Private voice communication via [VitalPBX] using SIP-TLS and SRTP. |
| **SovrIT Notify** | Unified cross-system notification gateway powered by [ntfy]. |
| **Sovereign Mail Engine** | Modern, high-performance email hosting and ownership via [Stalwart]. |
| **Sovereign Social Feed** | Privacy-focused social networking via [Pixelfed] and [GoToSocial]. |

### 📂 Productivity & The Virtual Office
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Integrated Virtual Office** | File management via [FileBrowser Quantum] and editing via [OnlyOffice]. |
| **End-to-End Notes** | Encrypted note-taking and synchronization via [Notesnook]. |
| **Permanent Bookmarking** | Article archiving as searchable PDFs via [Readeck]. |
| **Web Memory & History** | Comprehensive web archiving via [ArchiveBox] and [Promnesia]. |
| **Schedules & People** | Sovereign calendar and contact synchronization via [Radicale]. |
| **Encrypted Temp-Sharing** | Mechanism for sharing large files via auto-expiring, protected links. |
| **P2P Asset Sync** | Direct, encrypted synchronization between mobile devices and the home node. |

### 🗄️ Vital Archives & Records
| Feature Name | Functionality & Integrated Services |
| :--- | :--- |
| **Financial Auditor** | Receipt capture via [QuickScan] and spend analysis via [Actual Budget]. |
| **Vital Records** | OCR-indexed medical and legal archives utilizing [Paperless-ngx]. |
| **AI Photo Management** | High-performance gallery with ML deduplication via [Immich]. |
| **Digital Library** | Hosting for e-books and audiobooks via [Kavita] and [Audiobookshelf]. |
| **Private Geolocation** | Location tracking via [Traccar] with private mapping via [MapLibre]. |
| **OCR Record Archive** | Automated full-text indexing of all uploaded PDFs for instant retrieval. |
| **Media & YouTube Hub** | Streaming via [Jellyfin] and local YouTube archiving via [TubeArchivist]. |

---

## 📜 License & Ethical Usage
The SovrIT PTI blueprint is provided for individual sovereignty. By deploying this stack, you assume total responsibility for your data security and the legal implications of hosting your own communication and encryption services.

[Netbird]: https://netbird.io/
[Authentik]: https://goauthentik.io/
[WebAuthn]: https://webauthn.guide/
[Traefik]: https://traefik.io/
[ZFS]: https://openzfs.org/
[Step-CA]: https://smallstep.com/certificates/
[n8n]: https://n8n.io/
[Ansible]: https://www.ansible.com/
[Kopia]: https://kopia.io/
[Forgejo]: https://forgejo.org/
[Dokuwiki]: https://www.dokuwiki.org/
[Flame]: https://github.com/pawelmalak/flame
[Ollama]: https://ollama.com/
[Whisper]: https://github.com/SYSTRAN/faster-whisper
[Piper]: https://github.com/rhasspy/piper
[Meilisearch]: https://www.meilisearch.com/
[Frigate]: https://frigate.video/
[Matrix]: https://matrix.org/
[VitalPBX]: https://www.vitalpbx.com/
[ntfy]: https://ntfy.sh/
[Stalwart]: https://stalwart.io/
[Pixelfed]: https://pixelfed.org/
[GoToSocial]: https://gotosocial.org/
[FileBrowser Quantum]: https://filebrowser.org/
[OnlyOffice]: https://www.onlyoffice.com/
[Notesnook]: https://notesnook.com/
[Readeck]: https://readeck.org/
[ArchiveBox]: https://archivebox.io/
[Promnesia]: https://github.com/karlicoss/promnesia
[Radicale]: https://radicale.org/
[QuickScan]: https://www.quickscanapp.com/
[Actual Budget]: https://actualbudget.org/
[Paperless-ngx]: https://docs.paperless-ngx.com/
[Immich]: https://immich.app/
[Kavita]: https://www.kavitareader.com/
[Audiobookshelf]: https://www.audiobookshelf.org/
[Traccar]: https://www.traccar.org/
[MapLibre]: https://maplibre.org/
[Jellyfin]: https://jellyfin.org/
[TubeArchivist]: https://tubearchivist.com/
[Home Assistant]: https://www.home-assistant.io/
