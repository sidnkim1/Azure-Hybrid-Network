# Architecture

## Overview

This project simulates a hybrid enterprise environment consisting of two on-premises sites connected to Microsoft Azure.

The environment is designed to provide hands-on experience with enterprise networking, cloud networking, VPN connectivity, routing, DNS, and troubleshooting.

---

# High-Level Architecture

```text
                     Microsoft Azure

                 +----------------------+
                 |       Hub VNet       |
                 +----------+-----------+
                            |
            +---------------+---------------+
            |                               |
            |                               |
    +-------+--------+             +--------+-------+
    |  Production    |             |   Services     |
    |     VNet       |             |     VNet       |
    +----------------+             +----------------+

                            |
                     Azure VPN Gateway

                      /             \

                     /               \

           Headquarters              Branch
```

---

# Headquarters

The Headquarters site contains:

- Four end-user hosts
- Two access switches
- Two Layer 3 core switches
- Two FortiGate firewalls configured in HA
- Two ISP pass-through switches
- Dual ISP connectivity

Traffic from users is forwarded through the access layer, core layer, and FortiGate firewalls before reaching external resources.

---

# Branch

The Branch site mirrors the Headquarters architecture.

The site contains:

- Four end-user hosts
- Two access switches
- Two Layer 3 core switches
- Two FortiGate firewalls configured in HA
- Two ISP pass-through switches
- Dual ISP connectivity

Branch resources communicate with Azure through the Azure VPN Gateway.

---

# Azure Environment

The Azure environment utilizes a hub-and-spoke architecture.

## Hub VNet

The Hub VNet provides:

- VPN connectivity
- Route propagation
- DNS services

## Production VNet

The Production VNet hosts:

- Application Gateway
- Application workloads
- Private Endpoints

## Services VNet

The Services VNet hosts:

- BIND DNS
- Azure Private DNS
- Shared infrastructure services

---

# Connectivity

Headquarters and Branch establish Site-to-Site VPN connections to Azure.

```text
HQ
  \
   \
    Azure VPN Gateway
   /
  /
Branch
```

The Azure Hub VNet serves as the central connectivity point between all environments.

---

# Routing

Routing within each site is handled through OSPF.

Routing between Azure and the on-premises sites is handled through BGP.

---

# DNS

DNS services are provided through a hybrid design utilizing:

- BIND DNS
- Azure DNS Resolver
- Azure Private DNS

Additional DNS information is documented in:

```text
docs/dns.md
```

---

# Project Components

## On-Premises

- Access Layer
- Core Layer
- FortiGate HA
- OSPF
- BGP
- Site-to-Site VPN

## Microsoft Azure

- Hub VNet
- Production VNet
- Services VNet
- VPN Gateway
- Application Gateway
- Private Endpoints
- Azure DNS Services
- Route Tables
- NSGs
