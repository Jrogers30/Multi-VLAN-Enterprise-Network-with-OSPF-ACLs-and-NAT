# Multi-VLAN Enterprise Network with OSPF, ACLs, and NAT

## Overview
This project demonstrates a small enterprise network that uses internal routing, access control, and network address translation to provide secure connectivity to an external network.

The design separates internal VLAN routing from edge connectivity, following common enterprise best practices.

---

## Network Purpose
The network represents a small enterprise environment where internal departments require routed connectivity while accessing external resources through a controlled edge router.

---

## Topology Design
The network uses a layered design:


<img width="583" height="413" alt="Screenshot 2025-12-19 131640" src="https://github.com/user-attachments/assets/ed41d663-8611-491e-940c-5445f121d8c0" />



- End devices connect to a Layer 3 switch
- The Layer 3 switch provides VLAN gateways and internal routing
- An edge router handles NAT and external connectivity
- A simulated ISP router represents the external network

All VLANs terminate at the Layer 3 switch, and no Layer 2 traffic extends beyond the LAN.

---

## VLAN and IP Addressing

| VLAN | Purpose | Subnet | Gateway |
|-----|--------|--------|--------|
| 10 | IT | 10.10.10.0/24 | 10.10.10.1 |
| 20 | Users | 10.10.20.0/24 | 10.10.20.1 |

Transit network between the Layer 3 switch and edge router uses a point-to-point subnet.

---

## Routing Design
- OSPF is used for internal routing
- The Layer 3 switch advertises VLAN networks
- The edge router advertises the external network
- Dynamic routing ensures scalability and easier expansion

---

## Security and Traffic Control
- Extended ACLs are used to restrict traffic between internal VLANs
- NAT/PAT is configured on the edge router to allow outbound access
- Internal IP addresses are not exposed to the external network

---

## Configuration Summary
- VLANs and SVIs configured on the Layer 3 switch
- Inter-VLAN routing enabled
- OSPF configured between the Layer 3 switch and edge router
- ACLs applied to control inter-VLAN traffic
- NAT/PAT configured on the edge router
- Default routing provided toward the ISP router

---

## Verification and Testing
The following checks were used to confirm correct operation:

- Verified OSPF neighbor adjacency
- Confirmed routing table entries
- Tested inter-VLAN connectivity
- Verified ACL behavior with allowed and denied traffic
- Confirmed NAT translations for outbound traffic

Example verification commands:
show ip route
show ip ospf neighbor
show access-lists
show ip nat translations


---

## Design Decisions
- Routing is centralized on the Layer 3 switch for internal networks
- NAT is limited to the edge router to maintain clear boundaries
- OSPF is used instead of static routing for flexibility
- ACLs are applied close to the source for better control
