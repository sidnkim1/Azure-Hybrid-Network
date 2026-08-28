# Architecture

## Overview

This project simulates a hybrid enterprise environment consisting of two on-premises sites connected to Microsoft Azure.

The environment combines enterprise networking, security, and cloud services within a highly available architecture designed around redundant connectivity, dynamic routing, and centralized cloud integration.

---

# High-Level Architecture

```text
                     Microsoft Azure

        +----------------+    +----------------+
        | Production     |    | Services       |
        | VNET           |    | VNET           |
        +-------+--------+    +--------+-------+
                |                      |
                |      VNET Peering    |
                |                      |
                +----------+-----------+
                           |
                    +------+------+
                    |   Hub VNET  |
                    +------+------+
                           |
                    Azure VPN Gateway
                       /         \
                      /           \
                     /             \
              Headquarters       Branch
```

---

# Headquarters

The Headquarters site contains:

- Four end-user hosts
- Two access switches
- Two Layer 3 core switches
- FortiGate HA firewall pair
- Two ISP pass-through switches
- Two ISP demarcation routers
- Dual ISP connectivity

The site provides redundant routing, switching, firewalling, and WAN connectivity services.

---

# Branch

The Branch site mirrors the Headquarters architecture.

The site contains:

- Four end-user hosts
- Two access switches
- Two Layer 3 core switches
- FortiGate HA firewall pair
- Two ISP pass-through switches
- Two ISP demarcation routers
- Dual ISP connectivity

Branch resources communicate with Azure through the Azure VPN Gateway.

---

# Azure Environment

The Azure environment utilizes a Hub-and-Spoke architecture.

## Hub VNet

The Hub VNet serves as the central cloud connectivity platform.

Components:

- Azure VPN Gateway
- Azure DNS Resolver

Responsibilities:

- Site-to-Site VPN connectivity
- Hybrid routing
- DNS integration
- VNet interconnectivity

---

## Production VNet

The Production VNet hosts application services.

Components:

- Application Gateway
- Application Virtual Machine
- Private Endpoint

Responsibilities:

- Application delivery
- Workload hosting
- Private service access

---

## Services VNet

The Services VNet provides shared cloud services.

Components:

- Azure Private DNS

Responsibilities:

- Private name resolution
- DNS integration across Azure services

---

# Connectivity

Headquarters and Branch establish independent VPN connections to Azure.

```text
HQ
  \
   \
    Azure VPN Gateway
   /
  /
Branch
```

Azure serves as the central transit hub between on-premises environments and cloud resources.

---

# Routing

Routing within each site is handled through OSPF.

The Layer 3 core infrastructure provides:

- Inter-VLAN routing
- HSRP gateway redundancy
- Route exchange with the firewall layer

Routing between Azure and the on-premises environments is performed using BGP.

Azure functions as the central routing hub for the hybrid environment.

---

# High Availability

Redundancy is implemented throughout the architecture.

### Headquarters

- Dual access switches
- Dual Layer 3 core switches
- FortiGate HA pair
- Dual ISP connectivity

### Branch

- Dual access switches
- Dual Layer 3 core switches
- FortiGate HA pair
- Dual ISP connectivity

### Azure

- Hub-and-Spoke architecture
- Redundant Azure VPN infrastructure
- Route propagation through BGP

---

# DNS

DNS services are provided through Azure-native services.

Components:

- Azure DNS Resolver
- Azure Private DNS

These services provide name resolution between Azure-hosted resources and connected enterprise networks.

---

# Project Components

## On-Premises

- Access Layer
- Core Layer
- HSRP
- OSPF
- FortiGate HA
- Site-to-Site VPN
- BGP

## Microsoft Azure

- Hub VNet
- Production VNet
- Services VNet
- Azure VPN Gateway
- Azure DNS Resolver
- Azure Private DNS
- Application Gateway
- Application VM
- Private Endpoint
- Route Tables
- Network Security Groups
