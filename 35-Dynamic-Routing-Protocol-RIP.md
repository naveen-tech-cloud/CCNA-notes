# Routing Information Protocol (RIP)

## Introduction

Routing Information Protocol (RIP) is one of the oldest dynamic routing protocols used in IP networks. It automatically exchanges routing information between routers, enabling them to learn and maintain the best available paths to remote networks.

RIP is a Distance Vector Routing Protocol that uses **Hop Count** as its routing metric. It is simple to configure and suitable for small to medium-sized networks but is not recommended for large enterprise environments due to its scalability limitations.

RIP operates at the **Application Layer (OSI Layer 7)** and uses the **User Datagram Protocol (UDP) Port 520** for communication.

---

# Objectives

This document covers:

- Introduction to RIP
- Why RIP is Required
- Distance Vector Routing
- RIP Characteristics
- Hop Count
- RIP Versions
- Routing Updates
- Timers
- Cisco Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is RIP?

Routing Information Protocol (RIP) is a dynamic routing protocol that enables routers to automatically exchange routing information.

Instead of manually configuring routes, routers running RIP share network information with neighboring routers.

Example

```
Router A

↓

Router B

↓

Router C

↓

Remote Network
```

Each router learns routes automatically.

---

# Why RIP is Required

Without RIP

- Manual route configuration
- Difficult maintenance
- Time-consuming
- Higher administrative effort

With RIP

- Automatic route learning
- Dynamic updates
- Easy implementation
- Simplified network administration

---

# Distance Vector Routing

RIP belongs to the **Distance Vector** routing protocol family.

Each router shares its routing table with directly connected neighbors.

Routing decisions are based on:

- Distance (Hop Count)
- Direction (Next-Hop Router)

---

# Hop Count

Hop Count is the number of routers a packet passes through to reach its destination.

Example

```
PC

↓

Router1

↓

Router2

↓

Router3

↓

Server
```

Hop Count = **3**

---

# Maximum Hop Count

| Hop Count | Status |
|-----------|--------|
| 1–15 | Reachable |
| 16 | Unreachable |

A route with a hop count of **16** is considered unreachable.

---

# RIP Versions

## RIP Version 1 (RIPv1)

Features

- Classful routing
- No subnet mask information
- No authentication
- Broadcast updates

---

## RIP Version 2 (RIPv2)

Features

- Classless routing (CIDR & VLSM support)
- Authentication support
- Multicast updates
- Supports route summarization

Recommended Version

```
RIPv2
```

---

# Routing Updates

RIP sends its complete routing table to neighboring routers every:

```
30 Seconds
```

Updates are sent using:

```
UDP Port 520
```

---

# RIP Timers

| Timer | Default Value |
|--------|---------------|
| Update Timer | 30 Seconds |
| Invalid Timer | 180 Seconds |
| Hold-down Timer | 180 Seconds |
| Flush Timer | 240 Seconds |

---

# Administrative Distance

Default Administrative Distance for RIP:

```
120
```

Lower values are preferred over higher values when multiple routing protocols are available.

---

# Routing Metric

RIP uses only one metric:

```
Hop Count
```

The route with the lowest hop count is selected.

---

# Example Topology

```
LAN A

↓

Router1

↓

Router2

↓

Router3

↓

LAN B
```

Each router exchanges routing information automatically.

---

# Cisco RIP Configuration

Enable RIP

```
Router(config)# router rip
```

Specify RIP Version

```
Router(config-router)# version 2
```

Disable Auto Summary

```
Router(config-router)# no auto-summary
```

Advertise Networks

```
Router(config-router)# network 192.168.1.0

Router(config-router)# network 10.0.0.0
```

---

# Complete Example

```
enable

configure terminal

router rip

version 2

no auto-summary

network 192.168.1.0

network 10.0.0.0
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

---

# Example Routing Table

```
R 192.168.2.0/24

[120/1]

via 10.0.0.2
```

Where:

- R = RIP Route
- 120 = Administrative Distance
- 1 = Hop Count

---

# Advantages

- Simple configuration
- Automatic route learning
- Low resource requirements
- Suitable for small networks
- Easy troubleshooting
- Vendor interoperability (RIPv2)

---

# Limitations

- Maximum hop count of 15
- Slow convergence
- Periodic updates consume bandwidth
- Not suitable for large enterprise networks
- Limited scalability
- Less efficient than OSPF or EIGRP

---

# RIP Version 1 vs Version 2

| Feature | RIPv1 | RIPv2 |
|----------|--------|--------|
| Routing Type | Classful | Classless |
| VLSM Support | No | Yes |
| Authentication | No | Yes |
| Updates | Broadcast | Multicast |
| CIDR Support | No | Yes |

---

# Best Practices

- Use RIPv2 instead of RIPv1.
- Disable auto-summary in modern networks.
- Use authentication where supported.
- Avoid RIP in large enterprise environments.
- Monitor routing updates regularly.
- Document advertised networks.
- Prefer OSPF or EIGRP for scalable networks.

---

# Important Notes

- RIP stands for **Routing Information Protocol**.
- RIP is a **Distance Vector Routing Protocol**.
- Uses **Hop Count** as its routing metric.
- Maximum hop count is **15**.
- Hop count **16** means the network is unreachable.
- Uses **UDP Port 520**.
- Sends routing updates every **30 seconds**.
- Default Administrative Distance is **120**.
- RIPv2 supports **CIDR**, **VLSM**, and **Authentication**.

---

# Conclusion

Routing Information Protocol (RIP) is a simple and widely recognized dynamic routing protocol that automatically exchanges routing information between routers. While its ease of configuration makes it ideal for learning and small-scale deployments, its limited hop count and slow convergence make it less suitable for modern enterprise environments. Understanding RIP provides a strong foundation for learning advanced routing protocols such as OSPF, EIGRP, and BGP.
