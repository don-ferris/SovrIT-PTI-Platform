# SovrIT PTI

**SovrIT PTI** (Personal/Private Technology Infrastructure) is a high-performance, local-first infrastructure designed to reclaim digital sovereignty. It replaces the _**entire**_ suite of modern cloud-dependent services—identity, authentication, email/text communication, calendar, contacts, office/documents, medical/legal/financial records, media, even telephony and location services (and more)—with a unified, encrypted, and self-hosted ecosystem. 

SovrIT replaces reliance on ISP, mobile carrier, and third-party cloud services with a modular ecosystem you operate yourself—engineered to be used, understood, and maintained by anyone in your home.

---

## 🌱 Purpose & Mission

Most personal data today lives inside third‑party clouds you do not control. It is routinely inspected, analyzed, monetized, and used by the companies that store it, as well as by government agencies that increasingly disregard the spirit and intent of constitutional privacy protections. SovrIT exists to break that dependency by providing a stable, sovereign foundation for digital life—engineered and maintained with the same safeguards, discipline, and mission‑critical mindset found in enterprise IT environments.

True digital sovereignty requires that your data, your communications, and your daily digital operations be protected end‑to‑end. SovrIT enables you to become your own ISP and mobile carrier, paying traditional providers only for the raw bandwidth required to move encrypted data. Your information should belong to and be visible only to you.

---

## The Seven Architectural Pillars of SovrIT PTI
### 1. Absolute Sovereignty & Zero-Trust Privacy
No third party holds the keys or has access to your data, identity, or mesh network. Where your data passes through servers that are not under your control (e.g. phone calls from a mobile device), they do so in encrypted form.
### 2. Autonomous Functional Resiliency
The system is _self-healing_. Continuous uptime monitoring is tethered to automated recovery workflows that detect service degradation and trigger immediate **atomic rebuilds**. This ensures that the infrastructure maintains its own integrity without requiring manual intervention for routine failures.
### 3. Geo-Distributed High Availability (HA)
SovrIT utilizes a geographically distant Remote (VPS) Failover Node to provide Ultra High Availability. Through a Netbird-based overlay and real-time state synchronization via Syncthing, critical services fail over automatically to the VPS if a home-site outage is detected. The VPS verifies the outage by confirming its own public internet connectivity while home nodes remain unreachable, ensuring continuity even during total local power or ISP failures.
### 4. Invisible & Active Security
Security is integrated into the user flow via biometrics (**WebAuthn**) and self-auditing,  proactive defense by SovrIT Steward - a dedicated security-focused Large Language Model (LLM) that monitors system logs and NetAlertX heartbeats to identify and autonomously remediate complex threats.
### 5. Sovereign Voice/AI Assistance
The SovrIT Assistant serves as the primary gateway to the system's intelligence, serving as  both a voice and chat-based AI assistant. By utilizing local Large Language Models (LLMs) and high-fidelity speech-to-text engines, the assistant processes complex intents, performs multi-step research, and executes system automations entirely within the private network. This sovereign intelligence is natively integrated with the universal search index, allowing the SovrIT Assistant to provide context-aware insights from personal records while remaining 100% private and immune to third-party data collection
### 6. Decoupled Encryption at Rest
All data is secured using hardware-agnostic, filesystem-level encryption (AES-256-GCM). By decoupling encryption keys from physical hardware, the system ensures that data remains mathematically indistinguishable from noise if the servers are physically seized or compromised.
### 7. Operational Continuity - The SovrIT Handbook
Comprehensive "Human-Centric" documentation walks users through procedures consisting of annotated screenshots. "Click the gear icon shown circled in red." An AI agent regularly reviews, autonomously updates, increments the revision number, and alerts the user when a new revision is available to be printed. This ensures the Handbook always matches precisely what the user sees on-screen-layout, menus, and dialog options - ensuring stress-free success and future confidence. This provides non-technical family members with a clear, visual roadmap to maintain and operate the system if the family IT person is unavailable.

---

## 🧩 SovrIT Ecosystem Overview

The SovrIT ecosystem is powered by a high-availability runtime substrate that supports all user-facing modules.

### SovrIT Core (Runtime Substrate)
The foundational layer responsible for the execution environment, security, and resiliency of the platform. It includes:
* **SovrIT SecureNet:** Encrypted P2P mesh networking and private, recursive DNS.
* **SovrIT Steward:** AI-driven SecOps orchestrating active defense and automated remediation.
* **SovrIT Access:** Centralized identity, biometric gatekeeping, and sovereign ingress.
* **SovrIT Fortitude:** The resilience engine managing immutable backups and self-healing.
* **SovrIT AppKernels:** Declarative provisioning and mission-critical encrypted storage management via **Nix flakes and systemd-nspawn** containers means no virtualization overhead and absolute minimal systems on an app/service to app/service basis, resulting in "AppKernels" that a) are as lean/efficient as possible, and b) have the smallest possible attack surface.

To understand how SovrIT stays reliable, imagine you have a high-precision, state-of-the-art mechanical watch that synchronizes its time wirelessly with reference time servers on the Internet. 

Now imagine that anytime the watch has the slightest problem, you can simply push a button so that the watch **explodes** — all the gears and jewels pop out, and then a high-precision robotic arm reassembles it **PERFECTLY** (thereby addressing the problem) and resynchronizes the time with the internet time servers — all in a matter of seconds. 

That is exactly how the SovrIT architecture works:

* **The Blueprint (Nix Flakes):** Instead of manually installing software, we use a "Nix flake." This is a perfect, mathematical blueprint of exactly how a service should look. It contains only the absolute essentials (including supporting elements of the underlying OS) required to make the service functional. 
* **The Containers (systemd-nspawn):** Every service lives in its own high-security container called a "systemd-nspawn" container. It’s like a tiny, isolated vault that keeps each part of the watch from interfering with the others. _Even the Linux kernel is optimized, removing non-essential kernel modules, and core utilities like ssh, ls, echo, sed, and awk - without which a hacker or malicious code is unable to change anything _even if it could somehow manage to get in_.
* **The Rebuild:** If a service breaks, the system doesn't try to "fix" it. It simply deletes the container and instantly re-grows a new one from the Blueprint. Because your data is stored separately, the service wakes up "Factory New" and perfect in seconds.
* **The Data Layer:** 
[Explanation of how the data (that changes as the user makes any sort of changes) are backed up to/restored from Forgejo repos]

---

## ⚙️ Hardware Architecture

SovrIT PTI is designed to be hardware-agnostic, optimized for a high-performance, low-wattage distributed model.

1. **The Network:** Router/Firewall & WAPs providing VLAN-based segmentation.
2. **The Core/Storage Node:** x86-64 server substrate (**NixOS**) managing ZFS pools and Core Modules.
3. **Compute Node (Local LLM):** High-bandwidth hardware (Recommended: Apple Silicon) for real-time AI performance.
4. **Remote (VPS) Failover Node:** Hardened remote failover node for critical service continuity.
5. **Mobile Endpoints:** Biometric-capable trusted nodes for identity and secure remote access.
6. **Off-site Archive:** S3-compatible object storage for immutable, geographical data redundancy.

---

## 🗺️ Functionality Map

| Feature Category | Capabilities & Integrated Services |
| :--- | :--- |
| **Infrastructure & Security** | Mesh networking, Universal SSO (WebAuthn), Private PKI, and AI-driven Active Defense. |
| **Sovereign Intelligence** | Local Private LLM (Ollama), Universal Data Search, and AI-powered NVR (Frigate). |
| **Communication & Social** | Unified Messenger Hub (Matrix), Sovereign Mail/Telephony, and Private Federated Social. |
| **Productivity & Knowledge** | Collaborative Office, Flat-file Markdown Notes, and Permanent Web Archiving. |
| **Vital Archives** | Financial Auditing, OCR-indexed Records, and AI-driven Media/Photo Management. |

---

## 💰 Cost of Sovereignty

You build a Digital Fortress because you value privacy and data integrity, not to find a bargain. While SovrIT can eliminate "subscription creep," it requires initial capital expenditure.
* **Initial Setup:** A 2-node entry-level stack typically ranges from **$600 to $1,000**.
* **Operational OpEx:** Ongoing costs include a remote VPS ($5–$15/mo) and S3-compatible cloud storage ($0.005/GB).
* **Efficiency:** Utilizing used enterprise thin clients and "cracked-screen" laptops can significantly reduce costs while maintaining high-performance compute.

---

## 📜 License & Ethical Usage
The SovrIT PTI blueprint is provided for individual sovereignty. Users assume total responsibility for data security and the legal implications of hosting their own communication and encryption services.

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
- [**systemd-nspawn**](https://www.freedesktop.org/software/systemd/man/latest/systemd-nspawn.html) — high-performance Linux containerization and modular service deployment
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
- [**Nix Flakes**](https://nixos.wiki/wiki/Flakes) — hermetic, reproducible build and configuration management
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
