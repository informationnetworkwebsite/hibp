# HIBP Transport Registry
### Version 1.0  
### File: `/spec/registry-transports.md`

This document defines the **official Transport Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
Transports describe the communication channels capable of carrying HIBP core frames and optional extended payloads.

HIBP is designed to be **transport‑agnostic**, allowing the protocol to operate across multiple short‑range and local‑network technologies.

This registry defines the transport classes recognized in HIBP‑v1 and reserves ranges for future expansion.

---

## Table of Contents
1. [Overview](#overview)  
2. [Registry Structure](#registry-structure)  
3. [Core Transports](#core-transports)  
   - [BLE Advertisements](#ble-advertisements)  
   - [Wi‑Fi LAN Multicast](#wi-fi-lan-multicast)  
4. [Optional Transports](#optional-transports)  
5. [Reserved Transports](#reserved-transports)  
6. [Transport Requirements](#transport-requirements)  
7. [Requesting New Transports](#requesting-new-transports)  
8. [Version History](#version-history)

---

## Overview

HIBP transports define **how** a HIBP core frame or extended payload is delivered.  
A transport may support:

- **core frames only** (e.g., BLE advertisements)  
- **extended payloads only** (e.g., HTTP)  
- **both**  

HIBP‑v1 defines two core transports:

1. **Bluetooth Low Energy (BLE) Advertisements**  
2. **Wi‑Fi LAN Multicast (UDP)**  

Additional transports are optional and may be standardized in future versions.

---

## Registry Structure

Each transport entry includes:

- **Name** — canonical identifier  
- **Transport Class** — broadcast, unicast, or hybrid  
- **Supports Core Frames** — yes/no  
- **Supports Extended Payloads** — yes/no  
- **Description** — intended usage and constraints  

---

## Core Transports

These transports are officially supported in HIBP‑v1 and MUST be implemented by compliant receivers.

---

### BLE Advertisements
**Transport Class:** Broadcast  
**Core Frames:** Yes  
**Extended Payloads:** No  

**Description:**  
BLE advertisements are the primary transport for HIBP core frames.  
The 21‑byte HIBP frame fits within the BLE advertisement payload, enabling:

- low power usage  
- short‑range hyperlocal communication  
- compatibility with mobile devices and IoT hardware  

BLE is the **reference transport** for HIBP‑v1.

---

### Wi‑Fi LAN Multicast
**Transport Class:** Broadcast (local network)  
**Core Frames:** Yes  
**Extended Payloads:** Yes  

**Description:**  
Wi‑Fi LAN multicast allows devices on the same local network to broadcast HIBP frames using UDP.  
Extended payloads may be delivered via:

- HTTP  
- WebSocket  
- local REST endpoints  

This transport is useful for:

- neighborhood compute nodes  
- home networks  
- local gateways  

---

## Optional Transports

These transports are not required for HIBP‑v1 but MAY be implemented.

---

### NFC (Near‑Field Communication)
**Transport Class:** Proximity  
**Core Frames:** Yes  
**Extended Payloads:** Yes  

Used for tap‑to‑broadcast or tap‑to‑retrieve scenarios.

---

### QR Activation
**Transport Class:** Visual / Out‑of‑band  
**Core Frames:** No  
**Extended Payloads:** Yes  

QR codes may encode:

- extended payload URLs  
- ephemeral IDs  
- intent metadata  

---

### WebRTC Data Channels
**Transport Class:** Peer‑to‑peer  
**Core Frames:** Yes  
**Extended Payloads:** Yes  

Useful for:

- device‑to‑device relays  
- mesh‑style communication  

---

### Mesh Networking (Experimental)
**Transport Class:** Multi‑hop broadcast  
**Core Frames:** Yes  
**Extended Payloads:** Yes  

Reserved for future HIBP versions.

---

## Reserved Transports

| Transport Class | Purpose |
|-----------------|----------|
| **Cellular Broadcast** | Reserved for future hyperlocal carrier‑level signaling |
| **UWB (Ultra‑Wideband)** | Reserved for high‑precision hyperlocal use cases |
| **LoRa / LPWAN** | Reserved for long‑range, low‑bandwidth extensions |
| **Satellite Local Beam** | Reserved for future experimental use |

Reserved transports MUST NOT be used without explicit assignment.

---

## Transport Requirements

All transports MUST:

- preserve the integrity of the 21‑byte core frame  
- deliver frames within the TTL window  
- avoid embedding identity or tracking metadata  
- support ephemeral ID rotation  

Transports SHOULD:

- minimize power consumption  
- minimize bandwidth usage  
- avoid requiring centralized infrastructure  

---

## Requesting New Transports

To propose a new transport, submit an issue or pull request including:

- Transport name  
- Transport class  
- Whether it supports core frames, extended payloads, or both  
- Technical justification  
- Example use cases  
- Security considerations  

New transports MUST NOT conflict with reserved categories.

---

## Version History

### **HIBP‑v1 (Initial Release)**
- Defined BLE Advertisements as the primary transport  
- Added Wi‑Fi LAN Multicast as a secondary core transport  
- Established optional transport categories  
- Reserved future transport classes  

---

End of document.
