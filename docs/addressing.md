# Addressing Plan

## Overview

This document defines the IP addressing, VLAN assignments, routing domains, cloud address spaces, WAN transit networks, and BGP design used throughout the Hybrid Enterprise Network project.

The addressing plan is designed to:

- Prevent overlapping address spaces
- Support route summarization
- Simplify troubleshooting
- Support hybrid-cloud connectivity
- Support dynamic route exchange using BGP
- Provide room for future expansion

---

# Headquarters (HQ)

## Site Summary

```text
10.42.0.0/16
```

### VLAN Assignments

| VLAN | Name | Subnet | Gateway |
|--------|--------|------------|------------|
| 10 | Management | 10.42.10.0/24 | 10.42.10.1 |
| 20 | Users | 10.42.20.0/24 | 10.42.20.1 |
| 30 | Servers | 10.42.30.0/24 | 10.42.30.1 |
| 40 | Guest | 10.42.40.0/24 | 10.42.40.1 |
| 100 | Finance | 10.42.100.0/24 | 10.42.100.1 |

### Infrastructure Networks

| Purpose | Subnet |
|------------|------------|
| FG-FW-A ↔ MLS-CORE-A | 10.42.5.0/30 |
| FG-FW-A ↔ MLS-CORE-B | 10.42.5.4/30 |
| FG-FW-B ↔ MLS-CORE-A | 10.42.5.8/30 |
| FG-FW-B ↔ MLS-CORE-B | 10.42.5.12/30 |
| WAN-A Transit | 172.42.0.0/29 |
| WAN-B Transit | 172.42.0.8/29 |
| FortiGate Loopback | 10.42.255.1/32 |

### Addressing Convention

| Device | Address Pattern |
|----------|----------|
| HSRP VIP | x.x.x.1 |
| Primary Core Switch | x.x.x.2 |
| Secondary Core Switch | x.x.x.3 |
| Primary FortiGate | x.x.x.5 |
| Secondary FortiGate | x.x.x.9 |

### Route Summary

```text
10.42.0.0/16
```

Advertised to Azure via BGP.

---

# Branch Office

## Site Summary

```text
10.69.0.0/16
```

### VLAN Assignments

| VLAN | Name | Subnet | Gateway |
|--------|--------|------------|------------|
| 10 | Management | 10.69.10.0/24 | 10.69.10.1 |
| 20 | Users | 10.69.20.0/24 | 10.69.20.1 |
| 30 | Servers | 10.69.30.0/24 | 10.69.30.1 |
| 40 | Guest | 10.69.40.0/24 | 10.69.40.1 |
| 100 | Finance | 10.69.100.0/24 | 10.69.100.1 |

### Infrastructure Networks

| Purpose | Subnet |
|------------|------------|
| FG-FW-C ↔ MLS-CORE-C | 10.69.5.0/30 |
| FG-FW-C ↔ MLS-CORE-D | 10.69.5.4/30 |
| FG-FW-D ↔ MLS-CORE-C | 10.69.5.8/30 |
| FG-FW-D ↔ MLS-CORE-D | 10.69.5.12/30 |
| WAN-C Transit | 172.69.0.0/29 |
| WAN-D Transit | 172.69.0.8/29 |
| FortiGate Loopback | 10.69.255.1/32 |

### Addressing Convention

| Device | Address Pattern |
|----------|----------|
| HSRP VIP | x.x.x.1 |
| Primary Core Switch | x.x.x.2 |
| Secondary Core Switch | x.x.x.3 |
| Primary FortiGate | x.x.x.5 |
| Secondary FortiGate | x.x.x.9 |

### Route Summary

```text
10.69.0.0/16
```

Advertised to Azure via BGP.

---

# Endpoint Placement

## Headquarters

| Host | VLAN |
|----------|----------|
| HOST-A | VLAN 20 |
| HOST-B | VLAN 20 |
| HOST-C | VLAN 30 |
| HOST-D | VLAN 10 |

---

## Branch

| Host | VLAN |
|----------|----------|
| HOST-E | VLAN 20 |
| HOST-F | VLAN 20 |
| HOST-G | VLAN 30 |
| HOST-H | VLAN 10 |

---

# Microsoft Azure

## Hub VNet

### Address Space

```text
10.100.0.0/16
```

### Subnets

| Subnet | Purpose |
|------------|------------|
| 10.100.1.0/24 | VPN Gateway |
| 10.100.2.0/24 | DNS Resolver |

### Services

- Azure VPN Gateway
- Azure DNS Resolver
- Route Tables
- User Defined Routes
- BGP Route Exchange

### Route Summary

```text
10.100.0.0/16
```

---

## Production VNet

### Address Space

```text
10.101.0.0/16
```

### Subnets

| Subnet | Purpose |
|------------|------------|
| 10.101.1.0/24 | Application Gateway |
| 10.101.10.0/24 | Application Servers |
| 10.101.20.0/24 | Private Endpoints |

### Services

- Application Gateway
- Application VM
- NSGs
- Route Tables
- Private Endpoints

### Route Summary

```text
10.101.0.0/16
```

---

## Services VNet

### Address Space

```text
10.102.0.0/16
```

### Subnets

| Subnet | Purpose |
|------------|------------|
| 10.102.10.0/24 | Azure Private DNS |

### Services

- Azure Private DNS
- Shared Infrastructure Services

### Route Summary

```text
10.102.0.0/16
```

---

# Azure Route Summaries

The Azure environment advertises the following networks:

```text
10.100.0.0/16
10.101.0.0/16
10.102.0.0/16
```

---

# VPN Connectivity

## Headquarters

VPN Endpoint:

```text
FG-FW-A / FG-FW-B
```

Peer:

```text
Azure VPN Gateway
```

---

## Branch

VPN Endpoint:

```text
FG-FW-C / FG-FW-D
```

Peer:

```text
Azure VPN Gateway
```

---

## Topology

```text
HQ
  \
   \
    Azure VPN Gateway
   /
  /
Branch
```

---

# Routing Design

## Internal Routing

### Headquarters

Protocol:

```text
OSPF Area 0
```

Participants:

- MLS-CORE-A
- MLS-CORE-B
- FG-FW-A
- FG-FW-B

---

### Branch

Protocol:

```text
OSPF Area 0
```

Participants:

- MLS-CORE-C
- MLS-CORE-D
- FG-FW-C
- FG-FW-D

---

## External Routing

Protocol:

```text
BGP
```

Azure functions as the cloud routing hub.

### Headquarters

```text
ASN 65001
```

Advertises:

```text
10.42.0.0/16
```

---

### Branch

```text
ASN 65002
```

Advertises:

```text
10.69.0.0/16
```

---

### Azure

```text
ASN 65515
```

Advertises:

```text
10.100.0.0/16
10.101.0.0/16
10.102.0.0/16
```

---

# Connectivity Model

Traffic between Headquarters and Branch traverses Azure.

```text
HQ
 |
 |
Azure VPN Gateway
 |
 |
Branch
```

### Headquarters Reachability

Can access:

```text
10.69.0.0/16
10.100.0.0/16
10.101.0.0/16
10.102.0.0/16
```

---

### Branch Reachability

Can access:

```text
10.42.0.0/16
10.100.0.0/16
10.101.0.0/16
10.102.0.0/16
```

---

# Address Space Summary

| Environment | Address Space |
|-------------|----------------|
| Headquarters | 10.42.0.0/16 |
| Branch | 10.69.0.0/16 |
| Azure Hub | 10.100.0.0/16 |
| Azure Production | 10.101.0.0/16 |
| Azure Services | 10.102.0.0/16 |

---

# Autonomous System Summary

| Environment | ASN |
|-------------|------|
| Headquarters | 65001 |
| Branch | 65002 |
| Azure | 65515 |
