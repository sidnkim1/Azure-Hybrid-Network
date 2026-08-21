# Hybrid Azure Networking & Troubleshooting Lab

<img width="3000" height="4000" alt="20260821_144005" src="https://github.com/user-attachments/assets/e8d6af5c-e4a2-45c1-9dcd-9c57ece565bd" />

## Overview

This project is a hybrid enterprise networking lab designed to simulate a real-world Azure-connected environment and provide hands-on experience with routing, VPNs, DNS, cloud networking, resiliency testing, and incident troubleshooting.

The primary goal of the lab is not to build a production-ready Azure environment, but rather to create a platform for learning and troubleshooting technologies commonly found in modern hybrid cloud deployments.

The design combines traditional enterprise networking concepts with Microsoft Azure networking services to emulate common connectivity scenarios encountered by network engineers supporting hybrid environments.

---

## Objectives

This lab was designed to provide practical experience with:

- Hybrid cloud networking
- Site-to-Site VPNs
- IPSec tunnels
- Dynamic routing and route propagation
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

## High-Level Architecture

### On-Premises Environment

The environment contains two sites:

#### Headquarters (HQ)

Network Summary:

```text
10.42.0.0/16
```

VLANs:

```text
VLAN 10 - Management
10.42.10.0/24

VLAN 20 - Users
10.42.20.0/24

VLAN 30 - Servers
10.42.30.0/24
```

Infrastructure:

- Dual Access Switches
- Dual Layer 3 Core Switches
- FortiGate HA Pair
- Dual ISP Connectivity

---

#### Branch Office

Network Summary:

```text
10.69.0.0/16
```

VLANs:

```text
VLAN 10 - Management
10.69.10.0/24

VLAN 20 - Users
10.69.20.0/24

VLAN 30 - Printers
10.69.30.0/24
```

Infrastructure:

- Dual Access Switches
- Dual Layer 3 Core Switches
- FortiGate HA Pair
- Dual ISP Connectivity

---

## Azure Environment

The Azure environment follows a simplified Hub-and-Spoke architecture.

---

### Hub VNet

```text
10.100.0.0/16
```

Purpose:

- Hybrid connectivity
- DNS services
- Route management

Components:

```text
VPN Gateway
10.100.1.0/24

DNS Resolver
10.100.2.0/24
```

Associated Services:

- BGP
- Route Propagation
- Route Tables
- User Defined Routes (UDRs)

---

### Production VNet

```text
10.101.0.0/16
```

Purpose:

Application hosting and connectivity testing.

Components:

```text
Application Gateway
10.101.1.0/24

Application Servers
10.101.10.0/24

Private Endpoints
10.101.20.0/24
```

Associated Services:

- NSGs
- Route Tables

---

### Services VNet

```text
10.102.0.0/16
```

Purpose:

DNS and shared infrastructure services.

Components:

```text
DNS Services
10.102.10.0/24
```

Services:

- Azure Private DNS
- BIND DNS Server

---

## Connectivity Model

The on-prem environment connects into Azure using Site-to-Site IPSec VPN tunnels terminating on the Azure VPN Gateway.

```text
HQ
  \
   \
    Azure VPN Gateway
   /
  /
Branch
```

Future enhancements may include:

- Direct HQ ↔ Branch connectivity
- BGP route exchange
- Advanced failover testing
- Route convergence validation

---

## DNS Design

The environment uses a hybrid DNS model.

```text
Client
   |
BIND DNS
   |
Conditional Forwarder
   |
Azure DNS Resolver
   |
Azure Private DNS
   |
Private Endpoint
```

This enables testing of:

- Private DNS resolution
- Conditional forwarding
- Split-horizon DNS
- DNS path analysis
- Name resolution troubleshooting

---

## Key Technologies

### Routing

- OSPF
- BGP
- Route Propagation
- Route Summarization
- Route Tables
- UDRs

### Security

- FortiGate HA
- IPSec VPN
- NSGs

### Azure Networking

- Hub-and-Spoke Architecture
- VNet Peering
- Private Endpoints
- Azure DNS Resolver
- Azure Private DNS
- Application Gateway

### Operations

- Incident Response
- Connectivity Troubleshooting
- Failover Testing
- Resiliency Validation
- Root Cause Analysis

---

## Lab Use Cases

Example troubleshooting scenarios include:

- VPN tunnel established but traffic not passing
- Missing route propagation
- Incorrect UDR configuration
- Asymmetric routing
- Broken VNet peering
- NSG traffic blocking
- DNS resolution failures
- Private Endpoint connectivity issues
- Conditional forwarding problems
- Application Gateway backend failures
- VPN failover validation

---

## Project Goal

The ultimate objective is to create a realistic hybrid networking environment that allows repeated practice of troubleshooting methodologies used in enterprise and cloud environments.

The lab is intentionally designed around packet flow analysis:

```text
Source
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

Understanding and troubleshooting that packet journey is the primary focus of this project.
