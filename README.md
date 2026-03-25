# Linux Network Namespace Simulation

## Objective

This project demonstrates how to create isolated network environments using Linux network namespaces, bridges, and routing.

---

## Network Topology

```
ns1 ---- br0 ---- router-ns ---- br1 ---- ns2
```

### With IP Addressing:

```
[ns1: 10.0.1.2]
    |
      (veth)
    |
      [br0]
    |
[router-ns: 10.0.1.1 | 10.0.2.1]
    |
      [br1]
    |
      (veth)
    |
[ns2: 10.0.2.2]
```

---

## IP Addressing Scheme

| Namespace | Interface | IP Address  | Network     |
| --------- | --------- | ----------- | ----------- |
| ns1       | veth-ns1  | 10.0.1.2/24 | 10.0.1.0/24 |
| router-ns | veth-r1   | 10.0.1.1/24 | 10.0.1.0/24 |
| router-ns | veth-r2   | 10.0.2.1/24 | 10.0.2.0/24 |
| ns2       | veth-ns2  | 10.0.2.2/24 | 10.0.2.0/24 |

---

## Implementation Steps

1. Created two bridges: `br0`, `br1`
2. Created namespaces: `ns1`, `ns2`, `router-ns`
3. Connected using veth pairs
4. Assigned IP addresses
5. Enabled IP forwarding in router
6. Configured routing between networks

---

## Routing Configuration

- ns1 default route → `10.0.1.1`
- ns2 default route → `10.0.2.1`
- router-ns has IP forwarding enabled

---

## Testing

### Ping Test:

```bash
ip netns exec ns1 ping 10.0.2.2
```

### Output:

```
64 bytes from 10.0.2.2: icmp_seq=1 ttl=63 time=0.466 ms
```

Successful communication between ns1 and ns2 via router

---

## Scripts

### Setup Script

```bash
./setup.sh
```

### Cleanup Script

```bash
./cleanup.sh
```

---

## Concepts Used

- Network Namespaces
- Linux Bridges
- Virtual Ethernet (veth)
- IP Routing
- IP Forwarding

---

## Conclusion

This project successfully demonstrates network isolation and routing using Linux network namespaces. Full connectivity between two isolated networks was achieved through a router namespace.

---
