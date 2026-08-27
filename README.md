# Hybrid Enterprise Network

## Overview

This project is a hybrid enterprise networking lab designed to simulate a real-world multi-site enterprise connected to Microsoft Azure.

The environment combines traditional enterprise networking technologies with cloud networking services to provide hands-on experience with routing, VPNs, DNS, high availability, cloud connectivity, troubleshooting, and network operations.

The primary goal of the project is to create a platform for learning, testing, and troubleshooting technologies commonly found in modern hybrid cloud environments.

---

## Objectives

This project provides practical experience with:

- Hybrid cloud networking
- Site-to-Site VPNs
- IPSec tunnels
- OSPF routing
- BGP fundamentals
- DNS troubleshooting
- Azure Private DNS
- Conditional forwarding
- Private Endpoints
- VNet Peering
- Route Tables and UDRs
- Application Gateway
- High availability and resiliency testing
- Incident response and troubleshooting workflows

---

## Environment Overview

The environment consists of:

### Headquarters Site

- Dual Access Switches
- Dual Layer 3 Core Switches
- FortiGate HA Pair
- Dual ISP Connectivity
- User, Management, and Server VLANs

### Branch Site

- Dual Access Switches
- Dual Layer 3 Core Switches
- FortiGate HA Pair
- Dual ISP Connectivity
- User, Management, and Server VLANs

### Microsoft Azure

- Hub VNet
- Production VNet
- Services VNet
- Azure VPN Gateway
- Azure Private DNS
- Application Gateway
- Application VM
- DNS Services

---

## Documentation

- [Architecture Design](docs//addressing.md
- [DNS Design](docs/dns.mdository Structure

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
