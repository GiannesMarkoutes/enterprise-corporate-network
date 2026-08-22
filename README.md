# Enterprise Network Project

Cisco Packet Tracer project based on a small enterprise network with VLAN segmentation, Layer 3 routing, ASA firewall, DHCP, NAT/PAT and basic network security.

## Network

The network is divided into separate VLANs:

| VLAN | Name       | Network         | Gateway         |
| ---- | ---------- | --------------- | --------------- |
| 10   | OFFICE     | 192.168.10.0/24 | 192.168.10.1    |
| 20   | SERVERS    | 192.168.20.0/24 | 192.168.20.1    |
| 30   | PRINTERS   | 192.168.30.0/24 | 192.168.30.1    |
| 40   | WIFI       | 192.168.40.0/24 | 192.168.40.1    |
| 50   | MANAGEMENT | 192.168.50.0/24 | 192.168.50.1    |
| 60   | DMZ        | 192.168.60.0/24 | Layer 2 segment |

The CORE-SW handles the inter-VLAN routing.

The connection between the CORE-SW and the ASA uses:

* CORE-SW: `10.0.0.1/30`
* ASA: `10.0.0.2/30`

The CORE-SW uses the ASA as its default route.

## DHCP

DHCP is configured on the CORE-SW for the Office and Wi-Fi networks.

Office:

`192.168.10.0/24`

Wi-Fi:

`192.168.40.0/24`

The DHCP configuration also provides the internal DNS server `192.168.20.10` and the domain `company.local`.

## ASA Firewall and NAT

The ASA is used as the firewall between the internal network and the simulated ISP.

Inside:

`10.0.0.2/30`

Outside:

`200.1.1.2/30`

Dynamic NAT/PAT is configured for internal networks.

During testing, NAT translations were generated successfully:

```text
translate_hits = 58
untranslate_hits = 54
```

## Security

The following security features were configured on the CORE-SW:

* SSH version 2
* SSH access restricted to VLAN 50
* Standard management ACL
* Wi-Fi ACL
* Port Security with sticky MAC addresses
* Port Security violation restrict
* PortFast
* BPDU Guard

The Wi-Fi ACL blocks clients from VLAN 40 from directly accessing the Server VLAN:

```text
deny ip 192.168.40.0 0.0.0.255 192.168.20.0 0.0.0.255
permit ip any any
```

## Routing

The CORE-SW has a default route towards the ASA:

```text
0.0.0.0/0 via 10.0.0.2
```

The ISP has static routes towards the internal enterprise networks through the ASA.

## Verification

The configuration was checked using:

```text
show vlan brief
show ip interface brief
show ip route
show ip dhcp pool
show ip access-lists
show port-security
show ip ssh
show xlate
show nat
```

The command outputs and verification notes are included in the `verification` folder.

Screenshots of the main configuration and verification steps are available in the `screenshots` folder.

## Packet Tracer Limitation

The ASA available in Packet Tracer has a license limitation regarding the number of active named interfaces.

Because of this, VLAN 60 was kept as a Layer 2 DMZ segment on the CORE-SW instead of configuring it as a third fully active ASA security zone.

The VLAN 60 SVI therefore has no IP address and is administratively disabled.

The simulated Internet section also has limitations compared with a real ISP connection, but the internal routing, ASA connectivity and NAT/PAT operation were verified.

## Project Structure

```text
Enterprise-Network/
├── README.md
├── Enterprise-Network.pkt
├── configurations/
├── verification/
└── screenshots/
```

## Technologies

* Cisco Packet Tracer
* Cisco IOS
* Cisco ASA
* VLANs
* Layer 3 Switching
* Inter-VLAN Routing
* Static Routing
* DHCP
* NAT/PAT
* ACLs
* SSH
* Port Security
* Spanning Tree / BPDU Guard
