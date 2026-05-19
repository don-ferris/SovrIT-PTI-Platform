# SovrIT Trust Hierarchy & Recovery Model
## Trust, Identity, Continuity, and Recovery in a Sovereign Digital Environment

### Foundational Trust & Recovery Document
### Part of the SovrIT PTI Ecosystem

---

# Purpose

SovrIT is designed to preserve digital sovereignty while minimizing the risk of permanent loss.

Unlike traditional systems that optimize almost exclusively for preventing unauthorized access, SovrIT intentionally balances:

- security
- continuity
- resiliency
- recoverability
- long-term human usability

The system recognizes an uncomfortable but important truth:

> A perfectly secure system that permanently locks out its rightful owners is a failed system.

SovrIT therefore prioritizes:

# recoverable sovereignty

Meaning:

> It is generally better for trusted individuals to eventually recover legitimate access than for a family’s digital life to become permanently inaccessible.

This philosophy shapes every part of the SovrIT trust hierarchy.

---

# Core Philosophy

SovrIT assumes:

- people age
- memory fades
- devices fail
- houses burn down
- relationships evolve
- credentials are lost
- emergencies happen
- death and incapacity must be planned for

Trust must therefore be:

- resilient
- distributed
- recoverable
- continuously reviewed
- human-centered

Rather than relying on a single password, device, or secret, SovrIT establishes trust through:

# multiple independent signals of legitimacy

This prevents catastrophic failure caused by the loss of any single trust factor.

---

# What Is Root Trust?

In SovrIT:

# root trust is not a password

and:

# root trust is not a device

Instead:

# root trust is continuity confidence

Meaning:

> sufficient independent evidence exists to reasonably conclude that a person or continuity authority should regain access.

This intentionally prioritizes:
- recoverability
- continuity
- family survivability
- long-term operational resilience

over irreversible lockout.

---

# Trust Hierarchy Overview

```text
ROOT TRUST
│
├── Human Continuity Trust
│
├── Possession Trust
│
├── Cryptographic Trust
│
├── Operational Trust
│
└── Supporting Trust Signals
```

Each layer contributes confidence rather than absolute authority.

No single failure should permanently destroy trust.

---

# 1. Human Continuity Trust

Human continuity trust represents trusted people and institutions that can help re-establish legitimacy.

Examples include:

- spouse or partner
- heirs
- legal executors
- attorneys
- designated continuity contacts
- trusted family members

These people are not assumed to possess unrestricted authority.

Instead, they act as:

# continuity validators

Examples:

- confirming death or incapacity
- participating in recovery workflows
- validating succession requests
- helping restore legitimate access

---

## Why This Exists

People are often more reliable than devices over long periods of time.

Devices fail.

Passwords are forgotten.

Memory changes.

Trusted relationships and legal processes frequently become more durable recovery mechanisms.

---

## Special Considerations

SovrIT explicitly recognizes:

- aging
- dementia
- Alzheimer’s disease
- concussion history
- cognitive decline
- grief
- stress

Recovery systems should therefore avoid depending heavily on memory-based authentication.

---

# 2. Possession Trust

Possession trust refers to physical or digital things already associated with a trusted identity.

Examples:

- security keys (WebAuthn/FIDO2)
- trusted devices
- enrolled phones
- laptops
- continuity recovery packages
- encrypted continuity vaults

These objects provide strong evidence of legitimacy.

However:

# no single possession should be catastrophic if lost

For example:

A house fire may destroy:

- phones
- laptops
- servers
- security keys

SovrIT therefore avoids treating any single possession as irreplaceable.

---

## Distributed Continuity Principle

Recovery materials should not be stored in only one place.

Example:

Bad:

```text
House
├── server
├── phone
├── recovery USB
└── security key
```

One disaster destroys everything.

Better:

```text
Primary residence
├── day-to-day credentials

Trusted continuity authority
├── continuity instructions

Attorney or executor
├── succession materials

Encrypted continuity vault
├── recovery materials
```

No single event destroys trust.

---

# 3. Cryptographic Trust

Cryptographic trust provides technical proof of legitimacy.

Examples include:

- certificates
- device identity
- cryptographic signatures
- WebAuthn credentials
- service identity
- encrypted continuity artifacts

Likely SovrIT technologies include:

- Step-CA
- Authentik
- WebAuthn
- sovereign PKI

---

## What Can Issue Identity?

SovrIT separates:

### Human identity

Managed through:

- Authentik
- WebAuthn enrollment
- continuity relationships

### Device and service identity

Managed through:

- Step-CA
- certificates
- cryptographic trust chains

Examples:

```text
Human
    ↓
Authentik identity
    ↓
WebAuthn credential
```

```text
Server / device
    ↓
Step-CA certificate
```

---

# 4. Operational Trust

Operational trust reflects behavioral evidence accumulated over time.

Examples include:

- known devices
- prior login history
- long-term usage patterns
- trusted mesh activity
- known device enrollment
- historical account behavior

Operational trust helps answer:

> “Does this recovery request look legitimate?”

Examples:

- device seen for years
- login from familiar geography
- normal continuity contact involvement

---

# 5. Supporting Trust Signals

Supporting trust signals assist recovery but should rarely act alone.

Examples:

- authentication interviews
- recovery prompts
- continuity questionnaires
- waiting periods
- delayed escalation
- handbook-guided recovery

These signals improve confidence.

They should not become sole gatekeepers.

---

## Authentication Interviews

SovrIT may optionally support:

# authentication interviews

However:

they are treated as:

# supporting evidence

rather than primary proof.

Questions must be:

- memorable
- difficult for outsiders to know
- reviewed periodically
- resilient to public information exposure

Examples should avoid:

- public facts
- social media knowledge
- genealogy data
- trivia easily guessed by relatives

Because memory changes over time, failure to answer perfectly should not permanently block recovery.

---

# Trust Restoration

SovrIT restores trust through:

# confidence accumulation

Rather than:

```text
one password
=
full access
```

SovrIT uses:

```text
multiple signals
=
increasing confidence
```

Examples of trust signals:

| Signal | Confidence |
|---|---|
| Trusted device | Medium |
| Security key | High |
| Continuity authority | High |
| Attorney confirmation | High |
| Continuity vault access | High |
| Authentication interview | Low |
| Prior behavior | Medium |
| Waiting period completion | Medium |

When confidence exceeds a threshold:

recovery proceeds.

---

# What Can Revoke Identity?

Identity may be revoked when trust is lost.

Examples:

- stolen device
- compromised credential
- divorce or relationship change
- changed inheritance plan
- executor replacement
- compromised system

Likely mechanisms:

### Human access

- Authentik
- WebAuthn revocation

### Device identity

- Step-CA certificate revocation

### Mesh access

- NetBird peer removal

Revocation should be:

- auditable
- reversible when appropriate
- documented
- reviewable

---

# Reversible Continuity Escalation

SovrIT avoids sudden, irreversible succession.

Instead it follows:

# reversible continuity escalation

Meaning:

> continuity actions are gradual, observable, interruptible, and reversible.

Example flow:

```text
Normal operation
        ↓
Long absence detected
        ↓
Continuity review begins
        ↓
Presence challenge issued
        ↓
Waiting period
        ↓
Limited continuity access
        ↓
Operational continuity
        ↓
Full succession
```

---

# Presence Challenge

Before succession proceeds:

SovrIT attempts a final verification.

Example:

```text
Unless we hear otherwise,
[Person] may be granted continuity access in 72 hours.
```

Possible actions:

- confirm presence
- delay escalation
- request emergency lock
- dispute succession

Notifications may occur through:

- SovrIT app
- ntfy
- email
- SMS
- Matrix
- trusted devices

Purpose:

# prevent false positive succession

while preserving recoverability.

---

# Continuity Stages

## Stage 0 — Normal Ownership

Owner has full control.

---

## Stage 1 — Continuity Review

No access transferred.

Signals reviewed.

Presence challenge issued.

---

## Stage 2 — Read-Only Continuity

Successor receives:

- handbook
- records inventory
- guidance
- documentation

No destructive privileges.

---

## Stage 3 — Operational Continuity

Successor may:

- maintain systems
- restore services
- continue operations
- preserve continuity

Actions remain auditable.

---

## Stage 4 — Full Succession

Authority fully transfers.

Ownership changes.

Recovery responsibilities shift.

---

# Annual Continuity Review

Trust decays over time.

Relationships change.

Health changes.

Memory changes.

SovrIT therefore treats trust as:

# living infrastructure

At least annually, SovrIT should review:

- spouse or partner status
- heirs
- continuity contacts
- attorney relationships
- executor assignments
- recovery materials
- continuity vault integrity
- authentication interview quality
- documentation accuracy
- inheritance assumptions
- cognitive accessibility

Questions may include:

> Can your family still recover access?

> Have trust relationships changed?

> Are continuity instructions still understandable?

> Would succession succeed if something happened tomorrow?

---

# Guiding Principle

SovrIT intentionally prioritizes:

# preventing permanent loss

over:

# perfect exclusion

while still maintaining strong safeguards against illegitimate access.

In practice this means:

> better to recover imperfectly than disappear permanently.

The goal is not absolute technical perfection.

The goal is:

# durable digital continuity.