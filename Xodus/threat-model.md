# Xodus Threat Model

## 1. Scope and Assumptions

This threat model applies to **Xodus operating in local or offline-capable
environments**, using a custom USB hardware device and cross-platform companion
applications for secure file sharing and media streaming.

### In Scope
- Local network communication (LAN / ad-hoc networks)
- Device pairing and trust establishment
- File transfer and media streaming workflows
- User-controlled hardware (Xodus USB dongle)
- Desktop and mobile companion applications

### Out of Scope
- Internet-facing deployments
- Anonymous or public sharing scenarios
- Large-scale multi-tenant environments
- Adversarial nation-state threat models

Xodus is designed for **personal, studio, and small trusted-group use** rather
than hostile open networks.

---

## 2. Assets to Protect

### Primary Assets
- Files shared through Xodus
- Media streams transmitted between devices
- Encryption keys and pairing credentials
- Trust relationships between paired devices

### Secondary Assets
- Metadata about transfers (timestamps, device identity)
- Local configuration and trusted-device lists
- Integrity of the Xodus USB hardware

---

## 3. Threat Actors

### A. Curious or Malicious Local Network Participant
A guest or nearby device connected to the same network attempting to:
- intercept traffic
- access shared files without authorization
- impersonate a trusted device

### B. Compromised Paired Device
A device that was legitimately paired but later compromised by malware.

### C. Opportunistic Attacker on Shared Infrastructure
An attacker on poorly secured or shared Wi-Fi attempting passive or active
network attacks (eavesdropping, spoofing).

### D. Accidental Insider
A legitimate user who unintentionally misconfigures sharing or pairing options.

---

## 4. Key Threats

### T1: Unauthorized Access to Files or Streams
An unpaired or malicious device attempts to access shared content.

**Impact:** Data exposure, privacy violation  
**Likelihood:** Medium on shared networks

---

### T2: Eavesdropping on Local Network Traffic
An attacker captures unencrypted traffic to view or manipulate content.

**Impact:** Confidentiality and integrity loss  
**Likelihood:** Medium if encryption is misconfigured

---

### T3: Device Impersonation or Spoofing
A rogue device attempts to pose as a trusted peer.

**Impact:** Unauthorized access or data injection  
**Likelihood:** Low–Medium depending on pairing strength

---

### T4: Compromise of a Trusted Device
A previously trusted device becomes compromised and abuses its access.

**Impact:** High (trusted channel misuse)  
**Likelihood:** Low–Medium (outside Xodus control)

---

### T5: Hardware Loss or Theft
The Xodus USB dongle is lost or stolen.

**Impact:** Potential exposure of trust material  
**Likelihood:** Low, but realistic

---

### T6: Privacy Leakage Through Metadata
Over-collection or long retention of logs reveals usage patterns.

**Impact:** Privacy erosion  
**Likelihood:** Medium if logging is excessive

---

## 5. Trust Boundaries

Xodus enforces clear trust boundaries:

1. **Between Paired and Unpaired Devices**  
   Only explicitly paired devices are allowed to exchange data.

2. **Between Local Network and External Networks**  
   Xodus does not expose services to the public internet by default.

3. **Between Hardware and Host Systems**  
   Sensitive trust operations are anchored to the Xodus USB device.

4. **Between User Intent and Automation**  
   File sharing and streaming require explicit user action.

---

## 6. Mitigation Strategies

### Encryption
- All file transfers and streams are encrypted in transit
- Session-based keys are preferred over long-lived secrets

### Secure Pairing
- QR-based pairing reduces manual key handling
- Pairing requires physical proximity and user confirmation

### Access Control
- Default-deny model for unpaired devices
- Allowlisting of trusted devices
- No anonymous access modes

### Minimal Data Retention
- No permanent storage of streamed media on receiving devices
- Logs kept minimal, local, and user-controlled

### Hardware Safeguards
- Hardware-backed trust separation
- Ability to revoke or reset trust if hardware is lost

### User Warnings & Safe Defaults
- Clear warnings when operating on untrusted networks
- Safe-mode defaults when network conditions are uncertain

---

## 7. Residual Risk

Even with strong mitigations, some residual risk remains:
- A fully compromised trusted device can abuse access
- Users may operate Xodus on insecure shared networks
- Physical theft of hardware remains possible

Xodus mitigates these risks through **explicit trust, minimal exposure,
and user awareness**, rather than attempting to eliminate all risk.

---

## 8. Security Design Philosophy

Xodus follows a **defensive, least-privilege security philosophy**:
- Prefer explicit trust over implicit discovery
- Reduce attack surface rather than add features
- Make secure behavior the default
- Design for human usability to reduce error

The goal is not to provide maximum functionality, but to provide
**safe, understandable, and privacy-respecting file sharing**.

---

## 9. Summary

Xodus is designed for secure local use cases where privacy, control,
and simplicity are valued over scale or convenience.

This threat model reflects a **realistic, applied security approach**,
acknowledging both technical threats and human factors while keeping
the system defensible and usable.

---

**End of Threat Model**
