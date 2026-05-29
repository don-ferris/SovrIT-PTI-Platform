# SovrIT Telephony Architecture — Complete Summary & Everyday Playbook (U.S. Context)

## 1. Core Purpose
Mobile numbers in the United States are surveillance anchors. They tie your identity, location, social graph, and financial life into one trackable profile. SovrIT telephony solves this by **splitting your phone identity into compartments**, each with a specific purpose, so no single number becomes a universal tracking point.

---

## 2. The SovrIT Number Tiers

### Tier 0 — Carrier SIM (Hidden)
- **Purpose:** data only  
- **Never shared**  
- **Never used for SMS, WhatsApp, or signups**  
- **Never given to humans**  

This SIM is just your internet pipe.

---

### Tier 1 — Life Number (VoIP, Clean, Long‑Term)
- **Use for:** doctors, attorneys, schools, service providers, WhatsApp (U.S. default is often SMS/iMessage, but WhatsApp is still common), anyone who doesn’t require legal identity  
- **Never for:** banks, government, utilities tied to legal identity, SMS 2FA  

This number stays out of credit bureaus and people‑finder databases.

---

### Tier 1.5 — Sacrificial KYC Number (Banks + 2FA Only)
- **Use for:** banks, credit cards, government portals, utilities, airlines, insurance, anything requiring SMS 2FA  
- **Created via:** prepaid SIM (minimal/light KYC) → register → port to VoIP → retire SIM  
- **Note:** This number *will* be tied to your legal identity and address, but it’s isolated.  

---

### Tier 2 — Semi‑Burners (Medium‑Term)
- **Use for:** shopping, deliveries, contractors, marketplaces, online accounts you may want to abandon later  
- **Implemented via:** additional MySudo identities  

---

### Tier 3 — True Burners (Short‑Term / OTP‑Only)
- **Use for:** one‑off signups, restaurant reservations, short‑term rentals, high‑risk websites, OTP‑only flows  
- **Implemented via:** Cloaked, SMSpool, disposable eSIMs  

---

## 3. The Two Identity Graphs

### Graph A — Clean Human Identity (Tier 1)
- No KYC  
- No address  
- No credit header  
- No carrier logs  
- No public records  
- No people‑finder exposure  

### Graph B — Legal/KYC Identity (Tier 1.5)
- Banks  
- Government  
- Utilities  
- Airlines  
- Insurance  
- 2FA  

These two graphs **never touch**.

---

## 4. Everyday Life Scenarios (Procedural, Simple)

### Scenario 1 — Doctor’s Office Calls You
- **Use:** Tier 1 Life Number  
- **Steps:** Give them your Life Number → they call via MySudo → you answer normally.  

---

### Scenario 2 — Wife Calls the Vet
- **Use:** Tier 1 Life Number  
- **Steps:** Open “Our Phone” (MySudo) → tap Vet contact → call.  

---

### Scenario 3 — Bank Sends 2FA Code
- **Use:** Tier 1.5 Sacrificial Number  
- **Steps:** Bank sends SMS → you receive in VoIP app → enter code.  

---

### Scenario 4 — Utility Registration (Electric, Water, Internet)
- **Use:** Tier 1.5 Sacrificial Number  
- **Steps:** Provide sacrificial number → utility ties it to your address → never use elsewhere.  

---

### Scenario 5 — WhatsApp Setup (U.S. Context)
- **Use:** Tier 1 Life Number  
- **Steps:** Register WhatsApp with Life Number → all WhatsApp flows through this.  

---

### Scenario 6 — Contractor Visit
- **Use:** Tier 2 Semi‑Burner  
- **Steps:** Give “Contractor Sudo” → delete later if spam.  

---

### Scenario 7 — Food Delivery
- **Use:** Tier 2 Semi‑Burner  
- **Steps:** Use “Shopping/Delivery Sudo” → safe if leaked.  

---

### Scenario 8 — Online Account Signup
- **Use:** Tier 2 or Tier 3 depending on trust  
- **Steps:** Trusted site → Tier 2; risky site → Cloaked/SMSpool.  

---

### Scenario 9 — Airbnb Rental
- **Use:** Tier 2 Semi‑Burner  
- **Steps:** Give medium‑term Sudo → delete after trip.  

---

### Scenario 10 — Restaurant Reservation
- **Use:** Tier 3 True Burner  
- **Steps:** Generate Cloaked number → give to restaurant → delete after.  

---

### Scenario 11 — Wife Calls a Friend
- **Use:** Signal (preferred) or Tier 1 Life Number  
- **Steps:** If friend has Signal → use Signal; if not → use “Our Phone.”  

---

### Scenario 12 — New Service Provider
- **Use:** Tier 1 Life Number  
- **Steps:** Call via MySudo → save contact in Life Sudo.  

---

### Scenario 13 — App Requiring SMS Verification
- **Use:** Tier 1.5 Sacrificial Number  
- **Steps:** Enter sacrificial number → receive SMS → verify.  

---

### Scenario 14 — Travel Abroad
- **Use:** Tier 0 for data, Tier 1 for WhatsApp/calls, Tier 2 for bookings  
- **Steps:** Install travel eSIM → everything else unchanged.  

---

### Scenario 15 — Emergency Call
- **Use:** Native Phone App (Carrier SIM)  
- **Steps:** Tap built‑in Phone app → dial emergency services.  

---

## 5. Keeping It Simple

### For You
- Manage Tier 1.5, Tier 2, Tier 3.  
- Handle porting, Cloaked, SMSpool.  
- Maintain SovrIT telephony map.  

### For Your Wife
She only needs **two rules**:  
1. **If it’s someone we know → use Signal.**  
2. **If it’s a business → use “Our Phone” (MySudo Life Number).**

---

## 6. GDPR & Jurisdiction Map

### GDPR Protections
- **Transparency & Consent:** Providers must disclose data use.  
- **Data Minimization:** Only necessary data collected.  
- **Storage Limitation:** Data retention must be justified.  
- **User Rights:** Access, correction, deletion.  
- **Cross‑Border Transfers:** Must use legal safeguards.  

### Practical Benefits
- **EU VoIP/SIP numbers:** Stronger protection against resale/misuse.  
- **EU eSIMs:** Even abroad, provider must comply with GDPR.  
- **WhatsApp with EU number:** Meta must comply with GDPR transparency, though enforcement is imperfect.  

### Limits
- **Global services (WhatsApp, Google, Meta):** GDPR applies, but enforcement is uneven.  
- **KYC entities (banks, utilities):** Identity verification overrides anonymity.  
- **Jurisdiction conflicts:** Non‑EU hosting may weaken protections.  

---

### Jurisdiction Map

| **Number Type** | **U.S. Protections** | **EU Protections (GDPR)** |
|-----------------|-----------------------|---------------------------|
| Carrier SIM     | Weak, resale allowed  | Stronger, but still tied to KYC |
| VoIP Life Number| No legal safeguards   | GDPR limits resale, grants rights |
| Sacrificial KYC | Linked to ID/address  | Still linked, but GDPR restricts misuse |
| Semi‑Burners    | Disposable, no rights | GDPR applies if EU provider |
| True Burners    | Disposable, no rights | GDPR applies if EU provider |

---

## 7. Final Rule of Thumb
- **If an organization can legally verify your identity → give them the Tier 1.5 sacrificial number.**  
- **Everyone else → give them the Tier 1 Life Number.**  
- **Your wife only needs two rules: Signal for people, MySudo for businesses.**

---
