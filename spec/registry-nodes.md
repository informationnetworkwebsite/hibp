# HIBP Neighborhood Compute Node Registry
### Version 1.0  
### File: `/spec/registry-nodes.md`

This document defines the **official Neighborhood Compute Node Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
Neighborhood Compute Nodes (NCNs) are optional components that receive, normalize, aggregate, analyze, and relay HIBP signals within a hyperlocal environment.

NCNs extend the capabilities of HIBP without altering the core protocol.  
They enable richer hyperlocal intelligence while preserving privacy and decentralization.

---

## Table of Contents
1. [Overview](#overview)  
2. [Node Principles](#node-principles)  
3. [Node Capability Structure](#node-capability-structure)  
4. [Core Node Capabilities](#core-node-capabilities)  
5. [Aggregation Capabilities](#aggregation-capabilities)  
6. [Relay & Transport Capabilities](#relay--transport-capabilities)  
7. [Analytics Capabilities](#analytics-capabilities)  
8. [Storage & Caching Rules](#storage--caching-rules)  
9. [Reserved Capability Ranges](#reserved-capability-ranges)  
10. [Requesting New Node Capabilities](#requesting-new-node-capabilities)  
11. [Version History](#version-history)

---

## Overview

Neighborhood Compute Nodes (NCNs) are **local, privacy‑preserving compute units** that enhance HIBP functionality by:

- receiving and normalizing HIBP frames  
- aggregating hyperlocal signals  
- performing short‑term caching  
- relaying frames across transports  
- enabling local analytics without identity or tracking  

NCNs may be implemented on:

- home routers  
- Raspberry Pi‑class devices  
- local servers  
- community‑hosted nodes  
- dedicated hardware  

NCNs are **not required** for HIBP‑v1 but significantly expand its capabilities.

---

## Node Principles

All NCNs MUST follow these principles:

- **Local‑first** — processing occurs locally, not in the cloud  
- **Privacy‑preserving** — no identity, no long‑term storage  
- **Ephemeral** — data expires quickly  
- **Non‑tracking** — no correlation across ephemeral ID rotations  
- **Interoperable** — must follow HIBP registries and specs  
- **Extensible** — capabilities may be added via this registry  

---

## Node Capability Structure

Each capability entry includes:

- **Capability ID** — 1‑byte value (`0x00–0xFF`)  
- **Name** — canonical identifier  
- **Description** — intended behavior  
- **Privacy Requirements** — constraints and rules  

Capabilities are grouped by functional domain.

---

## Core Node Capabilities

These capabilities define the minimum useful behavior of a Neighborhood Compute Node.

| ID | Name | Description | Privacy Requirements |
|----|------|-------------|----------------------|
| `0x01` | NODE_RECEIVE | Node receives HIBP frames from any transport | MUST NOT store frames beyond TTL |
| `0x02` | NODE_NORMALIZE | Node converts frames into canonical JSON | MUST NOT add identifying metadata |
| `0x03` | NODE_VALIDATE | Node validates signature fragments | MUST NOT log validation failures |
| `0x04` | NODE_DEDUP | Node removes duplicate frames | MUST NOT store ephemeral IDs long‑term |

---

## Aggregation Capabilities

These capabilities allow NCNs to summarize hyperlocal activity.

| ID | Name | Description | Privacy Requirements |
|----|------|-------------|----------------------|
| `0x20` | NODE_AGGREGATE_INTENTS | Aggregates counts of intents by category | MUST aggregate only within TTL window |
| `0x21` | NODE_AGGREGATE_METADATA | Aggregates metadata fields (e.g., categories) | MUST NOT aggregate identity‑related fields |
| `0x22` | NODE_SUMMARY | Produces short summaries (e.g., “3 items for sale nearby”) | MUST NOT include raw ephemeral IDs |

---

## Relay & Transport Capabilities

These capabilities allow NCNs to relay HIBP frames across transports.

| ID | Name | Description | Privacy Requirements |
|----|------|-------------|----------------------|
| `0x40` | NODE_RELAY_BLE | Relays frames to BLE advertisements | MUST NOT increase TTL |
| `0x41` | NODE_RELAY_WIFI | Relays frames to Wi‑Fi LAN multicast | MUST NOT modify core frame |
| `0x42` | NODE_RELAY_HTTP | Exposes normalized frames via HTTP endpoint | MUST require local‑network access |
| `0x43` | NODE_RELAY_WEBSOCKET | Streams frames to local clients | MUST enforce rate limits |

---

## Analytics Capabilities

These capabilities enable **local, privacy‑preserving analytics**.

| ID | Name | Description | Privacy Requirements |
|----|------|-------------|----------------------|
| `0x60` | NODE_ANALYTICS_BASIC | Counts, trends, and simple statistics | MUST NOT store data beyond TTL |
| `0x61` | NODE_ANALYTICS_CATEGORY | Category‑level analytics | MUST NOT store raw metadata |
| `0x62` | NODE_ANOMALY_DETECTION | Detects unusual spikes (e.g., many alerts) | MUST NOT identify devices |
| `0x63` | NODE_PREDICTIVE_HINTS | Generates short‑term predictions | MUST NOT use long‑term history |

Analytics MUST be **local‑only** and MUST NOT transmit results externally.

---

## Storage & Caching Rules

NCNs MAY implement short‑term caching:

- Cache MUST NOT exceed **TTL × 2**  
- Cache MUST NOT store:
  - ephemeral IDs beyond TTL  
  - extended payloads beyond TTL  
  - any identifying metadata  

NCNs MUST NOT:

- build long‑term histories  
- correlate ephemeral IDs across rotations  
- store raw frames indefinitely  

---

## Reserved Capability Ranges

| Range | Purpose |
|--------|----------|
| `0x80–0xAF` | Vendor‑specific node capabilities |
| `0xB0–0xCF` | Experimental node capabilities |
| `0xD0–0xEF` | Future HIBP versions |
| `0xF0–0xFF` | Internal reserved |

Reserved ranges MUST NOT be used without explicit assignment.

---

## Requesting New Node Capabilities

To propose a new node capability, submit an issue or pull request including:

- Capability name  
- Proposed ID  
- Description and justification  
- Privacy requirements  
- Example use cases  
- Compatibility considerations  

New capabilities MUST NOT conflict with existing assignments.

---

## Version History

### **HIBP‑v1 (Initial Release)**
- Defined core NCN capabilities  
- Added aggregation, relay, and analytics capabilities  
- Established caching and storage rules  
- Reserved future capability ranges  

---

End of document.
