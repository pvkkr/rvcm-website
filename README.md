# 🌿 RVCM – Remote Valve Control Mechanism
### IoT-Based Smart Irrigation System for Banana Farms

[![GitHub Pages](https://img.shields.io/badge/Live%20Site-GitHub%20Pages-2E7D32?style=flat&logo=github)](https://pvkkr.github.io/rvcm-website/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen)]()

> Control every irrigation valve across a 3-acre banana farm with a single SMS — no manual effort, ultra-low power, 3+ years on solar.

---

## 🌐 Live Website

👉 **[https://pvkkr.github.io/rvcm-website/](https://pvkkr.github.io/rvcm-website/)**

---

## 📄 Project Documents

| Document | Download |
|----------|----------|
| RVCM Project Report | [📥 Download PDF](https://github.com/pvkkr/rvcm-website/raw/main/rvcm.pdf) |
| Project Requirements | [📥 Download PDF](https://github.com/pvkkr/rvcm-website/raw/main/project_requires.pdf) |

---

## 📖 Overview

The **Remote Valve Control Mechanism (RVCM)** is a low-cost, low-power IoT solution designed for small to medium-scale agriculture. By combining **ESP32 microcontrollers**, **LoRa long-range wireless**, **GSM mobile connectivity**, and **intelligent power management**, this system enables a farmer to control all irrigation valves across a **3-acre banana farm** from their mobile phone.

The farm layout covers approximately **300m × 50m**. A single **Master Node** placed centrally communicates with **multiple Slave Nodes** distributed across the field.

---

## ✨ Key Features

- 📱 **SMS Control** — Farmer sends simple `VALVE1 ON` / `VALVE2 OFF` commands from any mobile
- 📶 **LoRa Wireless** — Long-range Sub-GHz communication across open farm terrain
- 🔋 **Ultra-Low Power** — Deep sleep + MOSFET-gated peripherals for 3+ year battery life
- ☀️ **Solar Powered** — 6W solar panel + 12V battery per node
- ✅ **Position Feedback** — Dual limit switches confirm fully open/closed valve state
- 💸 **Budget Friendly** — Under ₹1,500 per slave node using off-the-shelf components

---

## 🏗️ System Architecture

```
Farmer's Mobile Phone
        │
        │ SMS (GSM Network)
        ▼
┌─────────────────────┐
│    MASTER NODE      │  ← ESP32 + GSM + LoRa (Centre Field)
└─────────────────────┘
        │
        │ LoRa Wireless
        ▼
┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐
│  S1  │ │  S2  │ │  S3  │ │ S4+5 │   ← Slave Nodes
│North │ │N-Ctr │ │S-Ctr │ │South │      ESP32 + Motor + LoRa
└──────┘ └──────┘ └──────┘ └──────┘
    │         │        │        │
    └─────────┴────────┴────────┘
         DC Gear Motor + Limit Switches
```

---

## 🔧 Technology Stack

| Layer | Technology |
|-------|-----------|
| Microcontroller | ESP32 / NodeMCU |
| Wireless Protocol | LoRa (Sub-GHz ISM band) |
| Mobile Communication | GSM / SIM800L — SMS based |
| Motor Control | BTS7960 H-Bridge Driver |
| Actuator | 12V DC Gear Motor (10–30 RPM, 20–25 kg.cm) |
| Power | 12V Battery + 6W Solar + Charge Controller |
| Position Sensing | Mechanical Limit Switches (×2 per node) |
| Sleep / Wake | RTC scheduling + ESP32 Deep Sleep |

---

## 💰 Bill of Materials

### Slave Node (per unit — under ₹1,500)

| Component | Specification | Cost (INR) |
|-----------|--------------|------------|
| ESP32 Microcontroller | NodeMCU / ESP32 | ₹150–200 |
| LoRa Module + Antenna | SX1276 or equivalent | ₹200–250 |
| Motor Driver | BTS7960 H-Bridge | ₹200 |
| DC Gear Motor | 12V, 10–30 RPM | ₹400 |
| Limit Switches ×2 | 2 × ₹20 | ₹40 |
| 12V Battery | Per power requirement | <₹500 |
| 6W Solar Panel + Controller | With charge controller | <₹500 |
| Buck Converter | 12V → 5V | <₹100 |
| MOSFET | Power switching | ₹10 |
| Misc (PCB, casing) | — | ₹100–200 |
| **Total** | | **< ₹1,500** |

### Master Node

| Component | Specification | Cost (INR) |
|-----------|--------------|------------|
| ESP32 Microcontroller | NodeMCU / ESP32 | ₹150–200 |
| LoRa Module + Antenna | Long Range | ₹200–250 |
| GSM Module | SIM800L or equivalent | ₹500–700 |
| Solar Panel + Battery | Per requirement | As needed |

---

## 📡 Communication Flow

1. **Farmer sends SMS** → `VALVE1 ON` to Master Node's GSM number
2. **Master Node receives** → ESP32 wakes, parses command
3. **LoRa transmission** → Command relayed to target Slave Node
4. **Slave actuates valve** → DC gear motor opens/closes (10–20 sec)
5. **Limit switch confirms** → Fully open or closed position detected
6. **Acknowledgement sent** → Status relayed back, optional SMS to farmer

---

## ⚡ Power Management

- **Deep Sleep Mode** — ESP32 sleeps between communication windows
- **RTC Scheduling** — Wake-up at defined intervals only
- **MOSFET Power Gating** — LoRa, GSM, motor driver fully cut when idle
- **Gear Motor Hold** — Mechanically holds valve position, zero idle power
- **6W Solar + 12V Battery** — Sufficient for 3+ years of low-duty-cycle operation

---

## 🗺️ Farm Node Placement

| Node | Type | Position | Coverage Zone |
|------|------|----------|---------------|
| Node 0 | Master | Centre (~50m from south) | Full field via LoRa |
| Node 1 | Slave | North (~120m from south) | North irrigation |
| Node 2 | Slave | N-Centre (~80m from south) | North-centre zone |
| Node 3 | Slave | S-Centre (~30m from south) | South-centre zone |
| Node 4+5 | Slave (pair) | South end, side by side | South zones |

---

## 📅 Project Timeline

| Phase | Activity | Duration |
|-------|----------|----------|
| Phase 1 | Component procurement & hardware testing | Week 1–2 |
| Phase 2 | Slave node firmware (LoRa + Motor control) | Week 3–4 |
| Phase 3 | Master node firmware (GSM + LoRa gateway) | Week 5–6 |
| Phase 4 | Power management & deep sleep integration | Week 7 |
| Phase 5 | Field testing & calibration on farm site | Week 8–9 |
| Phase 6 | Documentation, review & final demo | Week 10 |

---

## 📁 Repository Structure

```
rvcm-website/
├── index.html              # Main website (GitHub Pages)
├── rvcm.pdf                # RVCM Project Report
├── project_requires.pdf    # Project Requirements Document
└── README.md               # This file
```

---

## 🚀 Website Built With

- Pure **HTML5 + CSS3** — no frameworks, no dependencies
- **Google Fonts** — Inter + Space Grotesk
- Hosted on **GitHub Pages** — free, permanent hosting

---

## 👤 Author

**pvkkr**
- GitHub: [@pvkkr](https://github.com/pvkkr)
- Project: [rvcm-website](https://github.com/pvkkr/rvcm-website)

---

## 📜 License

This project is licensed under the MIT License.

---

*Built for smart, affordable, and reliable irrigation management in Indian agriculture.*
