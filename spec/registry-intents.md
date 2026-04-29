# HIBP Intent Code Registry
### Version 1.0  
### File: `/spec/registry-intents.md`

This document defines the **official Intent Code Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
Intent codes are 1‑byte values (`0x00–0xFF`) used in the HIBP core message format to represent human or device intent.

The registry is grouped by functional domain and is designed to expand over time as new hyperlocal behaviors emerge.

---

## Table of Contents
1. [Overview](#overview)  
2. [Registry Structure](#registry-structure)  
3. [Commerce (0x01–0x1F)](#commerce-0x010x1f)  
4. [Community & Social (0x20–0x3F)](#community--social-0x200x3f)  
5. [Lost & Found (0x40–0x4F)](#lost--found-0x400x4f)  
6. [Environmental & Ambient (0x50–0x6F)](#environmental--ambient-0x500x6f)  
7. [Infrastructure & System (0x70–0x7F)](#infrastructure--system-0x700x7f)  
8. [Reserved Ranges](#reserved-ranges)  
9. [Requesting New Codes](#requesting-new-codes)  
10. [Version History](#version-history)

---

## Overview

HIBP intent codes represent **hyperlocal human‑intent signals**, such as:

- items for sale  
- free items  
- lost/found items  
- services  
- events  
- alerts  
- environmental conditions  
- system‑level broadcasts  

Each code is a single byte, allowing up to 256 possible values.

HIBP‑v1 defines the initial set of codes.  
Future versions may expand the registry while maintaining backward compatibility.

---

## Registry Structure

Each intent code entry includes:

- **Code** — 1‑byte hexadecimal value  
- **Name** — canonical identifier  
- **Description** — meaning and intended use  

Codes are grouped by domain to ensure long‑term scalability.

---

## Commerce (0x01–0x1F)

| Code | Name | Description |
|------|------|-------------|
| `0x01` | FOR_SALE | Item available for sale |
| `0x02` | FREE | Item is free to take |
| `0x03` | TRADE | Item available for trade or barter |
| `0x04` | LOOKING_TO_BUY | User seeking a specific item |
| `0x05` | SERVICE_AVAILABLE | User offering a service |
| `0x06` | SERVICE_REQUEST | User requesting a service |
| `0x07` | RENTAL_AVAILABLE | Item or property available for rent |
| `0x08` | RENTAL_WANTED | User seeking a rental |

**Reserved for future commerce expansion:** `0x10–0x1F`

---

## Community & Social (0x20–0x3F)

| Code | Name | Description |
|------|------|-------------|
| `0x20` | EVENT | Public event, gathering, or meeting |
| `0x21` | POPUP | Temporary booth, vendor, or pop‑up |
| `0x22` | ALERT | Non‑emergency alert (noise, traffic, etc.) |
| `0x23` | REQUEST_HELP | User needs assistance (non‑emergency) |
| `0x24` | OFFER_HELP | User offering assistance |
| `0x25` | COMMUNITY_ANNOUNCEMENT | General neighborhood broadcast |

**Reserved for future community expansion:** `0x30–0x3F`

---

## Lost & Found (0x40–0x4F)

| Code | Name | Description |
|------|------|-------------|
| `0x40` | LOST_ITEM | User lost an item |
| `0x41` | FOUND_ITEM | User found an item |
| `0x42` | LOST_PET | Lost dog, cat, or other pet |
| `0x43` | FOUND_PET | Found dog, cat, or other pet |
| `0x44` | LOST_DEVICE | Lost phone, laptop, or other device |

**Reserved for future lost/found expansion:** `0x45–0x4F`

---

## Environmental & Ambient (0x50–0x6F)

| Code | Name | Description |
|------|------|-------------|
| `0x50` | NOISE_EVENT | Loud noise, construction, or disturbance |
| `0x51` | TRAFFIC_EVENT | Local traffic congestion |
| `0x52` | WEATHER_EVENT | Hyperlocal weather anomaly |
| `0x53` | POWER_OUTAGE | Localized power outage |
| `0x54` | WATER_OUTAGE | Localized water disruption |
| `0x55` | NETWORK_OUTAGE | Localized internet outage |

**Reserved for future ambient expansion:** `0x60–0x6F`

---

## Infrastructure & System (0x70–0x7F)

| Code | Name | Description |
|------|------|-------------|
| `0x70` | NODE_BEACON | Node announcing presence |
| `0x71` | NODE_STATUS | Node health/status broadcast |
| `0x72` | NODE_CAPABILITY | Node advertises capabilities |
| `0x73` | NODE_RELAY_AVAILABLE | Node can relay HIBP packets |
| `0x74` | NODE_SYNC | Sync request/response |

**Reserved for future infrastructure expansion:** `0x75–0x7F`

---

## Reserved Ranges

| Range | Purpose |
|--------|----------|
| `0x80–0xAF` | Vendor‑specific intents |
| `0xB0–0xCF` | Experimental intents |
| `0xD0–0xEF` | Future HIBP versions |
| `0xF0–0xFF` | Internal reserved |

Reserved ranges MUST NOT be used without explicit assignment.

---

## Requesting New Codes

To request a new intent code, submit an issue or pull request including:

- Proposed name  
- Proposed code (or range)  
- Description and justification  
- Domain (commerce, community, etc.)  
- Example use cases  

New codes MUST NOT conflict with existing assignments.

---

## Version History

### **HIBP‑v1 (Initial Release)**
- Established core intent categories  
- Defined initial 1‑byte code assignments  
- Reserved future expansion ranges  

---

End of document.
