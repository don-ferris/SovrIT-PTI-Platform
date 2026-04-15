# SovrIT PTI

**SovrIT PTI** (Personal/Private Technology Infrastructure) is a high-performance, local-first infrastructure designed to reclaim digital sovereignty. It replaces the _**entire**_ suite of modern cloud-dependent services - identity, authentication, email/text communication, calendar, contacts, productivity, office/documents, medical/legal/financial records, media, even telephony and location services (and more) - with a unified, encrypted, and self-hosted ecosystem. 

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
### 4. Invisible Security
Security is integrated into the user flow via biometrics (FaceID/TouchID), eliminating the friction of traditional passwords. 
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
* **SovrIT Access:** Centralized identity and biometric gatekeeping ([WebAuthn](https://webauthn.guide/)), OIDC/SAML authentication ([Authentik](https://goauthentik.io/)), and private PKI ([Step-CA](https://smallstep.com/docs/step-ca/)). All traffic is orchestrated via sovereign ingress ([Traefik](https://traefik.io/)) for local SSL termination.
* **SovrIT Fortitude:** Resilience engine providing immutable backups ([Kopia](https://kopia.io/)), automated recovery ([n8n](https://n8n.io/)), and uptime monitoring ([Uptime Kuma](https://github.com/louislam/uptime-kuma)).
* **SovrIT Time:** Internal high-stratum time authority ([chrony](https://chrony-project.org/)) to ensure cryptographic and MFA synchronization during outages.
* **Core Ops:** Provisioning and lifecycle management utilizing NixOS for declarative system state, [Proxmox VE](https://www.proxmox.com/) for virtualization, and [TrueNAS CE](https://www.truenas.com/) for mission-critical data storage.

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
- **SovrIT Notes:** E2EE synchronized note-taking ([Notesnook](https://notesnook.com/)).
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
* **Substrate:** Router/Firewall & WAP
* **Responsibilities:** Physical perimeter and VLAN-based network segmentation.

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
| **End-to-End Notes** | Encrypted note-taking and synchronization via [Notesnook](https://notesnook.com/). |
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

- [**Docker**](https://www.docker.com/) - containerization and modular service deployment
- [**Python**](https://www.python.org/) - scripting, tooling, and automation logic
- [**NetBird**](https://netbird.io/)/[**WireGuard**](https://www.wireguard.com/) - encrypted overlay networking and sovereign VPNs
- [**ZFS**](https://openzfs.org/) - resilient, hardware-agnostic, and encrypted storage foundations
- [**Proxmox**](https://www.proxmox.com/en/products/proxmox-virtual-environment/overview) - enterprise-grade virtualization and orchestration
- [**Authentik**](https://goauthentik.io/) - centralized identity provider and biometric authentication gateway
- [**Ansible**](https://www.ansible.com/) - declarative provisioning and automated infrastructure configuration
- [**n8n**](https://n8n.io/) - low-code workflow automation and service integration
- [**Dokuwiki**](https://www.dokuwiki.org/) - lightweight, database-less documentation for maximum resiliency
- [**WebAuthn**](https://webauthn.guide/) - biometric MFA standard for secure, passwordless access
- [**Traefik**](https://traefik.io/) - cloud-native edge proxy and automated traffic management
- [**Step-CA**](https://smallstep.com/certificates/) - internal certificate authority for private mesh encryption
- [**chrony**](https://chrony-project.org/) - versatile implementation of the Network Time Protocol (NTP) for local synchronization
- [**Kopia**](https://kopia.io/) - fast, secure, and incremental encrypted backups
- [**Forgejo**](https://forgejo.org/) - lightweight self-hosted git service for infrastructure-as-code
- [**Ollama**](https://ollama.com/) - local large language model (LLM) orchestration
- [**Whisper**](https://github.com/SYSTRAN/faster-whisper) - high-fidelity local speech-to-text transcription
- [**Piper**](https://github.com/rhasspy/piper) - fast, local text-to-speech synthesis
- [**Meilisearch**](https://www.meilisearch.com/) - lightning-fast local search engine for all personal data
- [**Home Assistant**](https://www.home-assistant.io/) - the heart of local-only, cloud-independent smart home automation
- [**Frigate**](https://frigate.video/) - AI-powered local NVR and intelligent object detection
- [**Matrix**](https://matrix.org/)/[**Mautrix**](https://mautrix.net/) - decentralized communication hub and bridge architecture
- [**VitalPBX**](https://www.vitalpbx.com/) - sovereign voice-over-IP (VoIP) and telephony
- [**ntfy**](https://ntfy.sh/) - unified, lightweight notification gateway
- [**Stalwart**](https://stalwart.io/) - modern, memory-safe sovereign email server
- [**SnappyMail**](https://snappymail.eu/) - modern, privacy-focused web-based email client
- [**Mailgun**](https://www.mailgun.com/) - high-reputation SMTP relay to prevent outbound mail from being flagged as spam
- [**Pixelfed**](https://pixelfed.org/)/[**GoToSocial**](https://gotosocial.org/) - privacy-focused, federated social networking
- [**FileBrowser Quantum**](https://filebrowser.org/) - web-based file management and remote access
- [**OnlyOffice**](https://www.onlyoffice.com/) - collaborative document editing and office suite
- [**Notesnook**](https://notesnook.com/) - end-to-end encrypted note-taking and sync
- [**Readeck**](https://readeck.org/) - permanent article archiving and visual bookmarking
- [**ArchiveBox**](https://archivebox.io/)/[**Promnesia**](https://github.com/karlicoss/promnesia) - comprehensive web history archiving and exploration
- [**Radicale**](https://radicale.org/) - lightweight CalDAV/CardDAV for calendars and contacts
- [**QuickScan**](https://www.quickscanapp.com/)/[**OpenScan**](https://github.com/OpenScan-App/OpenScan) - mobile document capture with local processing
- [**Actual Budget**](https://actualbudget.org/) - privacy-first personal finance and envelope budgeting
- [**Paperless-ngx**](https://docs.paperless-ngx.com/) - powerful document management and OCR indexing
- [**Tika**](https://tika.apache.org) - extracts metadata and text from over a thousand different file types
- [**libimobiledevice**](https://libimobiledevice.org/) - cross-platform protocol library to communicate with iOS devices natively
- [**adb**](https://developer.android.com/tools/adb) - versatile command-line tool for Android device communication and data extraction
- [**Immich**](https://immich.app/) - high-performance, AI-driven photo and video management
- [**Uptime Kuma**](https://github.com/louislam/uptime-kuma) - self-hosted uptime monitoring and service alerts
- [**NixOS**](https://nixos.org/) - declarative and reproducible operating system configuration
- [**Flame**](https://github.com/pawelmalak/flame) - aesthetic, protected dashboard for all sovereign services
- [**Vaultwarden**](https://github.com/dani-garcia/vaultwarden) - lightweight, self-hosted Bitwarden-compatible secret management
- [**Kavita**](https://www.kavitareader.com/)/[**Audiobookshelf**](https://www.audiobookshelf.org/) - decentralized digital libraries for books and audio
- [**Traccar**](https://www.traccar.org/)/[**MapLibre**](https://maplibre.org/) - private location tracking and sovereign mapping
- [**Jellyfin**](https://jellyfin.org/) - high-performance personal media streaming
- [**Aeterna**](https://alpyxn.github.io/aeterna/)
- [**TubeArchivist**](https://tubearchivist.com/) - sovereign YouTube archiving and metadata management
- [**Hugging Face**](https://huggingface.co/) - LLM/AI frameworks for guided operations, documentation auditing, and household operability
