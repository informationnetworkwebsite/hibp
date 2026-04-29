# Hyperlocal Intent Broadcast Protocol (HIBP)
### Version 1.0 — Specification Document  
### File: `/spec/hibp-v1.md`

---

## Status of This Document

This document defines **HIBP‑v1**, the first stable version of the Hyperlocal Intent Broadcast Protocol.  
It is maintained in the official HIBP GitHub repository and published under the **Apache License 2.0**.

Future versions will be published as separate versioned specification files (`hibp-v2.md`, `hibp-v3.md`, etc.).  
Registries may expand without requiring a new protocol version.

---

## Table of Contents
1. [Introduction](#1-introduction)  
2. [Design Goals](#2-design-goals)  
3. [Terminology](#3-terminology)  
4. [HIBP‑v1 Core Message Format](#4-hibp-v1-core-message-format)  
   - [Field Layout](#41-field-layout-fixed-order)  
   - [Version Field](#42-version-field)  
   - [TTL Behavior](#43-ttl-behavior)  
   - [Ephemeral ID](#44-ephemeral-id)  
   - [Signature Fragment](#45-signature-fragment)  
5. [Extended Payload Format (Optional)](#5-extended-payload-format-optional)  
6. [HIBP‑v1 Intent Code Registry](#6-hibp-v1-intent-code-registry)  
7. [Device Type Registry](#7-device-type-registry)  
8. [Security & Privacy Model](#8-security--privacy-model)  
9. [Transport Layer Requirements](#9-transport-layer-requirements)  
10. [Reference Implementation](#10-reference-implementation)  
11. [Versioning](#11-versioning)  
12. [Registry Governance](#12-registry-governance)  
13. [Acknowledgments](#13-acknowledgments)  
14. [License](#14-license)  
15. [Changelog](#15-changelog)

---

## 1. Introduction

The **Hyperlocal Intent Broadcast Protocol (HIBP)** is an open, lightweight communication protocol for broadcasting short‑range, privacy‑preserving **intent signals** using Bluetooth Low Energy (BLE), Wi‑Fi LAN multicast, and other local transports.

HIBP enables devices to share hyperlocal human‑intent metadata across five primary domains:

- **Commerce**  
- **Community & Social**  
- **Lost & Found**  
- **Environmental & Ambient**  
- **Infrastructure & System**

HIBP‑v1 is designed to be minimal, extensible, and compatible with existing hardware.

---

## 2. Design Goals

HIBP‑v1 is designed to be:

- **Hyperlocal** — short‑range by design  
- **Privacy‑preserving** — no identity, no tracking  
- **Lightweight** — 21‑byte core frame  
- **Open** — public specification and registries  
- **Extensible** — future‑proof code ranges  
- **Transport‑agnostic** — BLE, Wi‑Fi, LAN, etc.  
- **Backward‑compatible** — versioned from day one  

---

## 3. Terminology

- **Broadcaster** — device emitting HIBP signals  
- **Receiver** — device capable of detecting and parsing signals  
- **Gateway** — receiver that forwards normalized signals  
- **Intent Signal** — compact message describing human or device intent  
- **Extended Payload** — optional metadata associated with a core frame  
- **Ephemeral ID** — rotating pseudonymous identifier  
- **NCN (Neighborhood Communication Node)** — infrastructure node capable of relaying or interpreting HIBP signals  

---

## 4. HIBP‑v1 Core Message Format

HIBP‑v1 defines a compact, fixed‑length **21‑byte** binary frame suitable for BLE advertisements and other constrained transports.

### 4.1 Field Layout (Fixed Order)

| Field | Size | Description |
|-------|------|-------------|
| `version` | 1 byte | Protocol version (`0x01` for HIBP‑v1) |
| `intent_code` | 1 byte | 1‑byte code from Intent Registry |
| `device_type_code` | 1 byte | 1‑byte code from Device Type Registry |
| `ttl_seconds` | 2 bytes | Time‑to‑live (unsigned, big‑endian) |
| `ephemeral_id` | 8 bytes | Rotating pseudonymous identifier |
| `signature_fragment` | 8 bytes | Truncated MAC/signature |

**Total Size:** 21 bytes

---

### 4.2 Version Field

- MUST be `0x01` for HIBP‑v1  
- Future versions MUST increment this value  

---

### 4.3 TTL Behavior

Receivers MUST discard signals after `ttl_seconds` has elapsed from the time of receipt.

---

### 4.4 Ephemeral ID

- MUST rotate periodically (recommended: every 10–20 minutes)  
- MUST NOT encode identity or trackable information  
- MAY be derived from a device secret using a rotating key schedule  

---

### 4.5 Signature Fragment

- MUST be computed over all preceding fields  
- MUST be truncated to 8 bytes  
- MAY be verified locally or via backend  

---

## 5. Extended Payload Format (Optional)

Extended metadata MAY be transmitted using JSON over IP, BLE GATT, or other transports.

````markdown
### 5.1 JSON Structure Example

```json
{
  "version": "1",
  "ephemeral_id": "b7f3a9c2d18e44aa",
  "intent": "FOR_SALE",
  "device_type": "PHONE",
  "ttl_seconds": 3600,
  "metadata": {
    "title": "iPhone 12, 128GB",
    "price": 250,
    "currency": "USD",
    "condition": "good",
    "category": "electronics",
    "tags": ["iphone", "smartphone"],
    "description": "Unlocked, minor scratches."
  }
}
```

Receivers MUST associate extended payloads with core frames using the `ephemeral_id`.

---

## 6. HIBP‑v1 Intent Code Registry

HIBP uses a 1‑byte intent code (`0x00–0xFF`).  
Codes are grouped by functional domain.

### 6.1 Commerce (0x01–0x1F)

| Code | Name |
| --- | --- |
| `0x01` | FOR_SALE |
| `0x02` | FREE |
| `0x03` | TRADE |
| `0x04` | LOOKING_TO_BUY |
| `0x05` | SERVICE_AVAILABLE |
| `0x06` | SERVICE_REQUEST |
| `0x07` | RENTAL_AVAILABLE |
| `0x08` | RENTAL_WANTED |

Reserved: `0x10–0x1F`

### 6.2 Community & Social (0x20–0x3F)

| Code | Name |
| --- | --- |
| `0x20` | EVENT |
| `0x21` | POPUP |
| `0x22` | ALERT |
| `0x23` | REQUEST_HELP |
| `0x24` | OFFER_HELP |
| `0x25` | COMMUNITY_ANNOUNCEMENT |

Reserved: `0x30–0x3F`

### 6.3 Lost & Found (0x40–0x4F)

| Code | Name |
| --- | --- |
| `0x40` | LOST_ITEM |
| `0x41` | FOUND_ITEM |
| `0x42` | LOST_PET |
| `0x43` | FOUND_PET |
| `0x44` | LOST_DEVICE |

Reserved: `0x45–0x4F`

### 6.4 Environmental & Ambient (0x50–0x6F)

| Code | Name |
| --- | --- |
| `0x50` | NOISE_EVENT |
| `0x51` | TRAFFIC_EVENT |
| `0x52` | WEATHER_EVENT |
| `0x53` | POWER_OUTAGE |
| `0x54` | WATER_OUTAGE |
| `0x55` | NETWORK_OUTAGE |

Reserved: `0x60–0x6F`

### 6.5 Infrastructure & System (0x70–0x7F)

| Code | Name |
| --- | --- |
| `0x70` | NODE_BEACON |
| `0x71` | NODE_STATUS |
| `0x72` | NODE_CAPABILITY |
| `0x73` | NODE_RELAY_AVAILABLE |
| `0x74` | NODE_SYNC |

Reserved: `0x75–0x7F`

### 6.6 Reserved Ranges

- `0x80–0xAF` — Vendor‑specific  
- `0xB0–0xCF` — Experimental  
- `0xD0–0xEF` — Future HIBP versions  
- `0xF0–0xFF` — Internal reserved  

---

## 7. Device Type Registry

| Code | Name |
| --- | --- |
| `0x01` | PHONE |
| `0x02` | TABLET |
| `0x03` | LAPTOP |
| `0x10` | GENERIC_DEVICE |
| `0x20` | BEACON_ONLY |

Reserved: `0x21–0xFF`

---

## 8. Security & Privacy Model

### 8.1 Privacy Principles

- No identity in core frames  
- No persistent identifiers  
- Ephemeral IDs MUST rotate  
- Extended metadata MUST be optional  

### 8.2 Threat Model

HIBP defends against:

- passive observers  
- trivial spoofing  
- replay attacks (via TTL)  

HIBP does **not** defend against:

- long‑range tracking  
- global adversaries  
- correlation across multiple receivers  

### 8.3 Signature Fragment

- MUST be derived from a MAC or signature  
- MUST be truncated to 8 bytes  
- MAY be verified locally or via backend  

---

## 9. Transport Layer Requirements

### 9.1 BLE Advertisements

- Core frame MUST fit within advertisement payload  
- Devices SHOULD broadcast at low intervals  

### 9.2 Wi‑Fi LAN Multicast

- Core frame MAY be sent as binary UDP  
- Extended payload MAY be sent via HTTP/WebSocket  

### 9.3 Other Transports

HIBP MAY be extended to:

- NFC  
- QR activation  
- WebRTC  
- Mesh networks  

---

## 10. Reference Implementation

Reference implementations will be published in future SDKs.

These will include:

- A gateway (receiver + normalizer)  
- A broadcaster (BLE advertiser)  
- SDKs (JavaScript, Python, and others)  

All reference implementations MUST conform to this specification.

---

## 11. Versioning

- HIBP‑v1 uses `version = 0x01`  
- Future versions MUST increment the version byte  
- Receivers MUST ignore unknown versions  

---

## 12. Registry Governance

HIBP registries include:

- Intent Code Registry  
- Device Type Registry  
- Transport Extensions  

Requests for new codes MUST include:

- name  
- description  
- justification  
- proposed code range  

---

## 13. Acknowledgments

HIBP is part of the broader Information Network Website ecosystem, including:

- shOPtions (Hyperlocal Commerce Engine)  
- Neighborhood Compute Nodes  
- Ambient hyperlocal intelligence systems  

---

## 14. License

This specification is published under the **Apache License 2.0**.  
See: [`../LICENSE`](../LICENSE)

---

## 15. Changelog

### v1.0 — Initial Publication
- First stable version of the Hyperlocal Intent Broadcast Protocol (HIBP)  
- Includes 21‑byte core message format  
- Includes domain‑based intent registry  
- Includes device type registry  
- Includes transport requirements (BLE, Wi‑Fi LAN)  
- Includes security & privacy model  
- Includes optional extended payload format  
