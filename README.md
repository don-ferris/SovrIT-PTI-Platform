# SovrIT  *(Platform – this repo)*
**Personal Information Technology Platform**

SovrIT is a sovereign, self‑hosted personal IT infrastructure platform designed to return control of your digital life to you. Private by default and transparent by design, it replaces reliance on third‑party cloud services with a modular ecosystem you operate yourself — built to be used, understood and maintained by anyone in your home.

This repository defines the SovrIT Platform: the architecture, design philosophy, and long‑term principles that guide the entire SovrIT ecosystem. All SovrIT modules follow the patterns established here.

For a visual overview of the SovrIT architecture, see **[Architecture.md](Architecture.md)**.

---

## 🌱 Purpose

Most personal data today lives inside third‑party clouds you do not control — and is routinely inspected, analyzed, monetized, retained, and used in an attempt to track and manipulate you by the companies that store it, as well as by government agencies that increasingly disregard the spirit and intent of constitutional privacy protections. SovrIT exists to break that dependency by providing a stable, sovereign foundation for identity, authentication, communication, storage, automation, and daily digital routines — engineered and maintained with the same safeguards, discipline, and mission‑critical mindset found in enterprise IT environments.

Self‑hosting isolated services is not enough. True digital sovereignty requires that your data, your communications, and your daily digital operations be protected end‑to‑end. SovrIT establishes patterns for running essential services — authentication and MFA, file storage, document management, financial and health records, messaging, media, and more — with enterprise‑grade security, redundancy, and high availability. These services are encrypted, backed up regularly, and routed through personal, self‑hosted VPNs to ensure absolute privacy. The servers that host them are patched, monitored, and incrementally hardened to defend against ransomware, intrusion attempts, and evolving threats.

But SovrIT goes further. It provides the architectural patterns and mechanisms needed to bring basic voice and text communication under your control as well. Mobile devices can operate on data‑only plans, with encrypted phone calls, video calls, messages, and email routed through your own sovereign VPN infrastructure — shielded from carriers, ISPs, and any entity that would log, inspect, or monetize your communications.

In essence, SovrIT enables you to become your own ISP and your own mobile carrier — while still paying traditional providers only for the raw bandwidth required to move encrypted data. Your information should belong and be visible only to you — not to the companies that move and store it, nor to the government agencies that oversee them.

---

## 🧱 What SovrIT (Platform – this repo) Provides

- The mission, philosophy, and guiding principles of SovrIT  
- Architectural patterns for building sovereign, long‑lived services  
- Naming conventions, repo structure, and documentation standards  
- Expectations for reliability, privacy, and long‑term stewardship  
- Patterns for reducing reliance on third‑party providers  
- Sovereign communication and VPN design principles  
- Human‑centered documentation guidelines for a non‑technical spouse/partner  

SovrIT is not a single application. It is the blueprint for a personal digital infrastructure.

---

## 🧩 SovrIT Ecosystem Overview

### **SovrIT Core (runtime substrate)**  
The sovereign execution environment that all SovrIT modules run on.  
Core includes:

- **SovrIT SecureNet** — encrypted overlay network and sovereign VPN  
- **SovrIT Fortitude** — the resilience engine of SovrIT (backups, DR, monitoring, self‑healing, hardware redundancy)  
- Provisioning and hardening  
- Encrypted storage foundations  
- LLM‑guided maintenance and household operability  
- Bootstrap, patching, and lifecycle management  

### **SovrIT Modules**

- **SovrIT Access** — authentication, MFA, and account stewardship  
- **SovrIT Vault** — secrets, passwords, and encrypted storage  
- **SovrIT Ledger** — financial records  
- **SovrIT Med** — medical records  
- **SovrIT Legal** — legal and estate records  
- **SovrIT Handbook** — system documentation and manuals  
- **SovrIT Notify** — notifications and cross‑system messaging  
- **SovrIT Carrier** — sovereign voice, text, and messaging  

### **Integrations (optional)**

- Home Assistant  
- Media servers  
- Other self‑hosted applications  

---

## 🛡️ SovrIT Brand Pillars

### **Sovereignty by Design**
Your data, your systems, your rules.

### **Infrastructure‑Grade Reliability**
Predictable, quiet, and steady.

### **Modular, Composable Architecture**
Each SovrIT module is independent but interoperable.

### **Human‑Centered Clarity**
Documentation is written for a spouse/partner to operate confidently.

### **Craftsmanship and Transparency**
Every configuration is intentional, annotated, and inspectable.

### **Longevity and Stewardship**
SovrIT is designed to outlive any single device or trend.

---

## 📐 Architecture Principles

- Small, focused services instead of monoliths  
- Clear boundaries between modules  
- Declarative configuration wherever possible  
- Idempotent provisioning for predictable rebuilds  
- Documented interfaces between components  
- Local‑first design with cloud as an optional extension  
- Self‑hosted VPN and communication layers  
- Preference for open standards and long‑term maintainability  
- Continuous hardening, monitoring, and patching  

---

## 🔒 Sovereign Communication and Connectivity

- **Data‑only mobile plans** routed through a sovereign VPN  
- **Self‑hosted VPN infrastructure** (WireGuard, NetBird, Pangolin‑style)  
- **Encrypted, self‑hosted voice and messaging**  
- **Carrier‑independent communication**  
- **End‑to‑end encrypted routing** for all mobile and household communication  

---

## 📘 Documentation Standards

- Plain language, short paragraphs, and clear steps  
- Visuals and diagrams where helpful  
- Explanations of *why*, not just *how*  
- Glossaries for technical terms  
- Procedures that assume the reader may be stressed or tired  
- A tone that is calm, respectful, and empowering  

---

## 🔭 Roadmap

- Additional architectural diagrams  
- SovrIT glossary and terminology guide  
- Documentation style guide  
- Versioning and lifecycle policies  
- Templates for new SovrIT modules  
- Sovereign mobile workflows  
- Self‑hosted VPN migration paths  
- Expanded hardening and monitoring patterns  

---

## 📜 License

SovrIT is released under the MIT License. See `LICENSE` for details.
