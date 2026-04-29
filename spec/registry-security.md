# HIBP Security & Privacy Registry
### Version 1.0  
### File: `/spec/registry-security.md`

This document defines the **official Security & Privacy Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
It specifies the security primitives, privacy requirements, and anti‑spoofing mechanisms used in HIBP‑v1, along with reserved ranges for future enhancements.

HIBP is designed to be **privacy‑preserving by default**, with no identity, no tracking, and no persistent identifiers.

---

## Table of Contents
1. [Overview](#overview)  
2. [Security Principles](#security-principles)  
3. [Privacy Requirements](#privacy-requirements)  
4. [Ephemeral ID Requirements](#ephemeral-id-requirements)  
5. [Signature Fragment Requirements](#signature-fragment-requirements)  
6. [Replay Protection](#replay-protection)  
7. [Threat Model](#threat-model)  
8. [Security Extension Registry](#security-extension-registry)  
9. [Reserved Ranges](#reserved-ranges)  
10. [Requesting New Security Extensions](#requesting-new-security-extensions)  
11. [Version History](#version-history)

---

## Overview

HIBP security is built around three core ideas:

1. **Ephemeral identifiers** instead of persistent IDs  
2. **Truncated signatures** to prevent trivial spoofing  
3. **Short‑range, short‑lived broadcasts** to limit exposure  

HIBP does not attempt to provide end‑to‑end cryptographic identity.  
Instead, it focuses on **hyperlocal authenticity**, **anti‑spoofing**, and **privacy preservation**.

---

## Security Principles

HIBP‑v1 is governed by the following principles:

- **No identity** — core frames MUST NOT contain personal identifiers.  
- **No tracking** — ephemeral IDs MUST rotate frequently.  
- **Minimal metadata** — only essential fields are included in core frames.  
- **Local verification** — receivers MAY verify signature fragments locally.  
- **Defense‑in‑depth** — TTL, ephemeral IDs, and signatures work together.  
- **Open design** — all security mechanisms are publicly documented.  

---

## Privacy Requirements

HIBP‑v1 enforces strict privacy rules:

- Core frames MUST NOT include:
  - names  
  - phone numbers  
  - email addresses  
  - device serial numbers  
  - advertising IDs  
  - MAC addresses  
  - GPS coordinates  

- Extended payloads MAY include optional metadata, but:
  - MUST NOT include identity  
  - MUST NOT include precise location  
  - MUST NOT include persistent identifiers  

- Receivers MUST NOT attempt to correlate ephemeral IDs across rotation windows.

---

## Ephemeral ID Requirements

The `ephemeral_id` field is 8 bytes and MUST follow these rules:

- MUST rotate periodically (recommended: every 10–20 minutes).  
- MUST NOT be predictable across rotations.  
- MUST NOT encode identity or device‑unique information.  
- MAY be derived from:
  - a device secret  
  - a rotating key schedule  
  - a PRNG seeded with a non‑identifying value  

- Receivers MUST treat each ephemeral ID as independent.

---

## Signature Fragment Requirements

The `signature_fragment` field is 8 bytes and MUST:

- be derived from a MAC or signature over the preceding fields  
- be truncated to 8 bytes  
- prevent trivial spoofing  
- allow lightweight verification  

HIBP‑v1 does **not** mandate a specific algorithm, but recommended options include:

- HMAC‑SHA256 (truncated)  
- BLAKE2s (truncated)  
- SipHash‑based MAC  

Signature fragments MUST NOT be reversible or leak key material.

---

## Replay Protection

HIBP uses **TTL‑based replay protection**:

- Each frame includes a `ttl_seconds` field.  
- Receivers MUST discard frames after TTL expiration.  
- Gateways MUST NOT rebroadcast expired frames.  

TTL is the primary replay‑mitigation mechanism in HIBP‑v1.

---

## Threat Model

HIBP defends against:

- **passive observers**  
- **casual spoofing**  
- **simple replay attacks**  
- **non‑targeted scanning**  

HIBP does **not** defend against:

- global adversaries  
- long‑range correlation  
- multi‑receiver triangulation  
- state‑level surveillance  

HIBP is designed for **hyperlocal, low‑risk environments**, not global adversarial resistance.

---

## Security Extension Registry

HIBP reserves a range of security extension identifiers for future enhancements.

| Extension ID | Name | Description |
|--------------|------|-------------|
| `0x01` | SIG_SHA256_TRUNC | Truncated HMAC‑SHA256 signature fragment |
| `0x02` | SIG_BLAKE2S_TRUNC | Truncated BLAKE2s signature fragment |
| `0x03` | SIG_SIPHASH | SipHash‑based MAC |
| `0x10` | EID_ROTATION_FAST | Fast ephemeral ID rotation mode |
| `0x11` | EID_ROTATION_SLOW | Slow ephemeral ID rotation mode |

These extensions are optional and MAY be used by implementations.

---

## Reserved Ranges

| Range | Purpose |
|--------|----------|
| `0x20–0x3F` | Future signature algorithms |
| `0x40–0x5F` | Future ephemeral ID schemes |
| `0x60–0x7F` | Transport‑specific security extensions |
| `0x80–0xAF` | Vendor‑specific security extensions |
| `0xB0–0xCF` | Experimental security extensions |
| `0xD0–0xEF` | Future HIBP versions |
| `0xF0–0xFF` | Internal reserved |

Reserved ranges MUST NOT be used without explicit assignment.

---

## Requesting New Security Extensions

To propose a new security extension, submit an issue or pull request including:

- Extension name  
- Proposed ID  
- Description and justification  
- Security properties  
- Example use cases  
- Compatibility considerations  

New extensions MUST NOT conflict with existing assignments.

---

## Version History

### **HIBP‑v1 (Initial Release)**
- Defined core security and privacy requirements  
- Established ephemeral ID rules  
- Defined signature fragment requirements  
- Added TTL‑based replay protection  
- Created the Security Extension Registry  
- Reserved future extension ranges  

---

End of document.
