# SovrIT Platform Functionality

> Implementations evolve. Capabilities endure.

# PLATFORM FUNCTIONS
---

## Networking
> **Description:** Provides trusted communication between people, devices, and services participating in the PTI.<br />
> **Fulfilled By:**<br />
> - TBD
## Security
> **Description:** Protects what matters by safeguarding people, information, systems, and services against unauthorized access, loss, or harm.<br />
> **Fulfilled By:**<br />
> - TBD
## Identity Management
> **Description:** Provides trusted identification and authentication of users, devices, and services participating in the PTI.<br />
> **Fulfilled By:**<br />
> - TBD
## Communications
> **Description:** Enables the exchange of information between people through the PTI.<br />
> **Fulfilled By:**<br />
> - TBD
## Knowledge Management
> **Description:** Preserves, organizes, and makes useful the information that supports the ongoing activities of a person's life.<br />
> **Fulfilled By:**<br />
> - TBD
## Automation
> **Description:** Delegates routine tasks and decision-making to the PTI, improving reliability, efficiency, and consistency.<br />
> **Fulfilled By:**<br />
> - TBD
## Home Management
> **Description:** Coordinates and manages residential systems and services that support daily living within the PTI.<br />
> **Fulfilled By:**<br />
> - TBD

---
---

# FUNCTIONAL CAPABILITIES

## Private Mesh Overlay Network
> **Why It Belongs:** Extend the PTI beyond the physical home by creating a trusted private network that securely connects users, devices, and remote nodes regardless of their physical location. This allows the PTI to remain the user's primary network whether at home or away, enabling remote failover, data synchronization, and secure access to PTI services while preventing network traffic from being observed by mobile carriers, ISPs, public Wi-Fi providers, or other intermediary networks.<br />
> **Planned Implementation:**<br />
> - [NetBird](https://netbird.io/) ([GitHub](https://github.com/netbirdio/netbird))
> **Notes:**<br />
> - Enables the Remote Failover Node (RFN) to participate as a full member of the PTI.
> - Intended to carry all practical traffic from mobile devices so the PTI remains the user's trusted network regardless of location.
> - Forms the foundation for secure communication between geographically separated PTI components.
---
## Server Hardening
> **Why It Belongs:** Reduce the attack surface of PTI servers by implementing layered security controls that make them more resistant to unauthorized access, exploitation, and compromise while preserving their intended functionality. Server hardening is fundamental to protecting the confidentiality, integrity, and availability of the PTI and the data it stores.<br />
> **Planned Implementation:**<br />
> - [CrowdSec](https://www.crowdsec.net/) ([GitHub](https://github.com/crowdsecurity/crowdsec))
> - [Lynis](https://cisofy.com/lynis/)
> - [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)
> - [OpenSSH](https://www.openssh.com/) (SSH hardening)
> - [AppArmor](https://apparmor.net/)
> **Notes:**<br />
> - Servers should be hardened to the greatest practical extent without interfering with their intended functionality.
> - This capability encompasses multiple hardening techniques and technologies that work together to reduce the attack surface of PTI servers.
> - SELinux is intentionally omitted pending further evaluation.
---