# IP Addressing Plan

## LAN Addressing

| Site     | Device     | Interface     | IP Address    | Subnet Mask   |
| -------- | ---------- | ------------- | ------------- | ------------- |
| HQ       | R-HQ       | G0/0          | 192.168.10.1  | 255.255.255.0 |
| HQ       | PC-HQ      | FastEthernet0 | 192.168.10.10 | 255.255.255.0 |
| HQ       | SERVER-01  | FastEthernet0 | 192.168.10.20 | 255.255.255.0 |
| Branch A | R-BRANCH-A | G0/0          | 192.168.20.1  | 255.255.255.0 |
| Branch A | PC-A       | FastEthernet0 | 192.168.20.10 | 255.255.255.0 |
| Branch B | R-BRANCH-B | G0/0          | 192.168.30.1  | 255.255.255.0 |
| Branch B | PC-B       | FastEthernet0 | 192.168.30.10 | 255.255.255.0 |

## Inter-Router Links

| Link                | Router Interface | IP Address   | Subnet      |
| ------------------- | ---------------- | ------------ | ----------- |
| HQ - Branch A       | R-HQ G0/1        | 10.0.0.1/30  | 10.0.0.0/30 |
| HQ - Branch A       | R-BRANCH-A G0/1  | 10.0.0.2/30  | 10.0.0.0/30 |
| HQ - Branch B       | R-HQ G0/2        | 10.0.0.5/30  | 10.0.0.4/30 |
| HQ - Branch B       | R-BRANCH-B G0/1  | 10.0.0.6/30  | 10.0.0.4/30 |
| Branch A - Branch B | R-BRANCH-A G0/2  | 10.0.0.9/30  | 10.0.0.8/30 |
| Branch A - Branch B | R-BRANCH-B G0/2  | 10.0.0.10/30 | 10.0.0.8/30 |

## Default Gateways

| Device    | Default Gateway |
| --------- | --------------- |
| PC-HQ     | 192.168.10.1    |
| SERVER-01 | 192.168.10.1    |
| PC-A      | 192.168.20.1    |
| PC-B      | 192.168.30.1    |

## Routing

- Protocol: OSPF
- Process ID: 1
- Area: 0
- LAN routes are advertised dynamically.
- Inter-router links use /30 subnets.
