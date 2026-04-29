# HIBP Event Registry
### Version 1.0  
### File: `/spec/registry-events.md`

This document defines the **official Event Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
Events represent a major category of hyperlocal intent signals and include public gatherings, pop‑ups, community activities, and temporary hyperlocal occurrences.

This registry standardizes:

- event categories  
- event‑specific metadata keys  
- event‑type behaviors  
- reserved ranges for future expansion  

---

## Table of Contents
1. [Overview](#overview)  
2. [Event Principles](#event-principles)  
3. [Event Category Structure](#event-category-structure)  
4. [Standard Event Categories](#standard-event-categories)  
5. [Event Metadata Keys](#event-metadata-keys)  
6. [Event Timing Rules](#event-timing-rules)  
7. [Event Severity Levels](#event-severity-levels)  
8. [Reserved Categories](#reserved-categories)  
9. [Requesting New Event Categories](#requesting-new-event-categories)  
10. [Version History](#version-history)

---

## Overview

Events are a core part of hyperlocal communication.  
HIBP events include:

- community gatherings  
- pop‑up vendors  
- yard sales  
- workshops  
- temporary disruptions  
- hyperlocal alerts  

Events are represented using:

- **intent codes** (e.g., `EVENT`, `POPUP`, `ALERT`)  
- **event categories** (defined in this registry)  
- **event metadata** (extended payload fields)  

This registry ensures interoperability across broadcasters, receivers, gateways, and neighborhood compute nodes.

---

## Event Principles

All HIBP events MUST follow these principles:

- **Hyperlocal** — events occur within a small physical radius  
- **Ephemeral** — events have a start and end time  
- **Non‑identifying** — no personal names or contact info  
- **Human‑readable** — metadata is designed for UI display  
- **Optional** — events may include extended metadata, but never require it  

---

## Event Category Structure

Each event category includes:

- **Category ID** — string identifier  
- **Name** — human‑readable label  
- **Description** — intended meaning  
- **Example Use Cases** — typical scenarios  

Event categories are **not** 1‑byte codes; they are metadata values used in extended payloads.

---

## Standard Event Categories

These categories apply to the `EVENT` (`0x20`) and `POPUP` (`0x21`) intent codes.

### Community Events

| Category ID | Name | Description |
|-------------|------|-------------|
| `community_meeting` | Community Meeting | Neighborhood meetings, HOA gatherings, planning groups |
| `workshop` | Workshop | Skill‑sharing, classes, DIY sessions |
| `volunteer_event` | Volunteer Event | Community cleanups, charity drives |
| `public_notice` | Public Notice | Announcements relevant to the neighborhood |

---

### Commerce‑Related Events

| Category ID | Name | Description |
|-------------|------|-------------|
| `yard_sale` | Yard Sale | Garage sales, stoop sales, moving sales |
| `popup_vendor` | Pop‑Up Vendor | Temporary vendor booths, food stands |
| `market` | Market | Farmers markets, flea markets |
| `giveaway` | Giveaway | Free items, community swaps |

---

### Social Events

| Category ID | Name | Description |
|-------------|------|-------------|
| `block_party` | Block Party | Neighborhood parties, celebrations |
| `meetup` | Meetup | Informal gatherings, interest groups |
| `kids_activity` | Kids Activity | Playgroups, children’s events |

---

### Disruption Events (Non‑Emergency)

These correspond to the `ALERT` (`0x22`) intent code.

| Category ID | Name | Description |
|-------------|------|-------------|
| `construction` | Construction | Temporary construction activity |
| `noise` | Noise | Loud noise, music, machinery |
| `traffic` | Traffic | Local traffic congestion |
| `utility_work` | Utility Work | Water, power, or network maintenance |

---

## Event Metadata Keys

These metadata keys apply specifically to events.

| Key | Type | Description |
|-----|------|-------------|
| `event_start` | string | ISO‑8601 start time |
| `event_end` | string | ISO‑8601 end time |
| `event_category` | string | Category ID from this registry |
| `venue` | string | Human‑readable venue name |
| `host` | string | Non‑identifying host label (e.g., “Community Garden Group”) |
| `cost` | string | Free, donation, or price description |
| `age_range` | string | Optional age suitability (e.g., “all ages”) |
| `notes` | string | Additional non‑identifying details |

**Important:**  
Hosts MUST NOT include personal names, phone numbers, or contact information.

---

## Event Timing Rules

- Events MUST include at least one of:
  - `event_start`
  - `event_end`

- If only `event_start` is provided:
  - Event is assumed to be short‑duration or ongoing.

- If only `event_end` is provided:
  - Event is assumed to be currently active.

- Events MUST NOT include:
  - GPS coordinates  
  - precise addresses  
  - personal contact info  

---

## Event Severity Levels

Severity applies primarily to disruption events.

| Severity | Meaning |
|----------|---------|
| `low` | Minor inconvenience |
| `medium` | Noticeable disruption |
| `high` | Significant temporary impact |

Severity MUST be human‑interpretable and MUST NOT imply emergency response.

---

## Reserved Categories

| Range | Purpose |
|--------|----------|
| `future_*` | Reserved for future HIBP versions |
| `vendor_*` | Vendor‑specific event categories |
| `exp_*` | Experimental categories |
| `v2_*` | Reserved for HIBP‑v2 |

Reserved categories MUST NOT be used without explicit assignment.

---

## Requesting New Event Categories

To propose a new event category, submit an issue or pull request including:

- Proposed category ID  
- Name  
- Description  
- Example use cases  
- Justification  
- Privacy considerations  

New categories MUST NOT conflict with existing assignments.

---

## Version History

### **HIBP‑v1 (Initial Release)**
- Defined community, commerce, social, and disruption event categories  
- Added event‑specific metadata keys  
- Established timing and severity rules  
- Reserved future category ranges  

---

End of document.
