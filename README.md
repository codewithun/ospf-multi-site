# OSPF Multi-Site Enterprise Network

## Overview

A multi-site enterprise network simulation built with Cisco Packet Tracer. The network connects a headquarters (HQ) and two branch offices using OSPF dynamic routing.

The project demonstrates network segmentation, IP addressing, dynamic route exchange, end-to-end connectivity testing, and routing failover when an inter-router link becomes unavailable.

## Network Topology

The network uses a triangular topology connecting three routers:

- **R-HQ** — Headquarters
- **R-BRANCH-A** — Branch Office A
- **R-BRANCH-B** — Branch Office B

Each site has a local LAN connected through a Cisco 2960 switch. The HQ site also hosts a server.

## Technologies

- Cisco Packet Tracer
- Cisco 2911 routers
- Cisco 2960 switches
- OSPF routing, process ID 1, area 0
- IPv4 addressing and subnetting
- ICMP connectivity testing
- Dynamic routing failover

## IP Addressing Plan

| Network             | Subnet            | Gateway        |
| ------------------- | ----------------- | -------------- |
| HQ LAN              | `192.168.10.0/24` | `192.168.10.1` |
| Branch A LAN        | `192.168.20.0/24` | `192.168.20.1` |
| Branch B LAN        | `192.168.30.0/24` | `192.168.30.1` |
| HQ – Branch A       | `10.0.0.0/30`     | —              |
| HQ – Branch B       | `10.0.0.4/30`     | —              |
| Branch A – Branch B | `10.0.0.8/30`     | —              |

## Routing Configuration

OSPF is configured on all three routers in area 0. Each router advertises its local LAN and directly connected inter-router networks.

OSPF automatically learns remote network routes and can select an alternative path when a link fails.

## Testing and Validation

The following tests have been performed:

- OSPF neighbor adjacencies established between HQ and both branch routers.
- Remote LAN routes learned dynamically through OSPF.
- End-to-end ICMP connectivity verified between HQ and the branch PCs.
- Failover tested by shutting down the direct HQ–Branch A link.
- The route to Branch A changed from metric 2 to metric 3 through Branch B.
- Ping from HQ to Branch A succeeded with 0% packet loss while the direct link was down.

Recovery of the direct HQ–Branch A route is still pending final verification.

## Project Files

- `ospf-multi-site.pkt` — Packet Tracer simulation.
- `configs/` — Router configuration records.
- `docs/` — Addressing plan and testing reports.

## Learning Outcomes

- Designing a multi-site network topology.
- Configuring router interfaces and IPv4 addressing.
- Implementing OSPF dynamic routing.
- Verifying routing tables and neighbor adjacencies.
- Testing network connectivity and routing failover.

## Disclaimer

This project is a simulated learning lab created in Cisco Packet Tracer. It does not represent a production network deployment.
