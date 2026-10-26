# OSPF Failover Test

## Objective

Verify that OSPF can reroute traffic through an alternate path when the direct connection between HQ and Branch A becomes unavailable.

## Topology

The network uses three routers connected in a triangle:

- R-HQ ↔ R-BRANCH-A
- R-HQ ↔ R-BRANCH-B
- R-BRANCH-A ↔ R-BRANCH-B

The alternate path from HQ to Branch A passes through R-BRANCH-B.

## Test Procedure

### 1. Disable the Direct Link

On R-HQ:

```text
configure terminal
interface GigabitEthernet0/1
shutdown
end
```

### 2. Verify the Alternate Route

```text
show ip route 192.168.20.0
```

The route to `192.168.20.0/24` switched to the next hop `10.0.0.6` through GigabitEthernet0/2, with metric 3.

### 3. Test Connectivity During Failover

From PC-HQ:

```text
ping 192.168.20.10
```

Result: 4 packets sent, 4 received, 0% packet loss.

This confirmed that PC-HQ could still reach PC-A through the alternate path while the direct link was unavailable.

### 4. Restore the Direct Link

On R-HQ:

```text
configure terminal
interface GigabitEthernet0/1
no shutdown
end
```

### 5. Verify Recovery

Commands:

```text
show ip interface brief
show ip ospf neighbor
show ip route 192.168.20.0
```

Observed results:

- GigabitEthernet0/1 returned to `up/up`.
- The OSPF neighbor at `10.0.0.2` returned to `FULL/DR`.
- The route to `192.168.20.0/24` returned to next hop `10.0.0.2` with metric 2.

## Conclusion

The failover test succeeded. OSPF dynamically redirected traffic through the alternate route when the direct HQ–Branch A link was disabled. After the link was restored, OSPF re-established the adjacency and selected the lower-cost direct route again.
