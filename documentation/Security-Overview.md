# Security Overview

## Security Architecture

The network uses multiple security mechanisms to protect internal resources and control network access.

Security is implemented at different layers, including network segmentation, firewall protection, access control and secure device management.

## VLAN Segmentation

The network is divided into dedicated VLANs:

- VLAN 10 – OFFICE
- VLAN 20 – SERVERS
- VLAN 30 – PRINTERS
- VLAN 40 – WIFI
- VLAN 50 – MANAGEMENT
- VLAN 60 – DMZ

This segmentation reduces unnecessary communication between network segments and provides a more structured enterprise network architecture.

## Cisco ASA Firewall

The Cisco ASA acts as the perimeter firewall between the internal corporate network and the external network.

The ASA provides:

- Firewall security
- Traffic filtering
- NAT
- Separation of internal and external networks
- Routing toward the external network

The internal ASA interface uses:

`10.0.0.2/30`

The external ASA interface uses:

`200.1.1.2/30`

## Network Address Translation

NAT is configured on the ASA to translate internal network addresses when communicating with the external network.

Dynamic interface PAT is used for internal networks.

This allows multiple internal hosts to share the external ASA address when accessing external resources.

## Access Control Lists

Access Control Lists are used to control network traffic.

An extended ACL is intended to restrict traffic between the wireless network and the server network.

Source network:

`192.168.40.0/24`

Destination network:

`192.168.20.0/24`

The purpose of this policy is to prevent unrestricted direct access from wireless clients to internal server resources.

## Secure Management

The CORE-SW is configured for secure remote management using SSH.

SSH version 2 is enabled.

Management access is controlled using the:

`SSH-MANAGEMENT`

standard access list.

The management network is:

`192.168.50.0/24`

Only hosts from the management network are permitted to access the switch through the configured VTY lines.

## Port Security

Port security is enabled on selected access ports.

The configuration includes:

- Sticky MAC address learning
- MAC address restrictions
- Violation restriction

This helps prevent unauthorized devices from being connected to protected access ports.

## Layer 2 Protection

Additional Layer 2 security mechanisms are configured on access ports.

### PortFast

PortFast is enabled on appropriate end-device access ports to allow connected hosts to transition quickly to the forwarding state.

### BPDU Guard

BPDU Guard is enabled on selected access ports to protect against unexpected spanning-tree BPDUs.

## Management Network

A dedicated management VLAN is used:

`VLAN 50 – MANAGEMENT`

Network:

`192.168.50.0/24`

Separating management traffic from normal user traffic improves administrative control and network organization.

## DMZ

A dedicated DMZ network is configured:

`VLAN 60 – DMZ`

Network:

`192.168.60.0/24`

The DMZ is intended to isolate services that may require controlled exposure from the internal corporate networks.

## Security Objectives

The main security objectives of the project are:

1. Separate different types of network traffic.
2. Protect internal resources from unauthorized access.
3. Control communication between network segments.
4. Secure network device management.
5. Protect access ports from unauthorized devices.
6. Provide perimeter firewall protection.
7. Provide controlled external connectivity.
8. Isolate DMZ services from internal networks.

## Verification

Security configuration can be reviewed using commands such as:

    show access-lists
    show port-security
    show vlan brief
    show running-config
    show ip interface brief

Connectivity and access-control behavior can be tested using:

    ping
    ipconfig

The results should be compared with the intended network security policy.
