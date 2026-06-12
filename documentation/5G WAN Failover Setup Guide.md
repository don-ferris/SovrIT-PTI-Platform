# 5G WAN Failover Setup Guide
## Complete Parts List, Wiring Diagram, Grounding Plan, Installation Procedure, Aiming Guide, and Band‑Locking Instructions

---

_This guide uses a Cradlepoint W1850 modem/router with a Panorama WMM4G‑6‑60‑05NJ 4x4 MIMO LPDA Antenna (both available on eBay at reasonable prices) for high bandwisth. Other antennas and 5G modems/routers could be used but at the time this guide was written, those two products seemed to offer the "best bang for the buck"._

# 1. Complete Parts List

| **Item** | **Qty** | **Approx. Price (each)** | **Description** |
|----------------------------------|---------|---------------------------|-----------------|
| [**Cradlepoint W1850 5G Router + Antenna S5A325A**](https://cradlepoint.com/product/endpoints/w1850-series/)** | 1 | [$76](https://ebay.io/m/PRQ9uk) | 5G modem/router CPE. |
| [**Panorama WMM4G‑6‑60‑05NJ Antenna**](https://panorama-antennas.com/wp-content/uploads/2022/11/Datasheet-WMM4G-6-60-5.pdf) | 1 | — | 4×4 MIMO directional 5G/LTE antenna with 4 × N‑Female ports. |
| **N‑Male → N‑Female Lightning Arrestor (50Ω, DC–3GHz)** | 4 | ~$7–$20 | Screws directly into antenna N‑Female port. No jumpers needed. |
| **LMR‑240 N‑Male → SMA‑Male Coax (20 ft)** | 4 | — | Main low‑loss coax runs from arrestors to W1850 SMA ports. |
| **802.3at PoE+ Injector (Gigabit, 48 V)** | 1 | — | Powers W1850 over Ethernet. |
| **Outdoor‑Rated Cat6 Ethernet Cable** | As needed | ~$15–30 | PoE injector → W1850 run (outside/under eave). |
| **Short Cat6 Patch Cable** | 1 | ~$5–8 | ER605 → PoE injector LAN IN. |
| **10 AWG Bare Copper Ground Wire (Outdoor Rated)** | 1 roll | ~$12–20 | Bonds arrestors, mast, and surge devices to ground rod. |
| **5/8" Acorn Ground Rod Clamp** | 1 | ~$6 | Clamps ground wire to ground rod. |
| **Self‑Amalgamating Weatherproofing Tape (e.g., 3M 2228)** | 1 | ~$8–12 | Seals all outdoor N‑connectors against moisture. |
| **UV‑Resistant Cable Clamps / Straps** | 1 pack | ~$6–10 | Strain relief and routing for coax and Ethernet. |
| **PoE Surge Protector (optional)** | 1 | ~$12–18 | Inline surge protection on Ethernet PoE run. |

---

# 2. Wiring Diagram (Graphical)

                [Panorama WMM4G-6-60-05NJ]
                 (4 × N-Female ports)
                           |
                           |  N-Male → N-Female Arrestor
                           v
               ┌───────────────────────────┐
               │  Lightning Arrestor       │
               │   (N-Male → N-Female)     │
               └───────────────────────────┘
                           |
                           |  20 ft LMR-240 N-Male → SMA-Male
                           v
                [Cradlepoint W1850 Modem]
                 (4 × SMA-Female ports)
                           |
                           |  PoE IN (RJ45)
                           v
                     [PoE Injector]
                 LAN OUT → W1850 PoE IN
                 LAN IN  ← ER605 WAN Port
                           |
                           v
                       [ER605 Router]

**Key difference:**  
The arrestor screws **directly into the antenna**, eliminating the need for short N‑Male jumpers.

---

# 3. Grounding Plan (Correct + Safe + Simple)

### 1. Mount arrestors directly to antenna or to a metal plate
- If the arrestor body has a ground lug, mount it to a metal plate.
- If not, the arrestor’s metal body still bonds through the plate.

### 2. Bond all arrestors together
- Use **10 AWG bare copper**.
- Keep runs short and straight.

### 3. Run a single 10 AWG wire to the ground rod
- Use a **5/8" acorn clamp**.
- Tighten firmly.

### 4. Bond the antenna mast (if metal)
- Use another 10 AWG wire.
- Same ground rod.

### 5. Optional: Bond PoE surge protector
- Connect its ground lug to the same rod.

### 6. Single-point grounding
- All grounds terminate at **one** ground rod.
- Avoid loops or multiple unbonded rods.

### 7. Weatherproofing
- Wrap all outdoor N‑connections with self‑amalgamating tape.
- Overwrap with UV electrical tape if desired.

---

# 4. Atomic Step-by-Step Installation Procedure

## 4.1 Pre‑Installation

1. Update W1850 firmware.
2. Gather all parts.
3. Plan antenna + W1850 locations.
4. Label all four LMR‑240 cables.
5. Verify PoE injector is 802.3at (PoE+).

---

## 4.2 Mounting the Antenna

6. Install antenna bracket.
7. Mount Panorama antenna.
8. Aim roughly toward tower.
9. Create drip loops.
10. Secure coax routing path with UV clamps.

---

## 4.3 Installing Arrestors (No Jumpers Needed)

11. Screw each **N‑Male → N‑Female arrestor** directly into each antenna N‑Female port.
12. Tighten gently with wrench (do not over‑torque).
13. Weatherproof the antenna/arrestor connection.

---

## 4.4 Connecting Coax to W1850

14. Connect each LMR‑240 N‑Male to the **N‑Female** side of each arrestor.
15. Route cables neatly to W1850.
16. Connect SMA‑Male ends to W1850 SMA‑Female ports.
17. Snug with SMA wrench (light torque).

---

## 4.5 Installing PoE and Ethernet

18. Mount W1850 under eave or in ventilated enclosure.
19. Connect **PoE injector LAN OUT → W1850 PoE IN**.
20. Connect **ER605 WAN → PoE injector LAN IN**.
21. Optional: Insert PoE surge protector near W1850.
22. Power on PoE injector.

---

## 4.6 Grounding

23. Bond all arrestors with 10 AWG copper.
24. Run ground wire to ground rod.
25. Clamp with acorn clamp.
26. Bond mast to same rod.
27. Verify continuity (optional multimeter).

---

## 4.7 Configuration and Testing

28. Log into W1850 UI.
29. Set Mas Móvil APN.
30. Enable 5G NR.
31. Band‑lock to n41 (optional).
32. Check RSRP/RSRQ/SINR.
33. Fine‑tune antenna aim.
34. Run speed tests.
35. Configure ER605 failover.
36. Verify thermal stability.

---

# 5. Aiming Instructions for Panorama WMM4G‑6‑60‑05NJ

1. Identify tower direction using map/app.
2. Set initial azimuth using compass.
3. Keep elevation level unless tower is very close.
4. Loosen hardware slightly for fine‑tuning.
5. Rotate antenna in 5–10° increments.
6. After each move, wait 30–60 seconds.
7. Optimize for:
   - **Highest SINR**
   - Strongest RSRP (less negative)
   - Best RSRQ
8. Tighten hardware fully.
9. Document final bearing.

---

# 6. Band‑Locking Instructions for Mas Móvil (n41 Focus)

1. Log into W1850 UI.
2. Open WAN/Cellular settings.
3. Set APN to Mas Móvil value (e.g., `internet`).
4. Ensure 5G NR is enabled.
5. Open **Advanced Radio Settings**.
6. Switch from Auto to Manual/Custom band selection.
7. Enable **NR Band n41**.
8. Optionally allow LTE fallback bands (B3, B7, B28).
9. Apply and reboot if required.
10. Verify:
    - Connection type: **5G NR**
    - Active band: **n41**
    - Signal metrics are healthy.
11. Run performance tests.

---

# 7. Ethernet Length Limits (PoE and Non‑PoE)

- **ER605 → PoE injector LAN IN:**  
  Standard Ethernet. Max **100 m (328 ft)**.

- **PoE injector LAN OUT → W1850:**  
  802.3at PoE+. Max **100 m (328 ft)**.

Your installation will be far below these limits.

---

# End of Document
