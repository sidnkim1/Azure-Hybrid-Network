# Hybrid Enterprise Network

## Overview

Hybrid enterprise network deployment simulating a multi-site organization integrated with Microsoft Azure through a hybrid-cloud architecture.

The environment combines enterprise routing, firewalling, high availability, VPN connectivity, and cloud networking services to model a modern network spanning on-premises infrastructure and Azure resources.

The primary objective is to demonstrate a resilient hybrid enterprise architecture that integrates traditional networking infrastructure with cloud-native services, centralized connectivity, dynamic routing, and secure access to distributed workloads.

---

## Key Features

- Multi-site enterprise architecture
- FortiGate High Availability (HA)
- OSPF internal routing
- BGP route exchange with Azure
- Dual ISP connectivity
- Site-to-Site IPSec VPN connectivity
- Azure Hub-and-Spoke architecture
- Azure Virtual WAN integration
- Private Endpoint connectivity
- Azure DNS services
- Layer 3 core redundancy using HSRP
- Segmented VLAN architecture
- Redundant switching infrastructure

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

The Azure environment utilizes a Hub-and-Spoke architecture and consists of:

#### Hub VNet

- Azure VPN Gateway
- Azure DNS Resolver
- Hybrid Connectivity Services
- Route Propagation

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
- Route Summarization
- Route Propagation
- Azure Route Tables
- User Defined Routes (UDRs)

### Security

- FortiGate High Availability
- Site-to-Site IPSec VPN
- Network Security Groups (NSGs)
- Private Endpoints

### Azure Networking

- Hub-and-Spoke Architecture
- Azure VPN Gateway
- Azure DNS Resolver
- Azure Private DNS
- VNet Peering
- Application Gateway
- Virtual WAN

---

## Documentation

### Architecture

High-level design, connectivity model, and Azure integration.

```text
docs/architecture.md
```

### Addressing Plan

IP addressing, VLAN assignments, routing domains, WAN connectivity, and Azure network design.

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
│   └── addressing.md
│
├── configs
│   ├── HQ
│   ├── Branch
│   └── Azure
│
└── screenshots
```

---

## Network Architecture Focus

The environment is designed to demonstrate end-to-end connectivity between enterprise users, on-premises infrastructure, security appliances, and Azure-hosted services.

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

The architecture provides visibility into traffic flow across multiple networking domains while supporting validation, troubleshooting, resiliency testing, and hybrid-cloud connectivity scenarios.
