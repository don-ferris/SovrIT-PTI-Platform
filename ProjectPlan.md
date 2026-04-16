# Project Plan - SovrIT PTI
## Phase 0: Network Setup
Replace consumer-grade/ISP-provided router with business-grade products, that support VLANs and better firewall controls and policies. 
**WILLWIF:** The Network Foundation and Edge infrastructure are established and verified. The gateway router is fully initialized with non-default, high-entropy credentials and a stable WAN connection.
Logical segmentation is implemented via at least five distinct VLANs (Management, Home, SovrIT, IoT, and Guest) with a strict "Default Deny" firewall posture, ensuring that no traffic can move between segments unless explicitly permitted. A centralized controller is active and successfully managing all network hardware (Router and WAPs), providing a single point of administrative control.
Finally, a secure wireless environment is active, with specific SSIDs mapped to their corresponding VLANs. This ensures that every device—from a core server to a guest’s phone—is instantly isolated into its designated security zone the moment it connects to the wire or the air.
