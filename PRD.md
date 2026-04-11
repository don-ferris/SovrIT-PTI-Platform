# SovrIT PTI - Product Requirements Document

## 1. Header & Metadata
* **Status:** Draft 
* **Owner:** @don-ferris
* **Stakeholders:** @TBD
* **Target Release:** Version 1.0

---

## 2. Executive Summary
### Objective
**Mission:** Total Digital Independence

**Vision:** A world where individuals own their data, their history, and their future — with absolute sovereignty and complete privacy.

---

## 3. The Problem: Data Serfdom
We currently live our digital lives on "rented land." Our family photos, financial and medical records, personal documents, and private communications are stored on servers owned by a handful of huge corporations and subject to their oversight and privacy violations - whether for the purpose of monetization, marketing/manipulation, collaboration with other big corporations, or governmental surveillance and overreach. This isn't just a privacy issue; it’s a dependency issue. If a provider changes their terms, raises prices, or discontinues service, you lose your history and must scramble to find an acceptable replacement. You are a tenant in a digital ecosystem where you don't own the land, the walls, or the locks.

---

## 4. The Solution: SovrIT PTI
**SovrIT PTI (Personal/Private Technology Infrastructure)** is a blueprint for independence. It is a self-hosted "Digital Fortress" built on hardware you own, running software you control. It replaces “the Cloud" with a private, invisible network that is accessible globally — to you, your family, and _no one else._

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
The SovrIT Assistant serves as the primary gateway to the system's intelligence, serving as  both a voice and chat-based AI assistant. By utilizing local Large Language Models (LLMs) and high-fidelity speech-to-text engines, the assistant processes complex intents, performs multi-step research, and executes system automations entirely within the private network. This sovereign intelligence is natively integrated with the universal search index, allowing the SovrIT Assistant to provide context-aware insights from personal records while remaining 100% private and immune to third-party data collection
### 6. Decoupled Encryption at Rest
All data is secured using hardware-agnostic, filesystem-level encryption (AES-256-GCM). By decoupling encryption keys from physical hardware, the system ensures that data remains mathematically indistinguishable from noise if the servers are physically seized or compromised.
### 7. Operational Continuity - The Living Handbook
Comprehensive "Human-Centric" documentation ensures the system can be maintained and recovered by anyone in the household. An AI-audited Handbook uses annotated screenshots and real-time UI tracking to ensure that the documentation precisely matches the screen layout,  menus, dialogs, and options that the user sees on-screen. This provides non-technical family members with a clear, visual roadmap to maintain and operate the system if the family IT person is unavailable.

---

## 6. User Stories
### 1. The Catastrophe Survivor
_”As a homeowner who previously lost every physical record and family album during Hurricane Katrina, I want to have my vital data automatically failover to a remote VPS "Ghost Mirror," so that my family’s documentation and history survive even in the event of total local site destruction.”_
### 2. The Platform Refugee
_”As a consumer whose primary photo service was sunsetted last year and whose other cloud subscriptions just had substantial price hikes, I want to invest in high-capacity local hardware that I own, so that I can stop being a digital tenant and ensure my services never disappear due to a corporate board’s decision.”_
### 3. The Ransomware Defender
_”As a user who saw every important file and family photo encrypted by a ransomware attack ten months ago, I want my system to utilize immutable snapshots and automated "Insta-Restores" from an encrypted S3 vault, so that I can instantly roll back an attack without losing data or paying a criminal.”_
### 4. The Emergency Access Protocol
_”As a family member who sat in an emergency room for six hours unable to access a spouse’s medical history because it was locked behind a cloud account I didn't have the password for, I want a physical Operating Manual with annotated screenshots and AI-verified procedures, so that I can immediately retrieve vital life-saving information even if the family IT person is incapacitated.”_
### 5. The Burglary-Proof Professional
_”As a business owner whose office was burglarized and server stolen last year—resulting in a public data breach and massive fines because the drives were unencrypted, I want my encryption keys to be decoupled from my hardware, so that if my servers are ever physically removed, the data remains a mathematically unreadable brick.”_
### 6. The Metadata Privacy Advocate
_”As an individual who was targeted by identity thieves after a major data broker leaked a profile of my habits and contacts, I want to route all my communications through a private hub I own, so that no third-party carrier can track my location or sell a log of my private interactions.”_
### 7. The Flood-Proof Habitat
_”As a homeowner who returned from vacation to a flooded basement because my smart water sensor failed to alert me when its manufacturer's cloud service went down for maintenance, I want my smarthome logic to reside on dedicated, local-only hardware, so that my sensors and automations work 100% of the time, regardless of an internet connection or corporate server status.”_
### 8. The Coffee Shop Breach Survivor
_”As a user whose primary credentials were stolen during a “Man-In-The-Middle” attack while I sipped a mochasccino, I want my identity and password vault to be hosted on my own internal fortress and protected by a physical security key, so that my most sensitive data is never exposed on a public-facing corporate server that can be intercepted or spoofed.”_
### 9. The Private Sentinel
_”As a resident who is aware that major camera companies have shared customer footage with third parties without consent, I want my surveillance system to process AI detection locally on my own silicon, so that I have total property awareness without giving a corporation a 24/7 window into my home.”_
### 10. The Permanent Professional
_”As a remote worker who lost access to critical documents during a massive three-day cloud provider outage, I want to host my collaborative office tools on a local server that mirrors to a global failover node, so that my work remains accessible and private even when the public internet fails.”_

---

## 7. Functional Requirements
| ID | Feature Name | Priority | Requirement Description |
| :--- | :--- | :--- | :--- |
| **FR-01** | **Mesh Networking** | High | Establish an encrypted P2P mesh network ([Netbird](https://netbird.io/)) to facilitate secure node communication without public port exposure. |
| **FR-02** | **Universal Identity** | High | Provide a centralized Identity Provider ([Authentik](https://goauthentik.io/)) for OIDC/SAML authentication across all system modules. |
| **FR-03** | **Biometric Gatekeeper** | High | Mandate ([WebAuthn](https://webauthn.guide/)) (FaceID/TouchID) as the primary MFA via [Authentik](https://goauthentik.io/) to ensure high security with zero daily user friction. |
| **FR-04** | **Edge Traffic Control** | High | Implement an edge proxy ([Traefik](https://traefik.io/)) supporting gRPC and automated SSL management for mesh-wide routing. |
| **FR-05** | **Insta-Restore Engine** | High | Provide a dashboard (n8n/Ansible) to rebuild core services from a clean state using versioned configs and S3 data. |
| **FR-06** | **Universal Sovereign Search** | High | Deploy a centralized, lightning-fast indexer ([Meilisearch](https://www.meilisearch.com/)) that provides exhaustive, real-time search across mail, messages, files, notes, bookmarks, web history, and more. |
| **FR-07** | **Local AI Assistant** | High | Replace cloud assistants with local AI ([Ollama](https://ollama.com/), [Whisper](https://github.com/SYSTRAN/faster-whisper), [Piper](https://github.com/rhasspy/piper)) for voice commands, deep context queries, and hands-free data entry. |
| **FR-08** | **Encrypted Telephony** | High | Utilize SIP-TLS for signaling and SRTP for media to ensure mesh-wide encrypted voice communication. || **FR-07** | **Unified Messenger Hub** | High | Bridge external networks (WhatsApp, Signal, iMessage) into a [Matrix](https://matrix.org/) homeserver using [Mautrix](https://mautrix.net/) bridges to maintain a single local chat history. |
| **FR-09** | **Integrated Virtual Office** | High | Provide a high-speed file explorer ([FileBrowser](https://filebrowser.org/)) with integrated collaborative document, spreadsheet, and presentation editing ([OnlyOffice](https://www.onlyoffice.com/)). |
| **FR-10** | **Sovereign Mail Engine** | High | Host a modern, memory-safe email server ([Stalwart](https://stalwart.io/)) to ensure total ownership of personal and professional correspondence. |
| **FR-11** | **At-Rest Encryption** | High | Secure all user data using filesystem-level encryption ([ZFS](https://openzfs.org/)) with keys decoupled from physical boot media for maximum protection. |
| **FR-12** | **Immutable Backups** | High | Execute hourly encrypted client-side backups ([Kopia](https://kopia.io/)) to offsite S3-compatible storage to ensure data recoverability. |
| **FR-13** | **Remote Failover Mirror** | High | Maintain a minimal "Ghost Mirror" on a remote VPS to ensure access to Identity, Password Vault, and Vital Records during local hardware or internet outages. |
| **FR-14** | **Graceful Power Safety** | High | Integrate UPS monitoring to trigger clean shutdowns of virtual machines and storage pools during sustained power failures. |
| **FR-15** | **Versioned Infrastructure** | High | Maintain all OS and service configurations (NixOS/Ansible) in a private Git repository (Forgejo) for state reproducibility. |
| **FR-16** | **Internal Time Server** | High | Integrate UPS monitoring to trigger clean shutdowns of virtual machines and storage pools during sustained power failures. |
| **FR-17** | **Gateway Dashboard** | High | Maintain a unified web interface (Flame) as the primary entry point for all services, protected by the central IdP. |
| **FR-18** | **Secure Remote Access** | High | Enable secure, mesh-only management of the Proxmox/NixOS substrate from authorized mobile devices via Netbird. |
| **FR-19** | **Local Certificate Authority** | High | Implement an internal ACME server (Step-CA or Traefik) to issue trusted SSL certificates for all mesh-only domains. |
| **FR-20** | **Database Atomic Snapshots** | High | Coordinate ZFS snapshots with database "freeze" commands to ensure backup consistency. |
| **FR-21** | **Mobile Device Hardening** | High | Ensure mobile clients are configured to route all sovereign traffic through the mesh with "Always-On" VPN logic. |
| **FR-29** | **Resource Quotas** | High | Implement strict CPU/RAM limits for non-critical services to ensure Identity and Resilience services remain responsive. |
| **FR-30** | **Hardware Wear Monitoring** | Medium | Monitor SSD/NVMe S.M.A.R.T. data and trigger proactive alerts when "Remaining Life" falls below 15%. |
| **FR-22** | **Zero-Log Application Config** | Medium | Force containerized applications to log to the central aggregator while disabling identifiable debug logs to local disk. |
| **FR-23** | **Financial Auditor (Money)** | Medium | Integrate receipt capture ([QuickScan](https://www.quickscanapp.com/)) and OCR ([Paperless-ngx](https://docs.paperless-ngx.com/)) with spending analysis ([Actual Budget](https://actualbudget.org/)), including voice-based transaction logging. |
| **FR-24** | **Vital Records (Med/Legal)** | Medium | Automate the indexing and OCR of medical and legal documents ([Paperless-ngx](https://docs.paperless-ngx.com/)) for instant retrieval via the universal search interface. |
| **FR-25** | **AI Photo Management** | Medium | Host a gallery ([Immich](https://immich.app/)) with ML-driven deduplication and automated purging of low-value media (e.g., screenshots, blurry photos, pocket shots) after a set period. |
| **FR-26** | **End-to-End Notes** | Medium | Provide encrypted note-taking ([Notesnook](https://notesnook.com/)) with local synchronization and automated ingestion into the universal search index. |
| **FR-27** | **Web Memory & History** | Medium | Index and archive every web page visited ([ArchiveBox](https://archivebox.io/), [Promnesia](https://github.com/karlicoss/promnesia)) to create a private, exhaustive, and searchable history of personal research. |
| **FR-28** | **Permanent Bookmarking** | Medium | Provide a "Read-it-Later" service ([Readeck](https://readeck.org/)) that archives web content as searchable PDFs and supports Pinterest-style visual pinning. |
| **FR-29** | **Schedules & People** | Medium | Host synchronized calendars and contact directories via CalDAV/CardDAV ([Radicale](https://radicale.org/)) with native mobile integration. |
| **FR-30** | **The Living Handbook** | Medium | Maintain internal system documentation in a database-less format ([Dokuwiki](https://www.dokuwiki.org/)) to ensure readability during extreme system degradation. |
| **FR-31** | **Private Geolocation** | Medium | Host a private location tracking server ([Traccar](https://www.traccar.org/)) and vector tile server ([MapLibre](https://maplibre.org/)) to provide map services without third-party tracking. |
| **FR-32** | **Smart Home (Habitat)** | Medium | Centrally manage lights, climate, and sensors via a local-only hub ([Home Assistant](https://www.home-assistant.io/)) completely isolated from the public internet. |
| **FR-33** | **AI Handbook Auditor** | Medium | Employ a local agent to audit service UIs and update the Knowledge Base with annotated screenshots for visual and instructional parity. |
| **FR-34** | **Network Segmentation** | Medium | Isolate IoT and automation hardware into dedicated VLANs with zero outbound internet access to prevent lateral network attacks. |
| **FR-23** | **Air-Gapped IoT Radio** | Medium | Utilize local radio protocols (Zigbee/Z-Wave) that are physically incapable of communicating with the public internet. |
| **FR-25** | **OCR Record Archive** | Medium | Automatically OCR-index all uploaded PDFs to allow for full-text search of medical, legal, and financial records. |
| **FR-26** | **Digital Dead-Man Switch** | Medium | Trigger an automated information handover to beneficiaries if a user heartbeat is not detected for 30 days. |
| **FR-27** | **P2P Asset Sync** | Medium | Facilitate direct, encrypted synchronization of files and photos between mobile devices and the home node. |
| **FR-28** | **Automated Health Reports** | Medium | Generate weekly system health reports (Disk wear, backup integrity, failed auth attempts) sent via private mesh. |
| **FR-31** | **Snapshot Pruning Logic** | Medium | Implement automated ZFS snapshot thinning (hourly, daily, weekly retention) to optimize disk space. |
| **FR-32** | **Bandwidth QoS** | Medium | Implement Quality of Service (QoS) rules to prioritize mesh-failover and telephony traffic over media synchronization. |
| **FR-34** | **Local AI NVR** | Medium | Utilize local hardware acceleration for object detection; no video metadata may be sent to third-party clouds. |
| **FR-35** | **Log Aggregation** | Low | Centralize and encrypt logs from all nodes for auditing and troubleshooting without cloud log-analyzers. |
| **FR-36** | **MFA Recovery Vault** | Low | Establish a physical "Break-Glass" procedure involving paper-stored recovery codes and Yubikeys secured in a physical safe. |
| **FR-35** | **Sovereign Social Feed** | Low | Deploy private social networking and photo sharing ([Pixelfed](https://pixelfed.org/), [GoToSocial](https://gotosocial.org/)) to facilitate communication without metadata harvesting. |
| **FR-36** | **Media & YouTube Hub** | Low | Provide streaming of movies and music ([Jellyfin](https://jellyfin.org/)) with automated local archiving of relevant YouTube content ([TubeArchivist](https://tubearchivist.com/)). |
| **FR-37** | **Digital Library (Books)** | Low | Centralize e-books and audiobooks ([Kavita](https://www.kavitareader.com/), [Audiobookshelf](https://www.audiobookshelf.org/)) into a unified, cross-device accessible library. |
| **FR-38** | **Physical Security (Sentinel)** | Low | Utilize local AI object detection ([Frigate](https://frigate.video/)) for camera feeds to ensure no metadata or video streams are sent to third-party clouds. |
| **FR-37** | **Encryption Key Rotation** | Low | Support a procedure for rotating ZFS encryption master keys and IdP signing keys without data loss. |
| **FR-38** | **Encrypted Temp-Sharing** | Low | Provide a mechanism for sharing large files via auto-expiring, password-protected links. |
| **FR-40** | **Physical Asset Tracking** | Low | Maintain an encrypted inventory of all physical hardware (serial numbers, MAC addresses) within the Handbook. |

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


