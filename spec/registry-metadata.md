# HIBP Metadata Registry
### Version 1.0  
### File: `/spec/registry-metadata.md`

This document defines the **official Metadata Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
Metadata keys are used exclusively in **extended payloads**, which provide optional, human‑readable context for a HIBP intent signal.

Metadata is **never included** in the 21‑byte core frame.  
Extended payloads are optional, transport‑agnostic, and MUST NOT contain identity or precise location.

---

## Table of Contents
1. [Overview](#overview)  
2. [Metadata Principles](#metadata-principles)  
3. [Metadata Key Structure](#metadata-key-structure)  
4. [Standard Metadata Keys](#standard-metadata-keys)  
5. [Commerce Metadata](#commerce-metadata)  
6. [Community Metadata](#community-metadata)  
7. [Lost & Found Metadata](#lost--found-metadata)  
8. [Environmental Metadata](#environmental-metadata)  
9. [Reserved Keys](#reserved-keys)  
10. [Requesting New Metadata Keys](#requesting-new-metadata-keys)  
11. [Version History](#version-history)

---

## Overview

Extended payload metadata provides additional context for HIBP signals, such as:

- item descriptions  
- price and currency  
- condition  
- category and tags  
- event details  
- lost/found item information  

Metadata keys are **standardized** to ensure interoperability across:

- broadcasters  
- receivers  
- gateways  
- neighborhood compute nodes  

---

## Metadata Principles

All metadata MUST follow these principles:

- **Optional** — extended payloads are never required  
- **Non‑identifying** — MUST NOT include personal identity  
- **Non‑tracking** — MUST NOT include persistent identifiers  
- **Human‑readable** — intended for UI display  
- **Transport‑agnostic** — usable across BLE GATT, Wi‑Fi, HTTP, etc.  
- **JSON‑friendly** — keys MUST be lowercase with underscores  

---

## Metadata Key Structure

Metadata keys MUST:

- be lowercase  
- use underscores (`snake_case`)  
- be descriptive but concise  
- avoid ambiguity  

Example:

```json
"metadata": {
  "title": "iPhone 12, 128GB",
  "price": 250,
  "currency": "USD",
  "condition": "good"
}

Standard Metadata Keys

These keys apply across all intent categories.

| Key | Type | Description |
| --- | --- | --- |
| ``title`` | string | Short human‑readable title |
| ``description`` | string | Longer human‑readable description |
| ``category`` | string | High‑level category (electronics, pets, tools, etc.) |
| ``tags`` | array | User‑defined tags |
| ``language`` | string | Optional language code (ISO‑639‑1) |

Commerce Metadata

These keys apply to commerce‑related intents (FOR_SALE, FREE, TRADE, etc.).

| Key | Type | Description |
| --- | --- | --- |
| ``price`` | number | Numeric price value |
| ``currency`` | string | ISO‑4217 currency code |
| ``condition`` | string | Item condition (new, good, fair, poor) |
| ``quantity`` | number | Quantity available |
| ``brand`` | string | Optional brand name |
| ``model`` | string | Optional model identifier |

Community Metadata

These keys apply to events, pop‑ups, and community announcements.

| Key | Type | Description |
| --- | --- | --- |
| ``event_start`` | string | ISO‑8601 start time |
| ``event_end`` | string | ISO‑8601 end time |
| ``event_type`` | string | Category of event (meetup, sale, workshop, etc.) |
| ``venue`` | string | Human‑readable venue name |
| ``host`` | string | Non‑identifying host label (e.g., “Community Garden Group”) |

Note:

Hosts MUST NOT include personal names or contact information.

Lost & Found Metadata

These keys apply to lost/found items, pets, and devices.

| Key | Type | Description |
| --- | --- | --- |
| ``item_type`` | string | Type of item (wallet, keys, phone, etc.) |
| ``color`` | string | Color description |
| ``brand`` | string | Optional brand |
| ``model`` | string | Optional model |
| ``pet_type`` | string | Dog, cat, bird, etc. |
| ``pet_breed`` | string | Optional breed |
| ``notes`` | string | Additional non‑identifying details |

Environmental Metadata

These keys apply to hyperlocal environmental signals.

| Key | Type | Description |
| --- | --- | --- |
| ``severity`` | string | low, medium, high |
| ``source`` | string | Human‑readable source (e.g., “construction”, “traffic”) |
| ``duration_estimate`` | string | Human‑readable estimate (“10 minutes”, “1 hour”) |

Reserved Keys

| Range | Purpose |
| --- | --- |
| ``meta_*`` | Future standardized metadata keys |
| ``vendor_*`` | Vendor‑specific metadata |
| ``exp_*`` | Experimental metadata |
| ``v2_*`` | Future HIBP versions |

Reserved keys MUST NOT be used without explicit assignment.


Requesting New Metadata Keys

To propose a new metadata key, submit an issue or pull request including:

Proposed key name

Data type

Description and justification

Example use cases

Privacy considerations

New keys MUST NOT conflict with existing assignments.


Version History

HIBP‑v1 (Initial Release)

Defined standard metadata keys

Added commerce, community, lost/found, and environmental metadata

Reserved future metadata ranges

End of document.
