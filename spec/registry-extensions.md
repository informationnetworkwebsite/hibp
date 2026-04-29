# HIBP Extension Registry
### Version 1.0  
### File: `/spec/registry-extensions.md`

This document defines the **official Extension Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
Extensions represent optional, non‑core capabilities that enhance or augment HIBP behavior without modifying the core 21‑byte frame or the primary registries (intent, device type, transport, security).

Extensions allow HIBP to evolve while keeping the base protocol lightweight and stable.

---

## Table of Contents
1. [Overview](#overview)  
2. [Extension Categories](#extension-categories)  
3. [Standard Extensions](#standard-extensions)  
4. [Metadata Extensions](#metadata-extensions)  
5. [Gateway Extensions](#gateway-extensions)  
6. [Node Extensions](#node-extensions)  
7. [Reserved Ranges](#reserved-ranges)  
8. [Requesting New Extensions](#requesting-new-extensions)  
9. [Version History](#version-history)

---

## Overview

HIBP extensions define optional behaviors or capabilities that:

- do **not** alter the core message format  
- do **not** introduce identity or tracking  
- may be implemented by broadcasters, receivers, gateways, or nodes  
- may define additional metadata, behaviors, or processing rules  

Extensions are identified by a **1‑byte extension ID** (`0x00–0xFF`).

HIBP‑v1 defines a minimal set of extensions and reserves ranges for future expansion.

---

## Extension Categories

Extensions fall into four broad categories:

1. **Standard Extensions**  
   - General protocol enhancements  
   - Optional behaviors  

2. **Metadata Extensions**  
   - Additional metadata fields for extended payloads  

3. **Gateway Extensions**  
   - Behaviors specific to HIBP gateways and relays  

4. **Node Extensions**  
   - Capabilities for neighborhood compute nodes  

Each category has its own reserved ranges.

---

## Standard Extensions

These extensions apply broadly across the protocol.

| Extension ID | Name | Description |
|--------------|------|-------------|
| `0x01` | EXT_TTL_HINT | Broadcaster provides a recommended TTL for downstream relays |
| `0x02` | EXT_PRIORITY_HINT | Broadcaster suggests relative priority (low/normal/high) |
| `0x03` | EXT_CATEGORY_HINT | Broadcaster provides a high‑level category tag for UI grouping |
| `0x04` | EXT_LANGUAGE_HINT | Broadcaster provides a language code for extended payloads |

These extensions are optional and MAY be ignored by receivers.

---

## Metadata Extensions

These extensions define optional metadata keys for extended payloads.

| Extension ID | Name | Description |
|--------------|------|-------------|
| `0x20` | META_PRICE | Standardized price field (numeric) |
| `0x21` | META_CURRENCY | ISO‑4217 currency code |
| `0x22` | META_CONDITION | Item condition (new/good/fair/poor) |
| `0x23` | META_CATEGORY | High‑level category (electronics, pets, tools, etc.) |
| `0x24` | META_TAGS | Array of user‑defined tags |
| `0x25` | META_DESCRIPTION | Human‑readable description text |

Metadata extensions MUST NOT include identity or precise location.

---

## Gateway Extensions

These extensions apply to HIBP gateways (devices that receive and forward signals).

| Extension ID | Name | Description |
|--------------|------|-------------|
| `0x40` | GATEWAY_NORMALIZE | Gateway normalizes frames into a canonical JSON format |
| `0x41` | GATEWAY_DEDUP | Gateway performs deduplication based on ephemeral ID |
| `0x42` | GATEWAY_RATE_LIMIT | Gateway applies rate‑limiting to repeated broadcasts |
| `0x43` | GATEWAY_FORWARD | Gateway forwards normalized frames to a local node |

Gateways MAY implement any subset of these extensions.

---

## Node Extensions

These extensions apply to **neighborhood compute nodes**, which may aggregate, analyze, or relay HIBP signals.

| Extension ID | Name | Description |
|--------------|------|-------------|
| `0x60` | NODE_AGGREGATE | Node aggregates multiple HIBP signals into summaries |
| `0x61` | NODE_CACHE | Node caches extended payloads for short periods |
| `0x62` | NODE_RELAY | Node relays HIBP frames across transports |
| `0x63` | NODE_ANALYTICS | Node performs local, privacy‑preserving analytics |

Node extensions MUST NOT store identity or long‑term history.

---

## Reserved Ranges

| Range | Purpose |
|--------|----------|
| `0x80–0xAF` | Vendor‑specific extensions |
| `0xB0–0xCF` | Experimental extensions |
| `0xD0–0xEF` | Future HIBP versions |
| `0xF0–0xFF` | Internal reserved |

Reserved ranges MUST NOT be used without explicit assignment.

---

## Requesting New Extensions

To propose a new extension, submit an issue or pull request including:

- Extension name  
- Proposed ID  
- Category (standard, metadata, gateway, node)  
- Description and justification  
- Example use cases  
- Security and privacy considerations  

New extensions MUST NOT conflict with existing assignments.

---

## Version History

### **HIBP‑v1 (Initial Release)**
- Established extension categories  
- Defined initial extension IDs  
- Reserved future expansion ranges  

---

End of document.
