# Connectivity Test

## Objective

Verify OSPF neighbor formation, inter-site routing, and end-to-end connectivity between devices across the HQ and branch networks.

## Test Results

| No. | Test                            | Expected Result                             | Status |
| --- | ------------------------------- | ------------------------------------------- | ------ |
| 1   | OSPF neighbor formation on R-HQ | Both branch routers reach FULL state        | PASS   |
| 2   | PC-HQ to PC-A ping              | Successful connectivity                     | PASS   |
| 3   | PC-HQ to PC-B ping              | Successful connectivity                     | PASS   |
| 4   | Routing table on R-HQ           | Remote branch LANs learned through OSPF     | PASS   |
| 5   | Recovery of HQ–Branch A link    | OSPF adjacency and preferred route restored | PASS   |

## Verification Commands

Commands used on the routers:

```text
show ip interface brief
show ip ospf neighbor
show ip route
show ip route 192.168.20.0
show ip route 192.168.30.0
```

Commands used on the PCs:

```text
ping 192.168.20.10
ping 192.168.30.10
```

## Conclusion

The network successfully established OSPF adjacencies and enabled communication between the HQ and both branch LANs. After the HQ–Branch A link was restored, the OSPF adjacency returned to FULL state and the preferred route to the Branch A LAN returned to the direct link with metric 2.
