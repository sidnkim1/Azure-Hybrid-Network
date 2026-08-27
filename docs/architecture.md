# Architecture

## Overview

This project simulates a hybrid enterprise environment consisting of two on-premises sites connected to Microsoft Azure.

The environment is designed to provide hands-on experience with enterprise networking, cloud networking, VPN connectivity, routing, DNS, high availability, and troubleshooting.

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
- Two ISP demarcation routers
- Dual ISP connectivity

Traffic traverses the access layer, core layer, and FortiGate firewalls before reaching external resources.

---

# Branch

The Branch site mirrors the Headquarters architecture.

The site contains:

- Four end-user hosts
- Two access switches
- Two Layer 3 core switches
- Two FortiGate firewalls configured in HA
- Two ISP pass-through switches
- Two ISP demarcation routers
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

### Components

- Azure VPN Gateway
- Azure DNS Resolver

---

## Production VNet

The Production VNet hosts:

- Application Gateway
- Application VM
- Private Endpoint

---

## Services VNet

The Services VNet hosts:

- Azure Private DNS

---

# Connectivity

Headquarters and Branch establish independent Site-to-Site VPN connections to Azure.

```text
HQ
  \
   \
    Azure VPN Gateway
   /
  /
Branch
```

The Hub VNet serves as the central connectivity point between all environments.

---

# Routing

Routing within each site is handled through OSPF.

Routing between Azure and the on-premises sites is handled through BGP.

Azure functions as the cloud transit hub between Headquarters and Branch.

---

# DNS

DNS services are provided using:

- Azure DNS Resolver
- Azure Private DNS

DNS requests from on-premises sites are resolved through Azure DNS services over the VPN infrastructure.

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
- Azure VPN Gateway
- Azure DNS Resolver
- Azure Private DNS
- Application Gateway
- Application VM
- Private Endpoint
- Route Tables
- NSGs
