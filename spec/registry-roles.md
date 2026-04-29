# HIBP Role Registry
### Version 1.0  
### File: `/spec/registry-roles.md`

This document defines the **official Role Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
Roles describe the functional responsibilities of devices and systems participating in the HIBP ecosystem.

HIBP defines four primary roles:

1. **Broadcaster**  
2. **Receiver**  
3. **Gateway**  
4. **Neighborhood Compute Node (NCN)**  

Each role has specific capabilities, constraints, and privacy requirements.

---

## Table of Contents
1. [Overview](#overview)  
2. [Role Principles](#role-principles)  
3. [Broadcaster](#broadcaster)  
4. [Receiver](#receiver)  
5. [Gateway](#gateway)  
6. [Neighborhood Compute Node (NCN)](#neighborhood-compute-node-ncn)  
7. [Role Interoperability](#role-interoperability)  
8. [Reserved Roles](#reserved-roles)  
9. [Requesting New Roles](#requesting-new-roles)  
10. [Version History](#version-history)

---

## Overview

Roles define **how a device participates** in the HIBP ecosystem.  
A single device MAY implement multiple roles simultaneously (e.g., a phone may be both a broadcaster and a receiver).

Roles are:

- **functional** — describing behavior, not identity  
- **interoperable** — designed to work together  
- **privacy‑preserving** — none may store identity or long‑term history  
- **extensible** — new roles may be added in future versions  

---

## Role Principles

All HIBP roles MUST follow these principles:

- **No identity** — roles MUST NOT introduce personal identifiers  
- **Ephemeral** — data MUST expire according to TTL rules  
- **Local‑first** — processing SHOULD occur locally whenever possible  
- **Interoperable** — roles MUST follow HIBP registries and specs  
- **Minimal** — roles SHOULD avoid unnecessary complexity  

---

## Broadcaster

The **Broadcaster** is any device that emits HIBP core frames.

### Responsibilities

- Generate valid 21‑byte HIBP frames  
- Rotate ephemeral IDs  
- Compute signature fragments  
- Broadcast via supported transports (BLE, Wi‑Fi, etc.)  
- Respect TTL limits  

### MUST

- Follow the HIBP core message format  
- Use valid intent and device type codes  
- Rotate ephemeral IDs frequently  
- Avoid embedding identity or tracking metadata  

### MUST NOT

- Broadcast personal information  
- Use persistent identifiers  
- Exceed the 21‑byte core frame limit  

### Typical Broadcasters

- Phones  
- Tablets  
- Laptops  
- IoT beacons  
- Dedicated HIBP hardware  

---

## Receiver

The **Receiver** is any device capable of detecting and parsing HIBP frames.

### Responsibilities

- Scan for HIBP frames  
- Validate structure and version  
- Enforce TTL expiration  
- Optionally verify signature fragments  
- Optionally display or forward normalized data  

### MUST

- Discard expired frames  
- Ignore unknown versions  
- Avoid correlating ephemeral IDs across rotations  

### MUST NOT

- Store raw frames beyond TTL  
- Attempt to identify broadcasters  
- Build long‑term histories  

### Typical Receivers

- Phones  
- Laptops  
- IoT hubs  
- Gateways  
- Neighborhood Compute Nodes  

---

## Gateway

A **Gateway** is a specialized receiver that normalizes, deduplicates, and optionally forwards HIBP frames.

Gateways sit between broadcasters and NCNs or local applications.

### Responsibilities

- Receive and normalize frames  
- Deduplicate based on ephemeral ID  
- Enforce TTL  
- Optionally forward frames to NCNs or local apps  
- Optionally expose HTTP/WebSocket endpoints  

### MUST

- Normalize frames into canonical JSON  
- Enforce TTL and deduplication  
- Avoid modifying core frame fields  

### MUST NOT

- Store frames beyond TTL × 2  
- Add identifying metadata  
- Relay expired frames  

### Typical Gateways

- Home routers  
- Raspberry Pi devices  
- Local servers  
- Community‑hosted nodes  

---

## Neighborhood Compute Node (NCN)

A **Neighborhood Compute Node** is a local, privacy‑preserving compute unit that enhances HIBP functionality.

NCNs are optional but powerful components of the ecosystem.

### Responsibilities

- Aggregate hyperlocal signals  
- Perform short‑term caching  
- Provide local analytics  
- Relay frames across transports  
- Support local applications  

### MUST

- Follow all NCN privacy rules  
- Avoid long‑term storage  
- Avoid identity or tracking  
- Respect TTL and ephemeral ID rotation  

### MUST NOT

- Build long‑term histories  
- Correlate ephemeral IDs across rotations  
- Export raw data externally  

### Typical NCNs

- Home servers  
- Community compute nodes  
- Local mesh nodes  
- Dedicated HIBP hardware  

---

## Role Interoperability

Roles are designed to interoperate:

| Broadcaster | Receiver | Gateway | NCN |
|-------------|----------|---------|-----|
| Emits frames | Parses frames | Normalizes & forwards | Aggregates & analyzes |
| No storage | TTL‑limited storage | TTL × 2 storage | TTL × 2 storage |
| No metadata | Optional metadata | Extended payload support | Extended payload support |

A single device MAY implement multiple roles (e.g., phone = broadcaster + receiver).

---

## Reserved Roles

HIBP reserves additional roles for future versions:

| Role ID | Name | Purpose |
|---------|------|---------|
| `future_relay` | Future Relay Role | Multi‑hop mesh relays |
| `future_directory` | Directory Role | Local ephemeral directory services |
| `future_agent` | Agent Role | Autonomous hyperlocal agents |

Reserved roles MUST NOT be used without explicit assignment.

---

## Requesting New Roles

To propose a new role, submit an issue or pull request including:

- Role name  
- Description  
- Responsibilities  
- Privacy requirements  
- Example use cases  
- Justification  

New roles MUST NOT conflict with existing assignments.

---

## Version History

### **HIBP‑v1 (Initial Release)**
- Defined Broadcaster, Receiver, Gateway, and NCN roles  
- Established interoperability rules  
- Reserved future role categories  

---

End of document.
