# Hyperlocal Intent Broadcast Protocol (HIBP)

Welcome to the developer documentation for the **Hyperlocal Intent Broadcast Protocol (HIBP)**.

HIBP is an open, lightweight, privacy‑preserving standard for broadcasting hyperlocal intent signals over Bluetooth Low Energy (BLE), Wi‑Fi LAN multicast, and other short‑range transports.

This documentation site provides:

- Protocol overview  
- Versioned specifications  
- Open registries  
- Implementation notes  
- Examples and SDKs (future)  

---

## 📘 Current Version

### **HIBP‑v1 (Stable)**  
The first public version of the protocol.

📄 **Full Specification:**  
[HIBP‑v1 Specification](../spec/hibp-v1.md)

---

## 📚 Registries

HIBP maintains several open registries that define the protocol’s extensible components:

- [Intent Code Registry](../spec/registry-intents.md)  
- [Device Type Registry](../spec/registry-device-types.md)  
- [Transport Registry](../spec/registry-transports.md)  
- [Metadata Registry](../spec/registry-metadata.md)  
- [Security Registry](../spec/registry-security.md)  
- [Node Registry](../spec/registry-nodes.md)  
- [Events Registry](../spec/registry-events.md)  
- [Error Registry](../spec/registry-errors.md)  
- [Roles Registry](../spec/registry-roles.md)  

All registries are versioned and may expand without requiring a new protocol version.

---

## 🧭 Domain Overview

HIBP‑v1 organizes intent codes into five primary domains:

- **Commerce (0x01–0x1F)** — buying, selling, trading, rentals  
- **Community & Social (0x20–0x3F)** — events, alerts, help requests  
- **Lost & Found (0x40–0x4F)** — lost items, found items, lost pets  
- **Environmental & Ambient (0x50–0x6F)** — noise, traffic, outages, weather  
- **Infrastructure & System (0x70–0x7F)** — node beacons, status, capabilities  

Reserved ranges support vendor‑specific, experimental, and future protocol versions.

---

## 🔗 Additional Resources

- **GitHub Repository**  
  https://github.com/informationnetworkwebsite/hibp  

- **Information Network Website**  
  https://www.informationnetworkwebsite.com  

- **HIBP Definition Page**  
  https://www.informationnetworkwebsite.com/definition/hyperlocal-intent-broadcast-protocol/

- **HIBP Whitepaper**  
  https://www.informationnetworkwebsite.com/protocols/hyperlocal-intent-broadcast-protocol/whitepaper/

- **HIBP SDKs** (future)

---

## 🛠 Implementation Notes

Implementation guidance, examples, and SDKs will be added as the ecosystem grows.  
Contributions are welcome — see the GitHub repository for details.
