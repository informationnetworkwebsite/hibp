# HIBP Device Type Registry
### Version 1.0  
### File: `/spec/registry-device-types.md`

This document defines the **official Device Type Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
Device type codes are 1‑byte values (`0x00–0xFF`) used in the HIBP core message format to identify the general class of the broadcasting device.

The registry is intentionally minimal in HIBP‑v1 and is designed to expand as new device categories emerge.

---

## Table of Contents
1. [Overview](#overview)  
2. [Registry Structure](#registry-structure)  
3. [Device Types (0x01–0x20)](#device-types-0x010x20)  
4. [Reserved Ranges](#reserved-ranges)  
5. [Requesting New Device Types](#requesting-new-device-types)  
6. [Version History](#version-history)

---

## Overview

Device type codes provide a lightweight way for receivers and gateways to understand the **class of device** broadcasting a HIBP signal.

Examples include:

- phones  
- tablets  
- laptops  
- IoT devices  
- dedicated beacons  

Device type codes do **not** identify the manufacturer, model, or user.  
They exist solely to support:

- filtering  
- prioritization  
- analytics  
- extended payload interpretation  

---

## Registry Structure

Each device type entry includes:

- **Code** — 1‑byte hexadecimal value  
- **Name** — canonical identifier  
- **Description** — intended meaning and usage  

Codes are grouped into ranges to support long‑term scalability.

---

## Device Types (0x01–0x20)

| Code | Name | Description |
|------|------|-------------|
| `0x01` | PHONE | Mobile phone or smartphone |
| `0x02` | TABLET | Tablet device |
| `0x03` | LAPTOP | Laptop or notebook computer |
| `0x10` | GENERIC_DEVICE | Generic device type (fallback category) |
| `0x20` | BEACON_ONLY | Dedicated beacon device with no UI |

These codes represent the minimal set required for HIBP‑v1.

---

## Reserved Ranges

| Range | Purpose |
|--------|----------|
| `0x21–0x3F` | Future consumer device types |
| `0x40–0x5F` | IoT and sensor devices |
| `0x60–0x7F` | Infrastructure and node devices |
| `0x80–0xAF` | Vendor‑specific device types |
| `0xB0–0xCF` | Experimental device types |
| `0xD0–0xEF` | Future HIBP versions |
| `0xF0–0xFF` | Internal reserved |

Reserved ranges MUST NOT be used without explicit assignment.

---

## Requesting New Device Types

To request a new device type code, submit an issue or pull request including:

- Proposed name  
- Proposed code (or range)  
- Description and justification  
- Example use cases  
- Expected adoption or ecosystem impact  

New codes MUST NOT conflict with existing assignments.

---

## Version History

### **HIBP‑v1 (Initial Release)**
- Established core device type categories  
- Defined initial 1‑byte code assignments  
- Reserved future expansion ranges  

---

End of document.
