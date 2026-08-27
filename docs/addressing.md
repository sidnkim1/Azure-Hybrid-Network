# Addressing Plan

## Overview

This document defines the IP addressing, VLAN assignments, routing domains, and cloud address spaces used throughout the Hybrid Enterprise Network project.

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
| Core Transit | 10.42.254.0/30 |
| FG-FW-A ↔ Core-A | 10.42.5.0/30 |
| FG-FW-A ↔ Core-B | 10.42.5.4/30 |
| FG-FW-B ↔ Core-A | 10.42.5.8/30 |
| FG-FW-B ↔ Core-B | 10.42.5.12/30 |
| FortiGate Loopback | 10.42.255.1/32 |

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
| Core Transit | 10.69.254.0/30 |
| FG-FW-A ↔ Core-A | 10.69.5.0/30 |
| FG-FW-A ↔ Core-B | 10.69.5.4/30 |
| FG-FW-B ↔ Core-A | 10.69.5.8/30 |
| FG-FW-B ↔ Core-B | 10.69.5.12/30 |
| FortiGate Loopback | 10.69.255.1/32 |

### Route Summary

```text
10.69.0.0/16
```

Advertised to Azure via BGP.

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
| 10.100.1.0/24 | GatewaySubnet |
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
| 10.102.10.0/24 | DNS Services |

### Services

- BIND DNS Server
- Azure Private DNS
- Shared Services

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

- MLS-CORE-A
- MLS-CORE-B
- FG-FW-A
- FG-FW-B

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
