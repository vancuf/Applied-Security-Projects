# Xodus Architecture

## 1. Architectural Overview

Xodus is a **local-first, privacy-preserving file sharing and media streaming
system** built around **hardware-backed trust** and **explicit user-controlled
pairing**.

The architecture is intentionally minimal to:
- reduce attack surface
- avoid unnecessary network exposure
- maintain clear trust boundaries
- support safe use by non-technical users

Xodus is not designed as an internet service. All core functionality operates
within local or offline-capable environments.

---

## 2. Design Principles

### 2.1 Local-First Operation
Xodus operates entirely on local networks or direct device connections.
No internet connectivity is required for pairing, file sharing, or media
streaming.

### 2.2 Hardware-Anchored Trust
A custom **Xodus USB dongle** anchors trust and pairing operations, separating
sensitive security logic from general-purpose host systems.

### 2.3 Explicit Trust Establishment
Devices must be explicitly paired before any data exchange is allowed.
There is no implicit discovery-based trust.

### 2.4 Minimal Persistence
Xodus minimizes stored data to reduce exposure:
- no permanent storage of streamed media on receiving devices
- limited, local-only configuration storage
- optional, minimal logging

### 2.5 Human-Centered Security
Security workflows are designed to be visible, understandable, and reversible
to reduce user error.

---

## 3. System Components

### 3.1 Xodus USB Device

**Role**
- Acts as a portable, hardware-backed trust anchor
- Stores pairing credentials and trust material
- Enables consistent identity across host systems

**Security Properties**
- Isolated from general-purpose OS processes
- Supports revocation or reset if lost or compromised
- Reduces exposure of long-lived secrets

---

### 3.2 Desktop Application

**Role**
- Primary user interface for managing files and streams
- Initiates pairing and sharing actions
- Displays trust status and session activity

**Responsibilities**
- Enforce allowlist-based access controls
- Encrypt outbound transfers
- Require explicit user approval for sharing actions

---

### 3.3 Mobile Application

**Role**
- Receives files or streams media from trusted devices
- Acts as a controlled endpoint, not a permanent storage device

**Responsibilities**
- Verify pairing status before accepting data
- Avoid persistent storage of streamed content
- Display clear trust and session indicators

---

### 3.4 Local Communication Layer

**Role**
- Handles encrypted data exchange between paired devices
- Operates only on local network interfaces or direct connections

**Security Properties**
- Encrypted transport for all sessions
- Session-based keys with limited lifetime
- No exposed services beyond paired peers

---

## 4. Data Flow

### 4.1 Device Pairing Flow
1. User inserts Xodus USB device
2. Desktop application generates a pairing request
3. QR code is displayed for pairing
4. Mobile device scans QR code
5. Trust relationship is established and stored on the USB device
6. Paired devices are added to the local allowlist

---

### 4.2 Secure File Sharing Flow
1. User selects a file to share
2. User selects a trusted paired device
3. Encrypted session is established
4. File is transmitted securely
5. Session keys are destroyed after transfer

---

### 4.3 Media Streaming Flow
1. User initiates a media stream
2. Encrypted local session is established
3. Media is streamed in real time
4. Receiving device does not permanently store content
5. Stream ends and session is terminated

---

## 5. Trust Boundaries

Xodus enforces the following trust boundaries:

- **Unpaired vs Paired Devices**  
  Only explicitly paired devices may communicate.

- **Local Network vs External Networks**  
  Xodus does not expose services to the public internet.

- **Hardware vs Host OS**  
  Sensitive trust material is anchored to the USB device.

- **User Intent vs Automation**  
  No background sharing; all transfers require explicit action.

---

## 6. Security Controls Summary

| Control Area | Implementation |
|--------------|----------------|
| Encryption | All data encrypted in transit |
| Pairing | QR-based, user-initiated |
| Access Control | Allowlist, default-deny |
| Persistence | Minimal, local-only |
| Network Exposure | Local-only, no public ports |
| Revocation | Hardware reset and trust revocation |

---

## 7. Failure Modes & Safety

Xodus is designed to fail safely:
- If pairing fails, no communication occurs
- If trust status is unclear, sharing is blocked
- If hardware is removed, sessions terminate
- If network conditions are insecure, user warnings are shown

---

## 8. Limitations

- Not designed for high-latency or wide-area networks
- Requires physical access for pairing
- Not intended for anonymous or large-scale sharing
- Relies on user judgment for operating on shared networks

These limitations are intentional and aligned with the project's security goals.

---

## 9. Architectural Rationale

This architecture prioritizes:
- security over convenience
- clarity over complexity
- local control over cloud dependency

Xodus demonstrates how **hardware-backed trust and local-first design**
can provide secure, privacy-respecting file sharing without relying on
centralized services.

---

**End of Architecture Document**
