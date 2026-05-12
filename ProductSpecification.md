# SovrIT PTI: Product Specification

## 1. Introduction
### 1.1 Purpose
To reclaim digital autonomy by establishing a local-first, zero-trust infrastructure that replaces cloud-dependent services with a unified, encrypted ecosystem. Engineered to ensure that your data, communications, activit, and identity remain under your exclusive control, providing a stable and sovereign foundation for digital life that is immune to third-party surveillance or monetization.
### 1.2 Scope
This specification defines the technical boundaries and operational standards for the SovrIT PTI ecosystem. It encompasses the physical hardware architecture, logical network segmentation (VLANs, mesh overlay), and the Runtime Substrate - specifically identity, ingress, and storage layers. The scope extends to the integration of sovereign modules for communication, productivity, and intelligence, as well as a remote failover node for resiliency and "SovrIT Handbook" documentation systems.
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
* **Objective:** Maintain a geographically distant **Remote (VPS) Failover Node**.
* **Standard:** In the event of a local ISP or power failure, critical "Life-Line" services (Identity, Vault, and Communications) must automatically failover to the VPS to ensure zero downtime for remote users.

### 2.4 Invisible & Active Security
Security should be a silent partner, not a series of annoying pop-ups.
* **Objective:** Orchestrate a "Defense-in-Depth" stack overseen by the **SovrIT Steward** (Security LLM).
* **Standard:** Utilize **NetAlertX** for intrusion awareness and **CrowdSec** for behavioral blocking. SovrIT Steward correlates these signals to autonomously isolate threats and notify the user only when human judgment is required.

### 2.5 Sovereign Voice/AI Assistance
Intelligence must be private, local, and context-aware, utilizing a tiered model approach for different tasks.
* **Objective:** Process all AI requests (LLM, STT, TTS) on the local **Compute/LLM Node**.
* **Standard (Reasoning):** Utilize Gemma 4 for 100% local, high-speed, real-time voice interaction and complex, long-context document analysis (RAG).
* **Standard (Privacy):** No prompt data or personal records shall ever leave the network. The assistant has "Read-Only" access to the universal search index, providing insights from medical/legal/financial documents without exposing raw data to external APIs.

### 2.6 Decoupled Encryption at Rest
Physical possession of a server should not equal access to its data.
* **Objective:** Implement **ZFS-native encryption** where the master keys are never stored on the physical substrate.
* **Standard:** Encryption keys must be "injected" from a trusted mesh device during the boot sequence. If the server is powered down or removed from the premises, the data remains mathematically inaccessible noise.

### 2.7 Operational Continuity: The SovrIT Handbook
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

The SovrIT network is a hybrid architecture combining physical isolation (VLANs), an encrypted overlay (NetBird), and a geographically distant Remote (VPS) Failover Node (RFN).

### 3.1 Physical Segmentation (VLAN Schema)
The local substrate utilizes a "Default Deny" posture between five distinct security zones:

| VLAN ID | Name | Description & Policy |
| :--- | :--- | :--- |
| **10** | **MGMT** | 10.10.10.x - Infrastructure management (IPMI, Controllers). No WAN access. |
| **20** | **CORE** | 10.10.20.x - The Runtime Substrate (Identity, DNS, Ingress). Restricted WAN. |
| **30** | **TRUSTED** | 10.10.30.x - Primary user devices. Full mesh access. |
| **40** | **IOT** | 172.16.40.x - Isolated hardware (Cameras/Sensors). Zero outbound/inter-VLAN access. |
| **50** | **GUEST** | 192.168.0.x - Internet-only access. Total client isolation. |

### 3.2 The Sovereign Mesh & Remote (VPS) Failover Node (Hybrid Topology)
The network relies on **NetBird** (WireGuard) to bridge the home infrastructure with the remote VPS.
* **The SovrIT Cloud Mesh:** All administrative and inter-node traffic is encapsulated in a peer-to-peer overlay. No service ports are opened on the local home router.
* **The Remote (VPS) Failover Node:** Acts as a hardened, secondary node in the mesh.
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
* **Continuous Auditing (Lynis):** Automated security scans run weekly to identify configuration drift, outdated packages, or weak permissions. The "Hardening Index" from Lynis is reported directly to the SovrIT Steward for health tracking.

### 5.2 Intrusion Awareness & Proactive Defense
This layer monitors the "Wire" and the "Logs" for behavioral anomalies.
* **Network Sentry (NetAlertX):** Monitors the physical network substrate. It triggers immediate alerts for unauthorized MAC addresses or unrecognized device pings within the trusted VLANs.
* **Behavioral IPS (CrowdSec):** Acts as the "Immune System." It parses logs across all services to identify distributed brute-force attacks or L7 "scans" and blocks them at the firewall level.
* **Local Brute-Force Shield (Fail2Ban):** Provides high-speed, local banning for repeated authentication failures on critical infrastructure (SSH, Core Ops).

### 5.3 The SovrIT Steward (Security LLM)
The SovrIT Steward is a dedicated Security Large Language Model (LLM) that acts as the intelligent "Overseer" of the substrate.
* **The Intelligence Engine:** Utilizes local, security-tuned models (e.g., **VaultGemma** or **Cyber-Llama**) running on the Compute/LLM Node.
* **Role: Alert Triage & Correlation:** Instead of flooding the user with raw logs, SovrIT Steward correlates disparate events. 
    * *Example:* Correlating a blocked SSH attempt (Fail2Ban) with a new device on the network (NetAlertX) to elevate the threat level.
* **Role: Autonomous Remediation (SOAR):** SovrIT Steward executes automated playbooks via **n8n**. 
    * *Action:* If a service exhibits compromised behavior, SovrIT Steward can autonomously "Quarantine" the container by dropping its mesh connection and notifying the user via **ntfy**.
* **Role: Log Summarization:** Provides a daily "Security Heartbeat" summary, translating technical log spikes into plain English for the user.

---

## 6. Operational Automation & Self-Healing

The SovrIT ecosystem utilizes "Self-Healing Logic Trees" to ensure service continuity. This system is driven by a distinct layer of **Machine-Readable Standard Operating Procedures (mSOPs)** that exist independently of the human-facing Handbook.

### 6.1 The Operational Logic Substrate (mSOPs)
Automation is governed by structured logic files (mSOPs) stored within the system's version-controlled configuration (NixOS/Git). 
* **Separation of Concerns:** Unlike the Handbook, mSOPs are formatted for the **SovrIT Steward LLM** and **n8n** to execute. They contain the specific API calls, CLI commands, and logic branches required for autonomous remediation.
* **The "First Responder":** When a failure is detected, the system exclusively references the mSOPs. It only engages the human operator (and by extension, the Handbook) when these automated routines reach a "terminal fail" state.

### 6.2 The Remediation Loop (Observe-Orient-Decide-Act)
The SovrIT Steward follows a standardized loop to resolve degradation without human intervention:

1. **Observe:** **Uptime Kuma** or **NetAlertX** detects a service failure.
2. **Orient:** SovrIT Steward gathers system context (e.g., "Container is running, but logs show 'Out of Memory'").
3. **Decide:** The LLM parses the relevant **mSOP** logic tree to find the correct recovery path.
4. **Act:** n8n executes the remediation (e.g., "Clear temp cache and restart container").

### 6.3 Escalation: The Handoff to the Handbook
If the mSOP logic cannot resolve the issue, the system transitions from "Autonomous" to "Assisted" mode.
* **Incident Handover:** The SovrIT Steward ceases all automated write-actions to prevent further system instability.
* **Contextual Alerting:** An **ntfy** notification is sent to the human operator. This alert includes a direct link to the specific **SovrIT Handbook** page and the printed binder section required to fix the persistent issue.
* **Audit Trail:** The system provides the operator with a "Summary of Failed Attempts," detailing which mSOP branches were already tried and why they failed.

### 6.4 Health Check Standards
To support the mSOP layer, all services must provide "Visibility Hooks":
* **Web Services:** Standardized `/health` endpoints.
* **Substrate Nodes:** Real-time resource metrics via **Netdata**.
* **Integrity Checks:** Scheduled ZFS "scrub" and "trim" results must be readable by the SovrIT Steward.

---

## 7. Resilience & High Availability

This section defines the survival strategies for "Sovereign Life-Line Services." The goal is a **120-second RTO (Recovery Time Objective)** for identity and critical data access during a home-base outage.

### 7.1 The Remote (VPS) Failover Node Specifications
The Remote Failover Node is a geographically distant, hardened node acting as a "Warm Standby." To support the duplication of identity, financial, and medical document services, it must meet these minimums:
* **Compute:** 4 vCPU / 6GB RAM.
* **Storage:** 100GB NVMe (Primary OS + High-Priority Life-Line snapshots).
* **Network:** 10TB Monthly Bandwidth / 1Gbps Port.
* **Hardening Standards:** Strictly mesh-only SSH access via NetBird; host-level hardening via NixOS security profiles.

### 7.2 The Blueprint & State Sync
To ensure a perfect reconstruction, the system separates "How it works" from "The Data."
* **The Blueprint (Forgejo Mirror):** The master NixOS configuration and mSOP logic trees are hosted on a local **Forgejo** instance and automatically mirrored to a secondary Git repository on the VPS. This ensures the "System DNA" is always available even if the home server is physically destroyed.
* **The State (Kopia-S3):** Service-specific databases (Actual Budget, Vaultwarden) and document classes (Paperless-ngx) are encrypted client-side and synchronized to S3-compatible storage and the VPS NVMe at 1-4 hour intervals.

### 7.3 Failover Orchestration: The Life-Line Gate
* **Monitoring:** The VPS runs a light **Uptime Kuma** instance monitoring the Home Node’s mesh IP.
* **The Handover Logic:** If the Home Node is unreachable for >120 seconds:
    1. The VPS triggers a local activation script.
    2. Local "Warm" instances of Authentik, Vaultwarden, Paperless-ngx, and other serices are brought online.
    3. **NetBird DNS** is updated to route `auth.sovrit.lan` and `vault.sovrit.lan` to the VPS mesh IP.

### 7.4 The "Nuclear" Option: Site Reconstruction
In the event of total hardware loss at home, the Reconstruction Pipeline is as follows:
1. **Bootstrap:** Install base NixOS on new hardware and join the NetBird mesh.
2. **Clone:** Pull the master system configuration from the **Forgejo Mirror** on the VPS.
3. **Key Injection:** Re-authorize the new hardware via a trusted mesh device (Mobile/Laptop).
4. **Hydrate:** Execute the "Sovereign Restore" script to pull the ZFS hierarchy and service state from Kopia-S3.
5. **Rebuild:** Run `nixos-rebuild switch` to restore the entire 40+ service ecosystem to its exact pre-disaster state.

---

## 8. SovrIT Handbook (Operational Continuity)

The SovrIT Handbook is the human-centric "Fail-Safe." It ensures that the Digital Fortress remains operable even if auto-healing workflows fail or the primary administrator is unavailable.

### 8.1 The Physical-Digital Bridge
The Handbook exists in two synchronized states: a self-hosted **Dokuwiki** instance and a physical, printed **SovrIT Handbook Binder**.
* **Standard:** No technical change is considered "Production Ready" until the documentation reflects the current state of the UI.
* **The "Zero-Assumption" Rule:** Procedures must be written so a non-technical user can follow them to restore services when other means fail.

### 8.2 The Visual Parity Agent
To prevent documentation rot, the substrate utilizes a dedicated **Visual AI Agent** (e.g., Qwen2.5-VL) to audit the Handbook against the live environment.
* **Autonomous Auditing:** The agent periodically logs into system and module UIs and compares the screen layouts, menus, and dialogs to the screenshots in the Handbook.
* **Auto-Correction:** If a software update changes a layout, menu path, or dialog options:
    1. The agent captures and re-annotates a new screenshot.
    2. It updates the Markdown/Dokuwiki page with the new visual.
    3. It increments the revision number and triggers an **ntfy** alert for the user to print the updated page for the physical binder.

### 8.3 The Maintenance Cadence
* **The Print Cycle:** Monthly review of all "Flagged for Re-Print" pages.
* **The Restoration Drill:** Quarterly verification that the "Nuclear Option" (Section 7.4) can successfully hydrate a test node from the S3 archive.

---

## 9. Hardware Tiers & Performance Benchmarks

The hardware architecture is divided into three functional tiers to ensure compute-heavy tasks do not impact core service stability or data integrity.

### 9.1 The Network Tier
Provides the physical and logical "Moat" using accessible, prosumer-grade hardware.
* **Gateway Hardware:** Multi-VLAN capable router (e.g., TP-Link Omada ER605 or equivalent).
* **WAP Infrastructure:** Wi-Fi 6 Access Points with hardware-level SSID-to-VLAN mapping.
* **Benchmark (Internal):** Must support 1Gbps wire-speed switching within the same VLAN.
* **Benchmark (Inter-VLAN):** Must maintain a minimum of **300–500 Mbps** throughput when routing between CORE and TRUSTED zones with basic firewall rules active.

### 9.2 The Core Node (Storage & Substrate)
The "Heart" of the system, optimized for 24/7 uptime and data sovereignty.
* **Hardware Profile:** High-efficiency x86_64 nodes.
* **Storage Standard:** Minimum 2x mirrored drives for the Core substrate.

### 9.3 The Compute Node (LLM/Sovereign Intelligence)
The "Brain," dedicated to local inference, the SovrIT Steward, and the SovrIT Assistant.
* **Hardware Profile:** High-bandwidth/high VRAM architecture (Apple Silicon / M-Series Pro, Max, or Studio for its Unified Memory / Metal architecture) to support real-time local agents.
* **Inference Benchmarks:**
    * **SovrIT Steward (8B Model):** >30 tokens/sec for real-time log triage.
    * **Visual Agent (VLM):** <5 second processing time for UI audit screenshots.

### 9.4 Environmental Resilience & Power Protection
Hardware must be protected against environmental hazards and unconditioned power to prevent data corruption.
* **Thermal & Atmospheric Policy:** Systems must operate within hardware-specified thermal limits. In sites with extreme heat, humidity, or dust, active cooling and atmospheric filtration are mandatory.
* **Power Continuity Objective:** Every node must be capable of an orderly **ZFS export** and system shutdown before total battery depletion.
* **Monitoring Tiers:**
    * **Tier 1 (Direct):** Use of a "Smart UPS" with USB/HID integration (via **NUT**).
    * **Tier 2 (Simulated):** For "dumb" battery backups, the system shall utilize **Calculated Depletion Logic** to maximize uptime.
    * **AC-Sense Mechanism:** The system monitors a "Sacrifice Device" (e.g., a Zigbee smartplug) plugged directly into unconditioned wall power.
    * **Simulated State of Charge (SSOC):** 1. **Calibration:** The user must perform a one-time "Discharge Test" to determine the total runtime of the battery under a typical SovrIT load (e.g., 180 minutes).
        2. **Tracking:** Upon AC loss detection, a persistent timer tracks the "Minutes on Battery."
        3. **Logic:** The system calculates the remaining percentage: `(Total Runtime - Minutes Elapsed) / Total Runtime`.
    * **Trigger:** An orderly ZFS export and shutdown sequence is initiated only when the **SSOC reaches 15%**. If AC power is restored before this threshold, the timer is reset, and the shutdown is aborted.

---


## 10. Service Directory & Engine Selection

Every tool in the SovrIT ecosystem is selected based on three criteria: **Data Portability**, **SSO Compatibility (OIDC/SAML)**, and **Resource Efficiency**. This section provides the technical justification for the selected engines and explains why common alternatives were rejected.

### 10.1 SovrIT Core (Runtime Substrate)

#### 10.1.1 Networking & Security
* **NetBird:** Considered Tailscale (the market leader, but its control plane is proprietary and cloud-hosted), Headscale (an open-source Tailscale control plane, rejected due to its lack of a native, integrated web UI and the complexity of its OIDC integration), and ZeroTier. NetBird was selected for its native, high-performance peer-to-peer mesh, integrated Authentik support, and its ability to act as a complete "Sovereign VPN" without third-party dependencies.
* **AdGuard Home + Unbound:** Considered Pi-hole (lacks the native recursive capabilities provided by Unbound) and standard upstream DNS (Google/Cloudflare - rejected because they log DNS queries, creating a privacy leak). The pairing of AdGuard Home + Unbound ensures that DNS resolution happens locally at the "Root" level, making the user invisible to ISP tracking.
* **NetAlertX:** Considered WatchYourLAN for its "set-it-and-forget-it" simplicity but was ultimately rejected due to its lack of programmatic depth. NetAlertX provides a robust OpenAPI interface and native **n8n webhook** support, making it the only choice capable of feeding the **SovrIT Steward** with the high-fidelity telemetry required for autonomous threat remediation. Furthermore, its distributed master-slave architecture allows for seamless monitoring across all five SovrIT VLANs, whereas WatchYourLAN is strictly optimized for small, single-subnet environments.
* **Fail2Ban:** Considered CrowdSec (exclusively). While CrowdSec is the future of behavioral defense, Fail2Ban remains the "Shotgun at the Front Door" for local, signature-based protection. It was selected to provide immediate, low-latency banning for aggressive SSH and Auth attacks, acting as a secondary layer to the broader IPS.
* **CrowdSec:** Considered standard firewall blacklists (e.g., blocklist.de) but they are reactive and easily bypassed. CrowdSec was selected as the **Behavioral IPS/IDS** because it utilizes a community-sourced blocklist and local "Scenarios" to identify malicious patterns (like L7 scans) that signature-based tools like Fail2Ban would miss.
* **AppArmor:** Considered SELinux. SELinux was rejected due to its extreme complexity and "Policy Bloat," which often leads users to disable it entirely. AppArmor was selected for its "Profile-Based" approach, making it more maintainable for the SovrIT administrator while still providing robust service-level sandboxing.
* **Lynis:** Selected (over resource-heavy commercial scanners which often require cloud subscriptions) for its lightweight, local-first auditing of the NixOS host, providing a "Hardening Index" that the SovrIT Steward can monitor for configuration drift.
* **n8n:** Considered Node-RED (rejected because it lacks the "Job History" and structured JSON handling required for complex mSOP remediation) and Zapier (a cloud-based security nightmare). n8n provides a superior "Human-in-the-loop" interface, allowing the SovrIT Steward to execute complex security playbooks with ease.

#### 10.1.2 Access & Identity
* **Authentik:** Considered Okta (due to NetBird recommendation) but rejected it as it is a third-party SaaS platform which would constitute an "Identity Leak" to a corporate intermediary. Considered Authelia for its lightweight footprint but rejected due to its limited native OIDC/SAML provider capabilities and lack of a unified "App Portal" interface for non-technical users. Strongly considered Kanidm for its impressive Rust-based security-first architecture but ultimately rejected for its lack of an integrated "Outpost" and "Proxy" ecosystem. Authentik’s ability to secure legacy services that do not natively support modern authentication is essential for maintaining a unified Zero-Trust posture across the entire 40+ service stack. Authentik provides the best balance of enterprise-grade features, biometric **WebAuthn** support, and a manageable resource footprint.
* **Step-CA:** Considered Let's Encrypt (exclusively - rejected because it requires public DNS/HTTP challenges, which leak internal service names to public transparency logs) and OpenSSL (manual). Step-CA allows SovrIT to act as its own **Private PKI**, ensuring internal trust without leaking metadata to the public internet.
* **Traefik:** Considered Nginx Proxy Manager (NPM - rejected because it requires manual GUI configuration for every service, which breaks the "Self-Healing" automation) and Caddy. Caddy is excellent but Traefik is recommended by and integrates with Netbird more easily and completely.

#### 10.1.3 Core/Storage
* **NixOS:** Considered Ubuntu Server and Debian but NixOS was selected because it is **Declarative**. The entire system is defined in code which makes it much more conducive for autonomous self-healing and disaster recovery.
* **TrueNAS / ZFS:** Considered UnRAID and standard EXT4/LVM. UnRAID lacks the bit-rot protection and instantaneous snapshot capabilities of ZFS. ZFS was selected as the mandatory filesystem for its hardware-agnostic portability, "Copy-on-Write" architecture, which is the foundation of the system’s data integrity, and it's suitability for encryption at rest.
#### 10.1.4 Resilience
* **Kopia:** Considered Restic and Borg - both excellent but lacking a native, high-performance GUI and multi-backend S3 support as robust as Kopia's. Kopia’s content-addressable deduplication and client-side encryption make it the primary "Fortitude" engine for the 3-2-1-0 strategy.
* **Uptime Kuma:** Considered Nagios and Zabbix (Enterprise monitoring tools that are too complex for a home-scale environment) and Peekaping (for its lightweight focus on network latency and ICMP monitoring) but rejected it because it lacks the application-level depth (HTTP keyword checks, DNS resolution, and Docker health) required to trigger the SovrIT Steward's mSOP logic. Uptime Kuma's ability to serve as a visual "Status Dashboard" for non-technical users while providing a robust notification API for n8n makes it the superior choice for operational continuity.
* **Chrony:** Considered standard `ntpd`. Chrony was selected for its superior performance in environments with intermittent internet connectivity (e.g., outages), ensuring that cryptographic keys and MFA tokens remain synchronized even when the "High-Stratum" clock is unreachable.

---

### 10.2 SovrIT Modules (Applications)

#### 10.2.1 Intelligence & Discovery
* **Ollama/Whisper/Piper:** Considered OpenAI/Whisper API and Google TTS. Cloud APIs were rejected for violating the Zero-Knowledge mandate. Ollama (LLM), Whisper (STT), and Piper (TTS) provide a completely local, high-performance pipeline for the SovrIT Assistant.
* **Meilisearch:** Considered Elasticsearch and Solr. These are too resource-intensive for the Core node. Meilisearch provides "Instant Search" capabilities with a tiny memory footprint, allowing for universal discovery across all sovereign data.

#### 10.2.2 Communication & Social
* **Matrix:** Considered XMPP and Signal. Signal is excellent but tied to a phone number and central servers. XMPP lacks the modern "Bridge" ecosystem of Matrix. Matrix (via Mautrix) allows the user to unify WhatsApp, Signal, and iMessage into a single, sovereign archive.
* **VitalPBX:** Considered 3CX and FreePBX. 3CX is increasingly closed-source/commercial. FreePBX is aging. VitalPBX provides a modern, secure SIP-TLS/SRTP stack for encrypted sovereign telephony.
* **Stalwart:** Considered Mailcow and Mail-in-a-Box. Mailcow is a heavy multi-container stack. Stalwart is a single Rust binary that supports **S3-compatible storage natively**, making it the only viable choice for the "Remote Failover" geographically redundant mail strategy.
* **ntfy:** Considered Gotify and Pushover. Pushover is a third-party cloud service. Gotify is excellent but lacks the deep iOS/Android integration and "Actionable Notifications" provided by ntfy.

#### 10.2.3 Productivity & Office
* **FileBrowser Quantum:** Considered Nextcloud. Nextcloud was rejected for being "Monolithic" and notoriously slow. FileBrowser Quantum provides a lightning-fast, single-binary interface for file management without the bloat.
* **OnlyOffice:** Considered Collabora (LibreOffice Online). OnlyOffice provides superior compatibility with Microsoft Office formats, which is essential for interacting with the non-sovereign world.
* **Silverbullet:** Considered Obsidian and Logseq. Obsidian is a local-only app, making server-side AI interaction difficult. Silverbullet is a **Local-First Web Engine** that allows the Assistant to query the note library as a database.
* **Radicale:** Considered Baikal and Nextcloud Calendar. Radicale was selected for its extreme simplicity and flat-file storage, ensuring calendars and contacts are easily backed up and restored.

#### 10.2.4 Vital Archives
* **Actual Budget:** Considered Firefly III and YNAB. YNAB is a cloud subscription. Firefly III lacks a robust offline-first mobile experience. Actual Budget (Local-First) ensures transactions can be entered without internet and merged later.
* **Paperless-ngx:** Considered Mayan EDMS. Mayan is too complex for home use. Paperless-ngx provides the best OCR and auto-tagging experience for medical and legal archives.
* **Immich:** Considered Google Photos and Nextcloud Photos. Immich is the only self-hosted gallery that matches the UX and AI-tagging speed of Google Photos while maintaining absolute privacy.

#### 10.2.5 Media & Lifestyle
* **Jellyfin:** Considered Plex and Emby. Plex and Emby are proprietary and require "Phoning Home" to central servers. Jellyfin is strictly sovereign and open-source.
* **Home Assistant:** Considered OpenHAB and Apple HomeKit. Home Assistant is the gold standard for "Local-Only" automation, supporting the **Zigbee Sacrifice Device** logic required for Section 9.4.
* **Vaultwarden:** Considered the official Bitwarden RS. Vaultwarden is a lightweight Rust implementation that provides full feature parity with Bitwarden while running in a fraction of the memory.

---

## 11. Implementation Roadmap

Refer to **ProjectPlan.md** for the detailed, four-phase implementation roadmap, including hardware provisioning and service deployment timelines.
