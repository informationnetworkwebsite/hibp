# Hyperlocal Intent Broadcast Protocol (HIBP) — Specification Directory

### Open Standard • Versioned Specification • Public Registries

The **Hyperlocal Intent Broadcast Protocol (HIBP)** is an open, lightweight communication standard for broadcasting short‑range, privacy‑preserving intent signals using Bluetooth Low Energy (BLE), Wi‑Fi LAN multicast, and other local transports.

HIBP enables devices to share hyperlocal human‑intent metadata across six primary domains:

- **Commerce**  
- **Community & Social**  
- **Real Estate**  
- **Lost & Found**  
- **Environmental & Ambient**  
- **Infrastructure & System**

This directory contains the **official versioned specifications**, **registries**, and **reference documentation** for HIBP‑v1.

---

## 📘 Current Version

### **HIBP‑v1 (Stable)**  
The first public version of the protocol.

- 21‑byte core message format  
- Domain‑based Intent Code Registry  
- Real Estate domain (new in v1)  
- Device Type Registry  
- Transport requirements (BLE, Wi‑Fi LAN)  
- Security & privacy model  
- Optional metadata extensions  
- Reserved ranges for vendor‑specific and experimental use  

📄 **Full Specification:**  
[`hibp-v1.md`](hibp-v1.md)

---

## 📁 Specification Structure

```
spec/
├── README.md
├── hibp-v1.md
│
├── registry-intents.md
├── registry-device-types.md
├── registry-transports.md
├── registry-security.md
├── registry-metadata.md
├── registry-nodes.md
├── registry-events.md
├── registry-errors.md
└── registry-roles.md
```

---

## 📚 Registries Overview

HIBP maintains several open registries that define the protocol’s extensible components:

- **Intent Codes** — 1‑byte codes describing the meaning of a broadcast  
- **Device Types** — identifiers for broadcasting and receiving devices  
- **Transport Extensions** — BLE, Wi‑Fi LAN, and future transport definitions  
- **Metadata Fields** — optional structured metadata for extended use cases  
- **Security Registry** — privacy, encryption, and trust‑model parameters  
- **Node Registry** — NCN (Neighborhood Communication Node) roles and capabilities  
- **Events Registry** — standardized event categories  
- **Error Registry** — protocol‑level error codes  
- **Roles Registry** — protocol roles for devices and nodes  

All registries are versioned and may expand without requiring a new protocol version.

---

## 🧩 Versioning Policy

- Each protocol version is defined in its own Markdown file.  
- Versions are strictly incremental (`v1`, `v2`, `v3`, …).  
- Breaking changes require a major version increment.  
- Registries may expand without requiring a new protocol version.  
- Reserved ranges MUST NOT be used without explicit assignment.  

---

## 🤝 Contributing

HIBP is an open standard. Contributions are welcome.

See:  
[`../CONTRIBUTING.md`](../CONTRIBUTING.md)

---

## 📄 License

This project is licensed under the **Apache License 2.0**.  
See:  
[`../LICENSE`](../LICENSE)

---

## 🔗 Related Resources

- **GitHub Repository**  
  https://github.com/informationnetworkwebsite/hibp  

- **Developer Documentation (GitHub Pages)**  
  https://informationnetworkwebsite.github.io/hibp  

- **HIBP Definition Page**  
  https://www.informationnetworkwebsite.com/definition/hyperlocal-intent-broadcast-protocol/

- **HIBP Whitepaper**  
  https://www.informationnetworkwebsite.com/protocols/hyperlocal-intent-broadcast-protocol/whitepaper/

- **Information Network Website**  
  https://www.informationnetworkwebsite.com
