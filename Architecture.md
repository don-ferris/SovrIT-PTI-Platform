# SovrIT Architecture

This document provides a visual overview of the SovrIT Platform, SovrIT Core, and SovrIT Modules.  
It is intentionally high‑level and conceptual — detailed component‑level diagrams will live in the individual module repositories.

---

## 🧩 High‑Level Architecture

```mermaid
flowchart TD

    subgraph Platform["SovrIT Platform"]
        P1[Philosophy]
        P2[Architecture]
        P3[Design Principles]
        P4[Documentation Standards]
        P5[Sovereignty Patterns]
    end

    subgraph Core["SovrIT Core (runtime substrate)"]
        C1[SovrIT SecureNet]
        C2[SovrIT Fortitude]
        C3[Provisioning & Hardening]
        C4[Encrypted Storage Foundations]
        C5[LLM‑Guided Ops]
    end

    subgraph Modules["SovrIT Modules"]
        M1[SovrIT Access]
        M2[SovrIT Vault]
        M3[SovrIT Ledger]
        M4[SovrIT Med]
        M5[SovrIT Legal]
        M6[SovrIT Handbook]
        M7[SovrIT Notify]
        M8[SovrIT Carrier]
    end

    subgraph Integrations["Integrations (optional)"]
        I1[Home Assistant]
        I2[Media Servers]
        I3[Other Self‑Hosted Apps]
    end

    Platform --> Core
    Core --> Modules
    Modules --> Integrations
