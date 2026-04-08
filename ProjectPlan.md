This updated **ProjectPlan.md** now serves as your master blueprint, incorporating the five core pillars of the **SovrIT PTI** architecture exactly as defined.
```markdown
# ProjectPlan.md: SovrIT PTI (Personal/Private Technology Infrastructure)

## 🏛️ The Five Architectural Pillars
The SovrIT PTI is a permanent, sovereign extension of the user's life, built upon five non-negotiable architectural requirements:

1. **Absolute Sovereignty & Zero-Trust Privacy**: The infrastructure is architected to ensure total data ownership. By eliminating third-party intermediaries and cloud dependencies, the user maintains 100% control over their digital footprint. In a **Zero-Trust** environment, privacy isn't a policy—it’s a technical certainty.
2. **The Fortress Protocol (Decoupled Encryption at Rest)**: All data is secured using hardware-agnostic, filesystem-level encryption (**AES-256-GCM**). By decoupling encryption keys from physical hardware, the system ensures that data remains mathematically indistinguishable from noise if the servers are physically seized or compromised.
3. **Autonomous Functional Resiliency**: The system is **self-healing**. Continuous uptime monitoring is tethered to automated recovery pipelines that detect service degradation and trigger immediate rebuilds or relaunches. This ensures that the infrastructure maintains its own integrity without requiring manual intervention for routine failures.
4. **Global High Availability & Failover Redundancy**: SovrIT utilizes a geographically distant **VPS Ghost Mirror** to provide **Ultra High Availability**. Through automatic failover orchestration, critical services and data remain accessible even during local power outages, ISP failures, or catastrophic physical events like fire or theft. Your digital life exists everywhere, even when your home node is nowhere.
5. **Human-Centric Interface Continuity (The Living Handbook)**: The system bridges the gap between complex code and family operability. An **AI-audited Handbook** uses annotated screenshots and real-time UI tracking to ensure that the documentation exactly matches the current state of the software. This provides non-technical family members with a clear, visual roadmap to maintain and operate the system if the lead architect is unavailable.

---

## 🗺️ The 10-Phase Roadmap

### Phase 0: The Substrate (Infrastructure Bootstrap)
**Goal:** Establish the encrypted mesh and physical data protection.
* **Home OS:** [Proxmox VE](https://www.proxmox.com/) (Hypervisor for HA clustering).
* **VPS OS:** [NixOS](https://nixos.org/) (Immutable, reproducible, with native [ZFS Support](https://nixos.wiki/wiki/ZFS)).
* **SecureNet:** [Netbird](https://netbird.io/) P2P mesh overlay; all public ports closed via UFW.
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
* **Vault:** [Vaultwarden](https://github.com/dani-garcia/vaultwarden) (Private Bitwarden API).
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
* **Offsite Vault:** [Kopia](https://kopia.io/) encrypted backups to [Cloudflare R2](https://www.cloudflare.com/developer-platform/r2/).
* **Restore Logic:** [n8n](https://n8n.io/) + Ansible for "couple-click" service rebuilding.
* **Watchman:** [Uptime Kuma](https://uptime.kuma.pet/) for health monitoring and failover triggers.

### Phase 7: Sovereign Carrier (Communication)
**Goal:** Own your phone number and unify your messaging.
* **Voice PBX:** [VitalPBX](https://www.vitalpbx.com/) with SIP-TLS/SRTP encryption.
* **Messaging:** [Matrix](https://matrix.org/) unified via [Beeper Bridge Manager (bbctl)](https://github.com/beeper/bridge-manager).
* **Identity:** [JMP.chat](https://jmp.chat/) for portable phone identity via XMPP/Matrix.

### Phase 8: SovrIT Habitat (The Local IoT)
**Goal:** A home that works without the internet and respects privacy.
* **Smart Brain:** [Home Assistant](https://www.home-assistant.io/) (Core VM).
* **Radios:** [Zigbee](https://csa-iot.org/all-solutions/zigbee/) 3.0 / [Z-Wave](https://z-wavealliance.org/) 800-series (Local only).
* **Voice:** [Home Assistant Assist](https://www.home-assistant.io/voice_control/) for local voice processing.

### Phase 9: SovrIT Sentinel (Private Surveillance)
**Goal:** Intelligent monitoring invisible to third parties.
* **NVR:** [Frigate](https://frigate.video/) with [Local AI Object Detection](https://coral.ai/products/accelerator/).
* **Cameras:** Non-cloud PoE Hardware (Firewalled via VLAN).

---

## 🛠️ Maintenance & Lifecycle
1.  **The Binder Rule:** Every AI-detected revision change in Phase 5 must be printed and filed in the physical binder.
2.  **The Key Protocol:** ZFS Encryption passphrases must never be stored on the same physical node as the data.
3.  **The Audit:** Monthly "Insta-Restore" tests to verify S3 backup integrity.
