# Dynamic Routing

## Introduction

Dynamic Routing is a routing method in which routers automatically learn, update, and maintain routing information by exchanging routing tables with neighboring routers using routing protocols.

Unlike Static Routing, where routes are manually configured, Dynamic Routing automatically adapts to network topology changes. It is widely used in medium and large enterprise networks because it reduces administrative effort and improves scalability.

---

# Objectives

This document covers:

- Introduction to Dynamic Routing
- How Dynamic Routing Works
- Routing Protocols
- Types of Dynamic Routing Protocols
- Configuration Example
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is Dynamic Routing?

Dynamic Routing is a process in which routers automatically discover remote networks and determine the best path for forwarding packets using routing protocols.

The routers continuously exchange routing information to keep their routing tables updated.

Example:

```
PC1
 |
R1 ------ R2 ------ R3
 |
PC2
```

If a new network is added or a link fails, routers automatically update their routing tables.

---

# Why Dynamic Routing?

Dynamic Routing is preferred because it:

- Automatically discovers networks
- Updates routing tables
- Detects link failures
- Selects the best available path
- Supports large enterprise networks
- Reduces manual configuration

---

# How Dynamic Routing Works

The routing process follows these steps:

1. Routers exchange routing information.
2. Each router builds a routing table.
3. The best path is calculated.
4. Packets are forwarded based on the routing table.
5. If the network changes, routers automatically update routes.

---

# Dynamic Routing Protocols

Dynamic routing uses specialized routing protocols.

Common routing protocols include:

- RIP (Routing Information Protocol)
- OSPF (Open Shortest Path First)
- EIGRP (Enhanced Interior Gateway Routing Protocol)
- IS-IS (Intermediate System to Intermediate System)
- BGP (Border Gateway Protocol)

---

# Types of Routing Protocols

## Distance Vector Routing

Distance Vector protocols determine the best path based on distance.

Characteristics:

- Simple configuration
- Periodic routing updates
- Suitable for small networks

Example:

- RIP

---

## Link-State Routing

Link-State protocols maintain a complete map of the network topology.

Characteristics:

- Fast convergence
- Efficient routing
- Scalable

Example:

- OSPF
- IS-IS

---

## Hybrid Routing

Hybrid protocols combine features of both Distance Vector and Link-State routing.

Example:

- EIGRP

Characteristics:

- Fast convergence
- Efficient bandwidth usage
- High scalability

---

# Comparison of Routing Protocols

| Protocol | Type | Metric | Maximum Hops |
|----------|------|---------|--------------|
| RIP | Distance Vector | Hop Count | 15 |
| OSPF | Link-State | Cost | Unlimited |
| EIGRP | Hybrid | Bandwidth + Delay | Unlimited |
| BGP | Path Vector | AS Path | Internet Scale |

---

# Example Network

```
LAN A

192.168.1.0/24

      |

     R1

      |

     R2

      |

     R3

      |

LAN B

192.168.2.0/24
```

Routers exchange routing information automatically.

No manual static routes are required.

---

# Basic RIP Configuration Example

Router R1

```
router rip

version 2

network 192.168.1.0

network 10.0.12.0

no auto-summary
```

Router R2

```
router rip

version 2

network 10.0.12.0

network 10.0.23.0

no auto-summary
```

Router R3

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

Display Routing Protocol Information

```
show ip protocols
```

Display Running Configuration

```
show running-config
```

Display Interface Status

```
show ip interface brief
```

Test Connectivity

```
ping
```

Trace Packet Path

```
traceroute
```

---

# Routing Table Example

```
R1# show ip route

R 192.168.2.0/24

C 192.168.1.0/24

C 10.0.12.0/30
```

Legend

- C = Connected Route
- R = RIP Learned Route
- O = OSPF Route
- D = EIGRP Route
- B = BGP Route
- S = Static Route

---

# Advantages

- Automatic route learning
- Automatic route updates
- Better scalability
- Supports large enterprise networks
- Reduces administrative workload
- Automatic failure recovery
- Efficient path selection

---

# Limitations

- Higher CPU utilization
- More memory usage
- Initial configuration is more complex
- Routing updates consume bandwidth
- Requires understanding of routing protocols

---

# Dynamic Routing vs Static Routing

| Feature | Static Routing | Dynamic Routing |
|----------|---------------|-----------------|
| Configuration | Manual | Automatic |
| Scalability | Low | High |
| Maintenance | Difficult | Easy |
| Network Changes | Manual Updates | Automatic Updates |
| CPU Usage | Low | Higher |
| Best For | Small Networks | Medium & Large Networks |

---

# Best Practices

- Use Dynamic Routing in enterprise environments.
- Select the routing protocol based on network size.
- Regularly monitor routing tables.
- Keep router software updated.
- Document routing protocol configurations.
- Verify routing information after configuration changes.

---

# Important Notes

- Dynamic Routing automatically learns routes.
- Routing protocols exchange routing information.
- Dynamic Routing is recommended for medium and large networks.
- RIP, OSPF, EIGRP, and BGP are commonly used routing protocols.
- Dynamic Routing reduces manual configuration and improves scalability.

---

# Conclusion

Dynamic Routing enables routers to automatically discover, exchange, and maintain routing information, making it an efficient solution for modern enterprise networks. By adapting to network changes without manual intervention, dynamic routing improves scalability, reliability, and overall network performance. Understanding dynamic routing is essential before learning individual routing protocols such as RIP, OSPF, EIGRP, and BGP.
