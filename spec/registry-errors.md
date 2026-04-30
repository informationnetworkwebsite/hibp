# HIBP Error Code Registry
### Version 1.0  
### File: `/spec/registry-errors.md`

This document defines the **official Error Code Registry** for the Hyperlocal Intent Broadcast Protocol (HIBP).  
Error codes provide a standardized way for broadcasters, receivers, gateways, and neighborhood compute nodes to report issues related to:

- malformed frames  
- invalid signatures  
- TTL violations  
- transport failures  
- metadata errors  
- relay/normalization issues  

Error codes are **not** transmitted in HIBP core frames.  
They are used internally by implementations, logs, diagnostics, and developer tooling.

---

## Table of Contents
1. [Overview](#overview)  
2. [Error Code Structure](#error-code-structure)  
3. [Broadcaster Errors (0x01–0x1F)](#broadcaster-errors-0x01-0x1f)  
4. [Receiver Errors (0x20–0x3F)](#receiver-errors-0x20-0x3f)  
5. [Gateway Errors (0x40–0x5F)](#gateway-errors-0x40-0x5f)  
6. [Node Errors (0x60–0x7F)](#node-errors-0x60-0x7f)  
7. [Metadata & Payload Errors (0x80–0x9F)](#metadata--payload-errors-0x80-0x9f)  
8. [Reserved Ranges](#reserved-ranges)  
9. [Requesting New Error Codes](#requesting-new-error-codes)  
10. [Version History](#version-history)

---

## Overview

HIBP error codes provide:

- consistent debugging across implementations  
- predictable behavior for gateways and nodes  
- standardized logs for developers  
- clear separation between broadcaster, receiver, gateway, and node errors  

Error codes are **1 byte** (`0x00–0xFF`) and grouped by functional domain.

---

## Error Code Structure

Each error entry includes:

- **Code** — 1‑byte hexadecimal value  
- **Name** — canonical identifier  
- **Description** — intended meaning  
- **Applies To** — broadcaster, receiver, gateway, node  

Error codes MUST NOT be transmitted in core frames.

---

## Broadcaster Errors (0x01–0x1F)

Errors related to devices generating HIBP frames.

| Code | Name | Description |
|------|------|-------------|
| `0x01` | ERR_INVALID_INTENT | Invalid or unassigned intent code |
| `0x02` | ERR_INVALID_DEVICE_TYPE | Invalid or unassigned device type code |
| `0x03` | ERR_INVALID_VERSION | Unsupported protocol version |
| `0x04` | ERR_EID_GENERATION_FAILED | Ephemeral ID could not be generated |
| `0x05` | ERR_SIGNATURE_FAILED | Signature fragment could not be computed |
| `0x06` | ERR_TTL_INVALID | TTL is zero or exceeds allowed maximum |
| `0x07` | ERR_FRAME_TOO_LARGE | Frame exceeds 21‑byte limit |
| `0x08` | ERR_TRANSPORT_FAILURE | Transport layer failed to broadcast |

Reserved: `0x10–0x1F`

---

## Receiver Errors (0x20–0x3F)

Errors related to devices receiving or parsing HIBP frames.

| Code | Name | Description |
|------|------|-------------|
| `0x20` | ERR_FRAME_MALFORMED | Frame does not match required structure |
| `0x21` | ERR_VERSION_UNSUPPORTED | Receiver does not support this version |
| `0x22` | ERR_INTENT_UNKNOWN | Intent code not recognized |
| `0x23` | ERR_DEVICE_TYPE_UNKNOWN | Device type not recognized |
| `0x24` | ERR_TTL_EXPIRED | Frame TTL has expired |
| `0x25` | ERR_SIGNATURE_INVALID | Signature fragment does not validate |
| `0x26` | ERR_EID_INVALID | Ephemeral ID is malformed |
| `0x27` | ERR_DUPLICATE_FRAME | Duplicate frame detected |

Reserved: `0x30–0x3F`

---

## Gateway Errors (0x40–0x5F)

Errors related to gateways that normalize, relay, or forward HIBP frames.

| Code | Name | Description |
|------|------|-------------|
| `0x40` | ERR_NORMALIZATION_FAILED | Gateway failed to normalize frame |
| `0x41` | ERR_FORWARDING_FAILED | Gateway failed to forward frame |
| `0x42` | ERR_RELAY_LOOP_DETECTED | Relay loop detected and prevented |
| `0x43` | ERR_RATE_LIMITED | Gateway rate‑limited incoming frames |
| `0x44` | ERR_TRANSPORT_UNAVAILABLE | Required transport not available |
| `0x45` | ERR_PAYLOAD_TOO_LARGE | Extended payload exceeds allowed size |
| `0x46` | ERR_PAYLOAD_INVALID | Extended payload is malformed |
| `0x47` | ERR_METADATA_INVALID | Metadata keys or values invalid |

Reserved: `0x50–0x5F`

---

## Node Errors (0x60–0x7F)

Errors related to Neighborhood Compute Nodes (NCNs).

| Code | Name | Description |
|------|------|-------------|
| `0x60` | ERR_NODE_CACHE_EXCEEDED | Node cache exceeded TTL × 2 limit |
| `0x61` | ERR_NODE_STORAGE_FORBIDDEN | Node attempted to store long‑term data |
| `0x62` | ERR_NODE_ANALYTICS_INVALID | Analytics module encountered invalid data |
| `0x63` | ERR_NODE_RELAY_FAILED | Node failed to relay frame |
| `0x64` | ERR_NODE_CAPABILITY_UNKNOWN | Node advertised unknown capability |
| `0x65` | ERR_NODE_EXTENSION_UNSUPPORTED | Node does not support required extension |
| `0x66` | ERR_NODE_PRIVACY_VIOLATION | Node attempted disallowed correlation |

Reserved: `0x70–0x7F`

---

## Metadata & Payload Errors (0x80–0x9F)

Errors related to extended payloads and metadata.

| Code | Name | Description |
|------|------|-------------|
| `0x80` | ERR_METADATA_MISSING | Required metadata key missing |
| `0x81` | ERR_METADATA_TYPE_INVALID | Metadata value has incorrect type |
| `0x82` | ERR_METADATA_RESERVED_KEY | Metadata uses reserved key prefix |
| `0x83` | ERR_METADATA_TOO_LARGE | Metadata exceeds allowed size |
| `0x84` | ERR_METADATA_UNSUPPORTED | Metadata key not recognized |
| `0x85` | ERR_PAYLOAD_ENCODING | Payload encoding invalid or unsupported |

Reserved: `0x90–0x9F`

---

## Reserved Ranges

| Range | Purpose |
|--------|----------|
| `0xA0–0xBF` | Vendor‑specific error codes |
| `0xC0–0xDF` | Experimental error codes |
| `0xE0–0xEF` | Future HIBP versions |
| `0xF0–0xFF` | Internal reserved |

Reserved ranges MUST NOT be used without explicit assignment.

---

## Requesting New Error Codes

To propose a new error code, submit an issue or pull request including:

- Proposed code  
- Name  
- Description  
- Applies to (broadcaster, receiver, gateway, node)  
- Example scenarios  
- Justification  

New codes MUST NOT conflict with existing assignments.

---

## Version History

### **HIBP‑v1 (Initial Release)**
- Defined broadcaster, receiver, gateway, and node error codes  
- Added metadata/payload error codes  
- Reserved future error code ranges  

---

End of document.
