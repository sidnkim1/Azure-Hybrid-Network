# Hybrid Enterprise Network

## Overview

Hybrid enterprise networking deployment designed to simulate a multi-site enterprise connected to Microsoft Azure.

The environment combines traditional enterprise networking technologies with cloud networking services to provide hands-on experience with routing, VPNs, DNS, high availability, cloud connectivity, troubleshooting, and network operations.

The primary goal: troubleshooting technologies commonly found in modern hybrid cloud environments.

---

## Environment Overview

### Headquarters (HQ)

The Headquarters site includes:

- FortiGate HA firewall pair
- Dual Layer 3 core switches
- Dual access switches
- Multiple VLANs
- Dual ISP connectivity
- On-premises users and services

### Branch Office

The Branch site mirrors the HQ architecture and includes:

- FortiGate HA firewall pair
- Dual Layer 3 core switches
- Dual access switches
- Multiple VLANs
- Dual ISP connectivity
- On-premises users and services

### Microsoft Azure

The Azure environment consists of:

- Hub VNet
- Production VNet
- Services VNet
- Azure VPN Gateway
- Azure DNS services
- Application Gateway
- Application VM
- Private Endpoints
- Route Tables
- NSGs

---

## Documentation

### Architecture

High-level design, connectivity model, and Azure integration.

```text
docs/architecture.md
```

### Addressing Plan

IP addressing, VLAN assignments, Azure address spaces, and routing domains.

```text
docs/addressing.md
```

### DNS Design

Hybrid DNS architecture including BIND DNS, Azure DNS Resolver, Azure Private DNS, and conditional forwarding.

```text
docs/dns.md
```

---

## Repository Structure

```text
Hybrid-Enterprise-Network
│
├── README.md
│
├── docs
│   ├── architecture.md
│   ├── addressing.md
│   ├── dns.md
│   └── diagrams
│
├── configs
│   ├── HQ
│   ├── Branch
│   └── Azure
│
└── screenshots
```

---

Focused on understanding end-to-end packet flow:

```text
Client
  ↓
DNS
  ↓
Routing
  ↓
Firewall
  ↓
VPN
  ↓
Azure Networking
  ↓
Application
  ↓
Return Path
```
