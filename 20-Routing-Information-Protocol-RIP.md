# Routing Information Protocol (RIP)

## Introduction

Routing Information Protocol (RIP) is one of the oldest and simplest dynamic routing protocols used in IP networks. It is a **Distance Vector Routing Protocol** that determines the best path based on the number of hops between the source and destination networks.

RIP automatically exchanges routing information between routers at regular intervals, allowing routers to learn remote networks without manual configuration.

Although RIP has largely been replaced by more advanced routing protocols such as OSPF and EIGRP in enterprise environments, it remains an excellent protocol for learning the fundamentals of dynamic routing.

---

# Objectives

This document covers:

- Introduction to RIP
- Features of RIP
- How RIP Works
- RIP Versions
- RIP Metric
- RIP Timers
- Configuration
- Verification
- Advantages
- Limitations
- Best Practices

---

# What is RIP?

Routing Information Protocol (RIP) is a dynamic routing protocol that uses **Hop Count** as its routing metric.

The router selects the path with the lowest hop count.

Example:

```
PC1
 |
R1 ----- R2 ----- R3
 |
PC2
```

If R1 wants to reach a network connected to R3, RIP calculates the route based on the number of routers (hops) between them.

---

# Features of RIP

- Distance Vector Routing Protocol
- Uses Hop Count as Metric
- Maximum Hop Count = 15
- Hop Count 16 = Unreachable Network
- Automatic Route Exchange
- Simple Configuration
- Supports Classless Routing (RIPv2)

---

# How RIP Works

The routing process follows these steps:

1. Routers advertise their routing tables every 30 seconds.
2. Neighboring routers receive the updates.
3. Routers update their routing tables.
4. The route with the lowest hop count is selected.
5. If a route becomes unavailable, RIP updates the routing table automatically.

---

# RIP Versions

## RIP Version 1 (RIPv1)

Characteristics:

- Classful Routing Protocol
- Does not support VLSM
- Does not send subnet mask information
- Broadcast Updates
- Obsolete

---

## RIP Version 2 (RIPv2)

Characteristics:

- Classless Routing Protocol
- Supports VLSM
- Supports CIDR
- Multicast Updates
- Authentication Support
- Most commonly used RIP version

---

# RIP Metric

RIP uses **Hop Count** as its metric.

| Hop Count | Status |
|-----------|---------|
| 1 | Best Route |
| 5 | Reachable |
| 10 | Reachable |
| 15 | Maximum Reachable |
| 16 | Unreachable |

---

# RIP Timers

| Timer | Default Value |
|--------|---------------|
| Update Timer | 30 Seconds |
| Invalid Timer | 180 Seconds |
| Hold-down Timer | 180 Seconds |
| Flush Timer | 240 Seconds |

These timers help routers maintain accurate routing information.

---

# Network Topology

```
LAN A
192.168.1.0/24
     |
    R1
10.0.12.1
     |
10.0.12.2
    R2
10.0.23.1
     |
10.0.23.2
    R3
     |
192.168.2.0/24
LAN B
```

---

# RIP Configuration

## Configure Router R1

```
enable

configure terminal

router rip

version 2

network 192.168.1.0

network 10.0.12.0

no auto-summary
```

---

## Configure Router R2

```
router rip

version 2

network 10.0.12.0

network 10.0.23.0

no auto-summary
```

---

## Configure Router R3

```
router rip

version 2

network 10.0.23.0

network 192.168.2.0

no auto-summary
```

---

# Verification Commands

Display Routing Table

```
show ip route
```

Display RIP Information

```
show ip protocols
```

Display Running Configuration

```
show running-config
```

Display RIP Database

```
show ip rip database
```

Verify Interface Status

```
show ip interface brief
```

---

# Routing Table Example

```
R1# show ip route

R 192.168.2.0/24

C 192.168.1.0/24

C 10.0.12.0/30
```

Legend:

- **R** = RIP Learned Route
- **C** = Connected Route

---

# Advantages

- Easy to configure
- Automatic route updates
- Suitable for small networks
- Low administrative effort
- Good for learning routing concepts

---

# Limitations

- Maximum hop count is 15
- Slow convergence
- Not suitable for large networks
- Periodic updates consume bandwidth
- Less efficient than OSPF and EIGRP

---

# RIP vs Static Routing

| Feature | Static Routing | RIP |
|----------|----------------|-----|
| Route Learning | Manual | Automatic |
| Scalability | Low | Moderate |
| Updates | Manual | Automatic |
| Metric | None | Hop Count |
| Suitable For | Small Stable Networks | Small to Medium Networks |

---

# Best Practices

- Use **RIPv2** instead of RIPv1.
- Disable auto-summary using `no auto-summary`.
- Verify routing tables after configuration.
- Document network addresses before enabling RIP.
- Use RIP only in small networks or learning environments.

---

# Important Notes

- RIP is a **Distance Vector Routing Protocol**.
- RIP uses **Hop Count** as its routing metric.
- Maximum hop count is **15**.
- Hop count **16** indicates an unreachable network.
- RIPv2 supports **VLSM** and **CIDR**.
- RIP sends routing updates every **30 seconds**.

---

# Conclusion

Routing Information Protocol (RIP) is a simple and widely recognized dynamic routing protocol that automatically exchanges routing information between routers. While it is limited by its hop count and scalability, RIP remains an excellent protocol for understanding the fundamentals of dynamic routing. Learning RIP provides a solid foundation before moving to more advanced routing protocols such as OSPF, EIGRP, and BGP.
