# Hyperlocal Intent Broadcast Protocol (HIBP)

### Open Standard • Versioned Specification • Public Registries

The **Hyperlocal Intent Broadcast Protocol (HIBP)** is an open, lightweight communication standard for broadcasting short‑range, privacy‑preserving intent signals using Bluetooth Low Energy (BLE), Wi‑Fi LAN multicast, and other local transports.

HIBP enables devices to share hyperlocal human‑intent metadata—such as items for sale, lost items, free items, services, and local events—without accounts, logins, or centralized platforms.

This repository contains the **official versioned specifications**, **registries**, and **reference documentation** for HIBP.

---

## 📘 Current Version

### **HIBP‑v1 (Stable)**  
The first public version of the protocol.

- 21‑byte core message format  
- Intent Code Registry  
- Device Type Registry  
- Transport requirements (BLE, Wi‑Fi LAN)  
- Security & privacy model  
- Optional metadata extensions  

📄 **Specification:**  
[`/spec/hibp-v1.md`](hibp-v1.md)

---

## 📁 Repository Structure

hibp/
│
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
│
└── spec/
├── README.md
├── hibp-v1.md
├── registry-intents.md
├── registry-device-types.md
├── registry-transports.md
├── registry-security.md
├── registry-metadata.md
├── registry-nodes.md
├── registry-events.md
├── registry-errors.md
└── registry-roles.md


---

## 📚 Registries

HIBP maintains several open registries:

- Intent Codes  
- Device Types  
- Transport Extensions  
- Metadata Fields  
- NCN Roles  
- Events  
- Error Codes  
- Protocol Roles  

All registries are versioned and defined in the `/spec/` directory.

---

## 🧩 Versioning Policy

- Each protocol version is defined in its own Markdown file.  
- Versions are strictly incremental (`v1`, `v2`, `v3`, …).  
- Breaking changes require a major version increment.  
- Registries may expand without requiring a new protocol version.  

---

## 🤝 Contributing

HIBP is an open standard. Contributions are welcome.

Please see:  
[`CONTRIBUTING.md`](../CONTRIBUTING.md)

---

## 📄 License

This project is licensed under the **Apache License 2.0**.  
See:  
[`LICENSE`](../LICENSE)

---

## 🔗 Related Resources

- Protocol Overview  
- HIBP Definition Page  
- HIBP Whitepaper  
- HIBP SDKs (future)  
- Information Network Website

