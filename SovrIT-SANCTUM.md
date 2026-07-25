# SovrIT SANCTUM
> _Sovereign Attestation Network for Conditional Trust & Unlock Management_
> _A Context-Aware Distributed Trust System for Physical Compromise Detection and Conditional Key Release _
> _Protecting critical user data by protecting the phytsical devices on which it resides._

---

### Abstract

Modern encrypted storage systems are highly effective against remote compromise, but remain vulnerable to a critical class of attacks:
- physical seizure,
- theft,
- coercion,
- insider compromise,
- and live-system capture.

Traditional encryption systems operate on a simple assumption:

> possession of a valid decryption key implies authorization.

This assumption breaks down under adversarial physical conditions.

SovrIT SANCTUM introduces a distributed, context-aware attestation framework designed to evaluate environmental, operational, behavioral, and human trust signals before allowing encrypted ZFS pools to decrypt.

Unlike conventional approaches, SANCTUM does not rely on a single trust source. Instead, it combines:
- distributed attestations,
- environmental monitoring,
- operational continuity validation,
- intrusion awareness,
- weighted trust scoring,
- planned reboot declarations,
- and conditional human authorization.

The result is a sovereignty-oriented architecture capable of resisting real-world physical compromise scenarios while preserving operational usability for legitimate users and households.

---

## 1. Introduction

### 1.1 The Problem

Traditional encrypted storage systems answer a binary question:

> "Was the correct key supplied?"

They generally cannot answer:
- whether the system has been stolen,
- whether the environment has been compromised,
- whether the reboot was expected,
- whether the operator is under duress,
- or whether automatic trust assumptions are being manipulated by an adversary.

This creates a dangerous gap between:
- cryptographic security,
- and operational security.

Examples include:
- theft of powered infrastructure,
- coordinated seizure,
- malicious maintenance access,
- covert tampering,
- staged outages,
- or attacks designed to trigger unattended auto-unlock workflows.

SANCTUM is designed to evaluate not only:
- *whether decryption is possible*,
but also:
- *whether decryption should occur at all.*

---

## 2. Design Philosophy

SANCTUM operates according to six foundational principles.

---

### 2.1 Trust Must Be Distributed

No single component may independently authorize decryption.

Trust is distributed across:
- environmental observations,
- hidden beacons,
- continuity witnesses,
- network state,
- operational declarations,
- and user authorization.

---

### 2.2 Human Authorization is Strongly Preferred — But Not Universally Required

Human authorization is the highest-trust signal available to SANCTUM.

However, SANCTUM recognizes that:
- legitimate users may be unreachable,
- households may depend on uninterrupted services,
- and safe unattended recovery may sometimes be necessary.

Therefore:
- human authorization is not universally mandatory.

Instead:
- SANCTUM may permit unattended decryption only when an exceptionally low-threat state can be established through corroborating evidence.

This intentionally sets a very high bar.

---

### 2.3 Planned Operational Continuity Matters

A declared and expected reboot event significantly increases trust.

Planned reboot declarations may originate from:
- SovrIT Steward,
- SovrIT Fortitude,
- maintenance orchestration systems,
- update workflows,
- or administrative scheduling systems.

If a planned reboot declaration exists and all supporting continuity checks succeed, SANCTUM may permit unattended recovery even without direct human interaction.

---

### 2.4 All Signals Are Potentially Compromised

Attackers are assumed to:
- understand SANCTUM,
- know its defenses,
- and actively attempt to bypass them.

Therefore:
- no signal is treated as infallible,
- no environmental sensor is authoritative,
- and contradictory evidence reduces trust.

---

### 2.5 The System Must Fail Closed

False positives are catastrophic.

If SANCTUM cannot establish sufficient confidence:
- encrypted pools remain locked.

Operational inconvenience is preferable to compromise of sovereign data.

---

### 2.6 Rapid Cryptographic Evaporation

If compromise is suspected while systems are running:
- active encryption keys are destroyed,
- pools are exported,
- sessions are revoked,
- and operational trust material is invalidated.

This reduces exposure during live seizure events.

---

## 3. High-Level Architecture

| Component | Function |
|---|---|
| SANCTUM Engine | Central trust evaluation system |
| SovrIT Sentry | Environmental awareness and intrusion analysis |
| Anchors | Hidden local continuity beacons |
| Relays | Remote continuity witnesses |
| Custodian | Conditional key authority |
| BlackFlag | Duress and coercion subsystem |
| Steward/Fortitude | Operational continuity and maintenance orchestration |

---

## 4. SANCTUM Engine

The SANCTUM Engine is the core policy and trust evaluation subsystem.

It evaluates:
- environmental conditions,
- continuity signals,
- declared operational events,
- historical behavior,
- network conditions,
- and authorization evidence.

The engine determines whether:
- decryption is permitted,
- delayed,
- denied,
- or escalated into lockdown mode.

---

## 5. SovrIT Steward & Fortitude

Steward and Fortitude are trusted operational orchestration systems responsible for:
- maintenance coordination,
- autonomous rebuilds,
- patch scheduling,
- resilience operations,
- and continuity declarations.

One of their most important functions within SANCTUM is the publication of:

#### Planned Reboot Declarations

These declarations indicate:
- an expected reboot,
- expected outage timing,
- expected maintenance windows,
- and anticipated infrastructure state changes.

This allows SANCTUM to distinguish:
- expected operational behavior,
from:
- suspicious or adversarial events.

---

### 5.1 Planned Reboot Trust Elevation

A valid planned reboot declaration may significantly increase trust if:
- the reboot occurs within the expected time window,
- continuity beacons remain present,
- no intrusion indicators are detected,
- network topology remains consistent,
- and environmental observations appear normal.

Under sufficiently safe conditions:
- SANCTUM may permit unattended decryption without direct user interaction.

---

## 6. SovrIT Sentry

Sentry is the environmental awareness subsystem.

It monitors:
- cameras,
- microphones,
- occupancy,
- tamper sensors,
- power conditions,
- network continuity,
- and environmental anomalies.

Sentry contributes probabilistic trust signals only.

It is intentionally non-authoritative.

---

### 6.1 Positive Indicators

Examples include:
- expected occupancy patterns,
- ordinary outage conditions,
- normal environmental continuity,
- no observed intrusion activity.

---

### 6.2 Negative Indicators

Examples include:
- forced entry,
- camera tampering,
- environmental disruption,
- unexpected movement of infrastructure,
- simultaneous ISP and power interruption,
- or physical removal of equipment.

---

## 7. Anchors

Anchors are concealed local continuity beacons.

Examples may include:
- modified ESP32 smart bulbs,
- hidden embedded devices,
- secure microcontrollers,
- low-power concealed nodes.

Anchors do NOT store decryption keys.

Instead they provide:
- signed attestations,
- continuity validation,
- location continuity evidence,
- and environmental telemetry.

Their purpose is to help determine whether infrastructure remains within its expected operational environment.

---

## 8. Relays

Relays are geographically distributed friend nodes.

They function as:
- continuity witnesses,
- distributed attestation participants,
- and behavioral corroboration systems.

Relays may consist of:
- low-power embedded devices,
- WireGuard endpoints,
- secure micro routers,
- or lightweight embedded systems.

Relays do not independently authorize decryption.

Their purpose is observational and corroborative.

---

## 9. Custodian

Custodian is the conditional key authority.

Operational decryption authority is released only after SANCTUM determines that:
- trust conditions are sufficiently satisfied,
- and no active compromise indicators exist.

Importantly:
- SANCTUM does not permanently distribute operational decryption keys to low-trust devices.

Instead:
- ephemeral unlock authority is conditionally reconstructed during trusted boot conditions.

---

## 10. BlackFlag

BlackFlag is the coercion and duress subsystem.

It allows operators to:
- silently indicate compromise,
- trigger deceptive unlock paths,
- revoke future trust,
- or initiate delayed lockdown procedures.

Duress responses may:
- appear successful,
- reveal decoy datasets,
- or expose sanitized environments.

---

## 11. Trust Evaluation Model

SANCTUM uses:
- weighted contextual trust scoring,
- continuity validation,
- operational declarations,
- and conditional authorization logic.

---

### 11.1 Trust Categories

| Category | Examples |
|---|---|
| Operational Continuity | Planned reboot declarations |
| Environmental Safety | No intrusion indicators |
| Continuity Presence | Anchors and relays present |
| Network Consistency | Expected topology continuity |
| Human Authorization | User challenge response |
| Threat Indicators | Tamper or anomaly detection |

---

### 11.2 Human Authorization Weighting

Human authorization remains the highest-confidence trust factor.

However, unattended unlocks may still occur if:
- a planned reboot declaration exists,
- continuity indicators strongly corroborate safety,
- environmental threat indicators are absent,
- and aggregate trust exceeds an elevated threshold.

This permits:
- resilient household operation,
- autonomous recovery,
- and safe unattended maintenance workflows.

---

## 12. Example Scenarios

---

### 12.1 Planned Autonomous Rebuild

#### Conditions
- Steward publishes planned reboot declaration,
- reboot occurs within expected window,
- anchors remain present,
- relays observe expected continuity,
- no intrusion indicators detected.

#### Result
- unattended decryption permitted.

---

### 12.2 User Traveling With No Connectivity

#### Conditions
- user unreachable,
- expected outage occurs,
- planned reboot declaration exists,
- environmental continuity appears normal,
- no threat indicators observed.

#### Result
- unattended decryption permitted.

---

### 12.3 Neighborhood Power Outage

#### Conditions
- UPS exhausted,
- ordinary outage characteristics,
- no intrusion indicators,
- continuity beacons remain present.

#### Result
- decryption permitted.

---

### 12.4 Theft

#### Conditions
- abrupt movement,
- loss of anchors,
- suspicious motion detected,
- no continuity corroboration,
- network disruption.

#### Result
- decryption denied.

---

### 12.5 Coordinated Seizure

#### Conditions
- live infrastructure removal,
- environmental anomalies,
- user enters duress PIN.

#### Result
- deceptive unlock behavior initiated,
- operational datasets remain protected.

---

### 12.6 ISP Severed Before Entry

#### Conditions
- ISP disruption,
- power remains online,
- suspicious environmental activity detected.

#### Result
- emergency cryptographic evaporation initiated.

---

## 13. Rapid Cryptographic Evaporation

If active compromise is suspected:
- encryption keys are destroyed,
- ZFS pools exported,
- containers terminated,
- sessions revoked,
- and temporary trust material invalidated.

This minimizes exposure during active compromise scenarios.

---

## 14. Cryptographic Model

SANCTUM uses:
- layered encryption,
- distributed attestations,
- ephemeral unlock authority,
- and contextual policy enforcement.

Shamir's Secret Sharing may be used selectively for:
- archival recovery,
- catastrophic reconstruction,
- or emergency administrative recovery.

However:
- SANCTUM is fundamentally policy-driven rather than threshold-driven.

Contextual trust evaluation remains central to the architecture.

---

## 15. Privacy & Sovereignty Goals

SANCTUM aligns with the broader SovrIT mission:
- local-first infrastructure,
- operational resilience,
- privacy preservation,
- minimized third-party dependence,
- and sovereign control of digital systems.

The architecture intentionally avoids:
- centralized trust providers,
- cloud dependency,
- and single-authority unlock systems.

---

## 16. Limitations

SANCTUM is not designed to guarantee perfect protection against:
- already-mounted datasets,
- advanced hardware implants,
- insider compromise,
- or direct coercion against legitimate operators.

Instead, SANCTUM is designed to:
- reduce automatic trust,
- increase adversarial uncertainty,
- delay compromise,
- and require attackers to defeat multiple independent trust domains simultaneously.

---

## 17. Future Research Directions

Potential future capabilities include:
- RF environmental fingerprinting,
- WiFi topology attestation,
- BLE continuity analysis,
- decentralized unlock consensus,
- secure enclave integration,
- tamper-reactive hardware,
- and post-quantum cryptographic support.

---

## 18. Conclusion

Traditional encrypted storage systems ask:

> "Do you possess the key?"

SANCTUM asks:

> "Should the system trust this environment enough to release the key at all?"

By combining:
- distributed trust,
- environmental awareness,
- operational continuity validation,
- contextual policy enforcement,
- and conditional authorization,

SovrIT SANCTUM introduces a new approach to sovereign infrastructure protection against real-world physical compromise.

The objective is not merely encryption.

The objective is contextual trust under adversarial conditions.

---

## Appendix A — Example Unlock Flow

```text
System Boot
    │
    ▼
Planned Reboot Declaration Present?
    │
    ├── YES → Increase Trust Weight
    └── NO
    │
    ▼
Anchor Discovery
    │
    ▼
Relay Continuity Validation
    │
    ▼
Sentry Threat Evaluation
    │
    ▼
Threat Indicators Present?
    │
    ├── YES → LOCKDOWN
    └── NO
    │
    ▼
Human Authorization Available?
    │
    ├── YES → Increase Trust Weight
    └── NO
    │
    ▼
Aggregate Trust Evaluation
    │
    ├── Below Threshold → DENY
    └── Above Threshold
    │
    ▼
Custodian Releases Ephemeral Unlock Authority
    │
    ▼
ZFS Pools Decrypt
```

---

## Appendix B — Example Hardware

### Core Infrastructure
- TrueNAS SCALE
- NixOS
- ZFS
- WireGuard
- UPS systems

### Anchors
- ESP32-S3
- ATECC608 secure elements
- concealed embedded devices
- PoE microcontrollers

### Relays
- Raspberry Pi Zero 2 W
- GL.iNet micro routers
- embedded WireGuard nodes

---

## Appendix C — Example Security Principles

| Principle | Description |
|---|---|
| Fail Closed | Default deny under uncertainty |
| Distributed Trust | No single authority |
| Context Awareness | Environment matters |
| Continuity Validation | Expected operational state matters |
| Sovereign Operation | Minimized third-party dependence |
| Conditional Authorization | Unlock decisions are contextual |
| Rapid Key Destruction | Minimize live compromise exposure |

---

# SovrIT SANCTUM

## Sovereign Attestation Network for Conditional Trust & Unlock Management

> "Encryption protects data.
> SANCTUM protects trust."
