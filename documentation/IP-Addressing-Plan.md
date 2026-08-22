# IP Addressing Plan

## Corporate Network

| VLAN | Name | Network | Default Gateway | Purpose |
|------|------|---------|-----------------|---------|
| 10 | OFFICE | 192.168.10.0/24 | 192.168.10.1 | Office users |
| 20 | SERVERS | 192.168.20.0/24 | 192.168.20.1 | Internal servers |
| 30 | PRINTERS | 192.168.30.0/24 | 192.168.30.1 | Network printers |
| 40 | WIFI | 192.168.40.0/24 | 192.168.40.1 | Wireless clients |
| 50 | MANAGEMENT | 192.168.50.0/24 | 192.168.50.1 | Network management |
| 60 | DMZ | 192.168.60.0/24 | 192.168.60.1 | DMZ services |

## Infrastructure Links

| Connection | Network | Device A | Device B |
|------------|---------|----------|----------|
| CORE-SW ↔ ASA | 10.0.0.0/30 | 10.0.0.1 | 10.0.0.2 |
| ASA ↔ ISP | 200.1.1.0/30 | 200.1.1.2 | 200.1.1.1 |
| ISP ↔ Internet | 100.100.100.0/30 | 100.100.100.1 | 100.100.100.2 |

## DHCP

DHCP is configured on the CORE-SW for:

- VLAN 10 – OFFICE
- VLAN 40 – WIFI

Infrastructure addresses from `.1` to `.20` are excluded from the DHCP pools.

## DNS

Internal DNS server:

`192.168.20.10`

Domain:

`company.local`

## Routing

The CORE-SW provides Layer 3 routing between internal VLANs.

The default route from the CORE-SW points to:

`10.0.0.2`

The ASA forwards external traffic toward:

`200.1.1.1`

The ISP router uses:

`100.100.100.2`

as its upstream next hop.
