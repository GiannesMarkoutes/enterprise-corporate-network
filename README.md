# Enterprise Corporate Network – Cisco Packet Tracer

## Project Overview

This project demonstrates the design and implementation of an enterprise-style corporate network using Cisco Packet Tracer.

The network focuses on VLAN segmentation, inter-VLAN routing, DHCP, firewall security, NAT and access control.

---

## Network Topology

The network consists of the following main components:

- Cisco Layer 3 Core Switch
- Cisco ASA Firewall
- Cisco Router
- Office PCs
- Servers
- Network Printer
- Wireless Access Point
- Wireless Clients

The CORE-SW provides Layer 3 routing between the internal VLANs, while the Cisco ASA provides firewall and NAT functionality toward the external network.

---

## VLAN Configuration

The network is segmented into the following VLANs:

| VLAN | Name | Network | Purpose |
|------|------|---------|---------|
| 10 | OFFICE | 192.168.10.0/24 | Office network |
| 20 | SERVERS | 192.168.20.0/24 | Server network |
| 30 | PRINTERS | 192.168.30.0/24 | Printer network |
| 40 | WIFI | 192.168.40.0/24 | Wireless network |
| 50 | MANAGEMENT | 192.168.50.0/24 | Management network |

---

## Layer 3 Routing

The CORE-SW operates as a Layer 3 switch and provides the default gateway for the internal VLANs.

| VLAN | Default Gateway |
|------|-----------------|
| VLAN 10 | 192.168.10.1 |
| VLAN 20 | 192.168.20.1 |
| VLAN 30 | 192.168.30.1 |
| VLAN 40 | 192.168.40.1 |
| VLAN 50 | 192.168.50.1 |

Inter-VLAN routing is enabled on the CORE-SW using Switch Virtual Interfaces (SVIs).

---

## DHCP

DHCP services are configured on the CORE-SW for the required client networks.

### OFFICE

- Network: `192.168.10.0/24`
- Default Gateway: `192.168.10.1`
- DNS Server: `192.168.20.10`
- Domain: `company.local`

### WIFI

- Network: `192.168.40.0/24`
- Default Gateway: `192.168.40.1`
- DNS Server: `192.168.20.10`
- Domain: `company.local`

Infrastructure addresses are excluded from the DHCP pools to prevent IP conflicts.

---

## Firewall & NAT

A Cisco ASA Firewall is used between the internal corporate network and the external network.

The ASA provides:

- Firewall security
- Traffic control
- Network Address Translation (NAT)

The internal connection between the CORE-SW and ASA uses the `10.0.0.0/30` network.

| Device | IP Address |
|--------|------------|
| CORE-SW | 10.0.0.1/30 |
| ASA | 10.0.0.2/30 |

---

## Access Control

An extended ACL is configured to restrict traffic from the WIFI network to the SERVERS network.

- Source: `192.168.40.0/24`
- Destination: `192.168.20.0/24`

The ACL prevents direct access from the wireless network to the server network while permitting other traffic according to the configured policy.

---

## Network Security

The project demonstrates basic enterprise network security concepts:

- VLAN-based network segmentation
- Dedicated server network
- Dedicated printer network
- Dedicated wireless network
- Dedicated management VLAN
- Cisco ASA Firewall
- NAT
- Extended ACL
- Separation between internal and external networks

---

## Network Verification

The network configuration and connectivity can be verified using Cisco IOS commands such as:

`show vlan brief`

`show ip interface brief`

`show ip route`

`show ip dhcp pool`

`show access-lists`

Client connectivity can be tested using:

`ipconfig`

`ping`

Testing focuses on VLAN configuration, DHCP operation, routing, ACL behavior and network connectivity.
