# Network Design

## Overview

The project implements an enterprise-style corporate network using Cisco Packet Tracer.

The design separates users, servers, printers, wireless clients, management traffic and DMZ services into dedicated network segments.

Layer 3 routing is performed by the Cisco CORE-SW, while the Cisco ASA provides firewall and NAT functionality between the internal network and the external network.

## Network Architecture

The main network components are:

- Cisco Layer 3 Core Switch (CORE-SW)
- Cisco ASA Firewall (COMPANY-ASA)
- ISP Router
- Office PCs
- Internal Server
- Network Printer
- Wireless Access Point
- Wireless Clients
- DMZ Server

The logical architecture is:

    Internet
       |
    ISP Router
       |
    ASA Firewall
       |
    CORE-SW
       |
    +---------+---------+---------+---------+---------+
    |         |         |         |         |         |
  OFFICE   SERVERS   PRINTERS    WIFI   MANAGEMENT   DMZ
  VLAN 10  VLAN 20   VLAN 30   VLAN 40   VLAN 50   VLAN 60

## Core Switch

The CORE-SW operates as a Layer 3 switch.

Its main responsibilities are:

- Inter-VLAN routing
- Default gateway services
- DHCP services
- VLAN segmentation
- Access port configuration
- Port security
- SSH management
- Routing toward the ASA

The connection between the CORE-SW and ASA uses:

    CORE-SW: 10.0.0.1/30
    ASA:     10.0.0.2/30

## Firewall

The Cisco ASA separates the internal corporate network from the external network.

The ASA interfaces are configured as:

- Inside: 10.0.0.2/30
- Outside: 200.1.1.2/30

The ASA provides:

- Firewall functionality
- Traffic control
- NAT
- Routing between internal and external networks

## ISP Router

The ISP router represents the external network and Internet connectivity.

The connection between the ASA and ISP router uses:

    ASA:  200.1.1.2/30
    ISP:  200.1.1.1/30

The ISP router has an additional upstream connection:

    ISP: 100.100.100.1/30

## Network Segmentation

The network is divided into dedicated VLANs.

### VLAN 10 – OFFICE

Used by corporate office clients.

Network:

    192.168.10.0/24

### VLAN 20 – SERVERS

Used for internal network services and servers.

Network:

    192.168.20.0/24

### VLAN 30 – PRINTERS

Dedicated network segment for network printers.

Network:

    192.168.30.0/24

### VLAN 40 – WIFI

Dedicated network for wireless clients.

Network:

    192.168.40.0/24

### VLAN 50 – MANAGEMENT

Dedicated management network for network administration.

Network:

    192.168.50.0/24

### VLAN 60 – DMZ

Dedicated network segment for DMZ services.

Network:

    192.168.60.0/24

## Security Design

Several security mechanisms are implemented:

- VLAN segmentation
- Cisco ASA firewall
- NAT
- Extended ACL
- SSH management
- Management VLAN
- Port security
- Sticky MAC addresses
- PortFast
- BPDU Guard

Management access to the CORE-SW is restricted using the SSH-MANAGEMENT access control list.

Only the management network is permitted to access the switch through the configured SSH management policy.

## Design Goals

The main goals of the network design are:

1. Logical network segmentation
2. Controlled inter-VLAN communication
3. Centralized Layer 3 routing
4. Secure network management
5. Firewall protection
6. NAT for external connectivity
7. Separation of critical network services
8. Dedicated wireless and DMZ networks
9. Improved network scalability and maintainability

## Verification

The implementation can be verified using Cisco IOS and ASA commands such as:

    show vlan brief
    show ip interface brief
    show ip route
    show ip dhcp pool
    show access-lists
    show running-config

End-to-end connectivity can also be tested using:

    ipconfig
    ping
