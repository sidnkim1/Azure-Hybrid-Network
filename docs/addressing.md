# Addressing Plan

## Overview

This document defines the IP addressing, VLAN assignments, routing domains, WAN transit networks, Azure address spaces, and BGP design used throughout the Hybrid Enterprise Network deployment.

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

### Core Infrastructure

```text
HSRP Virtual Gateway = .1
MLS-CORE-A           = .2
MLS-CORE-B           = .3
```

### Firewall Transit Networks

#### CORE-A Transit

```text
10.42.5.0/30

FortiGate HA Pair = 10.42.5.1
MLS-CORE-A        = 10.42.5.2
```

#### CORE-B Transit

```text
10.42.5.4/30

FortiGate HA Pair = 10.42.5.5
MLS-CORE-B        = 10.42.5.6
```

### WAN Connectivity

#### ISP-A

```text
172.42.0.0/29
```

#### ISP-B

```text
172.42.0.8/29
```

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

### WAN Connectivity

#### ISP-C

```text
172.69.0.0/29
```

#### ISP-D

```text
172.69.0.8/29
```

### Route Summary

```text
10.69.0.0/16
```

Advertised to Azure via BGP.

---

# Endpoint Placement

## Headquarters

| Host | VLAN | Address |
|----------|----------|------------|
| HOST-A | VLAN 20 | 10.42.20.10 |
| HOST-B | VLAN 20 | 10.42.20.11 |
| HOST-C | VLAN 30 | 10.42.30.10 |
| HOST-D | VLAN 10 | 10.42.10.10 |

---

## Branch

| Host | VLAN | Address |
|----------|----------|------------|
| HOST-E | VLAN 20 | 10.69.20.10 |
| HOST-F | VLAN 20 | 10.69.20.11 |
| HOST-G | VLAN 30 | 10.69.30.10 |
| HOST-H | VLAN 10 | 10.69.10.10 |

---

# Microsoft Azure

## Hub VNet

### Address Space

```text
10.100.0.0/16
```

### Subnets

```text
10.100.1.0/24
Azure VPN Gateway
```

```text
10.100.2.0/24
Azure DNS Resolver
```

---

## Production VNet

### Address Space

```text
10.101.0.0/16
```

### Subnets

```text
10.101.1.0/24
Application Gateway
```

```text
10.101.10.0/24
Application Servers
```

```text
10.101.20.0/24
Private Endpoints
```

---

## Services VNet

### Address Space

```text
10.102.0.0/16
```

### Subnets

```text
10.102.10.0/24
Azure Private DNS
```

---

# Routing Design

## Internal Routing

```text
OSPF Process ID 42
Area 0
```

### Participants

```text
MLS-CORE-A
MLS-CORE-B
FortiGate HA Pair
```

---

## External Routing

```text
BGP
```

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
