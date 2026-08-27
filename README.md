# Hybrid Enterprise Network

## Overview

Hybrid enterprise networking deployment designed to simulate a multi-site enterprise connected to Microsoft Azure.

The environment combines traditional enterprise networking technologies with cloud networking services to provide hands-on experience with routing, VPNs, DNS, high availability, cloud connectivity, troubleshooting, and network operations.

The primary goal is to provide a realistic platform for learning and troubleshooting technologies commonly found in modern hybrid-cloud environments.

---

## Environment Overview

### Headquarters (HQ)

The Headquarters site includes:

- Four end-user hosts
- Two access switches
- Two Layer 3 core switches
- FortiGate HA firewall pair
- Two ISP pass-through switches
- Two ISP demarcation routers
- Dual ISP connectivity
- OSPF routing
- BGP connectivity to Azure

### Branch Office

The Branch site mirrors the Headquarters architecture and includes:

- Four end-user hosts
- Two access switches
- Two Layer 3 core switches
- FortiGate HA firewall pair
- Two ISP pass-through switches
- Two ISP demarcation routers
- Dual ISP connectivity
- OSPF routing
- BGP connectivity to Azure

### Microsoft Azure

The Azure environment utilizes a hub-and-spoke architecture and consists of:

#### Hub VNet

- Azure VPN Gateway
- Azure DNS Resolver
- Route Propagation
- Hybrid Connectivity Services

#### Production VNet

- Application Gateway
- Application Virtual Machine
- Private Endpoint

#### Services VNet

- Azure Private DNS

---

## Core Technologies

### Routing

- OSPF
- BGP
- Route Propagation
- Route Summarization
- Azure Route Tables
- User Defined Routes (UDRs)

### Security

- FortiGate High Availability
- Site-to-Site IPSec VPNs
- Network Security Groups (NSGs)
- Private Endpoints

### Azure Networking

- Hub-and-Spoke Architecture
- Azure VPN Gateway
- Azure DNS Resolver
- Azure Private DNS
- VNet Peering
- Application Gateway

---

## Documentation

### Architecture

High-level design, connectivity model, and Azure integration.

```text
docs/architecture.md
```

### Addressing Plan

IP addressing, VLAN assignments, Azure address spaces, routing design, VPN connectivity, and BGP configuration.

```text
docs/addressing.md
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

## Traffic Flow Focus

The project is designed around understanding end-to-end packet flow across on-premises and cloud environments.

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

Understanding and troubleshooting that packet journey is the primary focus of the project.
