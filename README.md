# OT / ICS Security Labs

![OT / ICS Security Labs](assets/ot-industrial-overview.png)

## About this repository

This repository is my hands-on **OT / ICS security portfolio**.

It is designed to document practical work across industrial networking, PLC/HMI communications, Modbus TCP, packet analysis, detection engineering, network segmentation, firewall hardening, process-aware monitoring, and OT incident response.

A major part of this portfolio is built using **Martin Scheu's `ot-lab` framework** as the underlying simulated industrial environment.

> **Credit:** The base OT lab framework was created by **Martin Scheu**.  
> Original project: `https://gitlab.switch.ch/martin.scheu/ot-lab`  
> Original project license: **MIT**
>
> I did not create the underlying `ot-lab` framework. My work in this repository focuses on deploying it, analyzing it, extending it, hardening it, creating detections, generating evidence, and building security projects around it.

---

## Why this lab

Martin Scheu's lab provides a realistic foundation for hands-on OT security work, including:

- OpenPLC v4
- FUXA HMI / SCADA
- Modbus TCP Sub Control Panels
- MikroTik RouterOS gateway / firewall
- MikroTik RouterOS distribution switch
- Containerlab
- Engineering terminal
- Integrated PCAP capture
- OT process simulation

Instead of using the lab only as a demo environment, the goal is to turn it into a progressive OT security portfolio:

```text
Deploy
  ↓
Understand the process
  ↓
Capture traffic
  ↓
Build a baseline
  ↓
Map registers
  ↓
Detect suspicious activity
  ↓
Harden the network
  ↓
Segment the architecture
  ↓
Investigate incidents
  ↓
Build process-aware detections
```

---

# Martin Scheu OT Lab — Project Series

All projects below are based on the original `ot-lab` framework and are stored under:

```text
martin-scheu-ot-lab/
```

| # | Project | Focus | Status |
|---:|---|---|---|
| 01 | **Modbus TCP Traffic Analysis** | FC03 / FC06, PCAP analysis, HMI-to-SCP traffic | 🟢 In progress |
| 02 | **Modbus Register & Process Mapping** | Reverse-map HMI variables to Modbus registers | ⏳ Planned |
| 03 | **OT Network Baseline** | Assets, flows, ports, polling frequency | ⏳ Planned |
| 04 | **Unauthorized Modbus Write Detection** | Detect abnormal FC06 / FC16 writes | ⏳ Planned |
| 05 | **Suricata Rules for Modbus** | OT IDS signatures and validation | ⏳ Planned |
| 06 | **Snort OT Detection Pack** | Snort rules for industrial control traffic | ⏳ Planned |
| 07 | **Wireshark OT Investigation Playbook** | Repeatable OT packet-investigation workflow | ⏳ Planned |
| 08 | **OT Asset Discovery** | Identify PLC/HMI/SCP/network roles from traffic | ⏳ Planned |
| 09 | **Modbus Register Enumeration** | Build and validate a register map | ⏳ Planned |
| 10 | **PLC/HMI Process Manipulation Analysis** | Correlate control changes with process impact | ⏳ Planned |
| 11 | **Process Anomaly Detection** | Detect unsafe or impossible process behavior | ⏳ Planned |
| 12 | **MikroTik OT Firewall Hardening** | Allow-listing and TCP/502 control | ⏳ Planned |
| 13 | **Flat Network vs Segmented OT Network** | Zones, conduits, segmentation, ACLs | ⏳ Planned |
| 14 | **Engineering Workstation Security** | Restrict and monitor engineering access | ⏳ Planned |
| 15 | **OT Incident Response Scenario** | Timeline, PCAP evidence, containment, recovery | ⏳ Planned |
| 16 | **Compromised HMI Scenario** | Detect valid-but-unauthorized control actions | ⏳ Planned |
| 17 | **OT PCAP Dataset** | Labelled normal / write / alarm / process captures | ⏳ Planned |
| 18 | **Complete OT SOC Monitoring Project** | Baseline + IDS + detections + investigation | ⏳ Planned |

---

## Current Project

### 01 — Modbus TCP Traffic Analysis

The first project analyzes communication between:

```text
FUXA HMI
172.18.1.30
     |
     | Modbus TCP / 502
     v
SCP-1
172.18.1.21
```

Observed behavior includes:

- FC03 — Read Holding Registers
- FC06 — Write Single Register
- Register-to-process mapping
- Level setpoint changes
- Outlet-flow setpoint changes
- Outlet-valve commands
- Process impact visible in the HMI

Current confirmed mappings:

| Register | Process Variable | Evidence |
|---:|---|---|
| `2` | Tank Level Setpoint | `60 → 65 → 60` |
| `4` | Outlet Valve Position / Command | `100 = Open`, `0 = Closed` |
| `16` | Outlet Flow Setpoint | `200 → 220 → 200 L/s` |

---

## Repository Structure

```text
ot-labs-/
├── README.md
├── assets/
│   └── ot-industrial-overview.png
│
└── martin-scheu-ot-lab/
    ├── README.md
    ├── 01-modbus-traffic-analysis/
    ├── 02-modbus-register-process-mapping/
    ├── 03-ot-network-baseline/
    ├── 04-unauthorized-modbus-write-detection/
    ├── 05-suricata-modbus-rules/
    ├── 06-snort-ot-detection-pack/
    ├── 07-wireshark-ot-investigation-playbook/
    ├── 08-ot-asset-discovery/
    ├── 09-modbus-register-enumeration/
    ├── 10-plc-hmi-process-manipulation/
    ├── 11-process-anomaly-detection/
    ├── 12-mikrotik-firewall-hardening/
    ├── 13-flat-vs-segmented-ot-network/
    ├── 14-engineering-workstation-security/
    ├── 15-ot-incident-response/
    ├── 16-compromised-hmi-scenario/
    ├── 17-ot-pcap-dataset/
    └── 18-complete-ot-soc-monitoring/
```

---

## Security Focus

The goal is not simply to run an OT simulation.

Each project is intended to produce evidence of practical security work:

- network diagrams
- packet captures
- Wireshark investigations
- register mappings
- detection rules
- firewall rules
- segmentation designs
- incident timelines
- defensive findings
- process-aware detections

---

## Disclaimer

All testing is performed in a controlled lab environment for educational and defensive-security purposes.

The original OT simulation framework belongs to its respective author and contributors. This repository documents my own security analysis, extensions, detections, configurations, and project work built around that environment.
