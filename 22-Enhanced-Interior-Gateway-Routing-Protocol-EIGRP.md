# Enhanced Interior Gateway Routing Protocol (EIGRP)

## Introduction

Enhanced Interior Gateway Routing Protocol (EIGRP) is an advanced dynamic routing protocol developed by Cisco Systems. It is often referred to as a **Hybrid Routing Protocol** because it combines the characteristics of both Distance Vector and Link-State routing protocols.

EIGRP is designed to provide fast convergence, efficient bandwidth utilization, loop-free routing, and excellent scalability. It is widely used in enterprise networks where high performance and reliability are required.

Unlike RIP, which uses Hop Count, and OSPF, which uses Cost, EIGRP selects the best path using a composite metric based on **Bandwidth** and **Delay** by default.

---

# Objectives

This document covers:

- Introduction to EIGRP
- Features of EIGRP
- How EIGRP Works
- EIGRP Terminology
- EIGRP Packet Types
- Metric Calculation
- Configuration
- Verification
- Advantages
- Limitations
- Best Practices

---

# What is EIGRP?

EIGRP (Enhanced Interior Gateway Routing Protocol) is a Cisco proprietary advanced dynamic routing protocol that automatically discovers routes and determines the best path between networks.

It uses the **Diffusing Update Algorithm (DUAL)** to calculate the shortest and loop-free path.

---

# Features of EIGRP

- Hybrid Routing Protocol
- Fast Convergence
- Supports VLSM and CIDR
- Classless Routing Protocol
- Incremental Updates
- Load Balancing
- Loop-Free Routing
- Low Bandwidth Usage
- Automatic Route Summarization (Older Versions)
- Manual Route Summarization Supported

---

# How EIGRP Works

The routing process follows these steps:

1. Routers discover neighboring EIGRP routers.
2. Neighbor relationships are established.
3. Routing information is exchanged.
4. The DUAL algorithm calculates the best route.
5. The routing table is updated automatically.
6. If a route fails, a backup route is used immediately if available.

---

# DUAL Algorithm

DUAL stands for:

**Diffusing Update Algorithm**

It is responsible for:

- Calculating the best route
- Preventing routing loops
- Providing fast convergence
- Selecting backup routes

---

# EIGRP Terminology

## Neighbor

A directly connected router running EIGRP.

---

## Successor

The primary best path to reach a destination.

---

## Feasible Successor

A backup path that can immediately replace the successor if it fails.

---

## Feasible Distance (FD)

The total calculated metric from the local router to the destination.

---

## Reported Distance (RD)

The distance reported by a neighboring router to the destination.

---

# EIGRP Packet Types

EIGRP uses five packet types.

| Packet | Purpose |
|----------|----------|
| Hello | Discover and Maintain Neighbors |
| Update | Send Routing Information |
| Query | Request Route Information |
| Reply | Respond to Query |
| Acknowledgment | Confirm Packet Receipt |

---

# EIGRP Metric

EIGRP calculates its metric using:

- Bandwidth
- Delay

Optional metrics:

- Reliability
- Load
- MTU

Simplified Formula

```
Metric = Bandwidth + Delay
```

Lower Metric = Better Route

---

# Administrative Distance

| Route Type | Administrative Distance |
|------------|-------------------------|
| Connected | 0 |
| Static | 1 |
| EIGRP Summary | 5 |
| Internal EIGRP | 90 |
| External EIGRP | 170 |
| OSPF | 110 |
| RIP | 120 |

---

# Network Topology

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

---

# Basic EIGRP Configuration

## Router R1

```
enable

configure terminal

router eigrp 100

no auto-summary

network 192.168.1.0

network 10.0.12.0
```

---

## Router R2

```
router eigrp 100

no auto-summary

network 10.0.12.0

network 10.0.23.0
```

---

## Router R3

```
router eigrp 100

no auto-summary

network 10.0.23.0

network 192.168.2.0
```

---

# Verification Commands

Display Routing Table

```
show ip route
```

Display EIGRP Neighbors

```
show ip eigrp neighbors
```

Display EIGRP Topology

```
show ip eigrp topology
```

Display Routing Protocol Information

```
show ip protocols
```

Display Running Configuration

```
show running-config
```

---

# Routing Table Example

```
R1# show ip route

D 192.168.2.0/24

C 192.168.1.0/24

C 10.0.12.0/30
```

Legend

- D = EIGRP Route
- C = Connected Route

---

# Advantages

- Very fast convergence
- Efficient bandwidth utilization
- Supports unequal-cost load balancing
- Automatic route updates
- Loop-free routing
- Highly scalable
- Easy troubleshooting
- Supports VLSM and CIDR

---

# Limitations

- Originally Cisco proprietary
- Slightly more complex than RIP
- Higher CPU and memory usage compared to static routing
- Requires proper planning for large deployments

---

# EIGRP vs OSPF

| Feature | EIGRP | OSPF |
|----------|--------|------|
| Protocol Type | Hybrid | Link-State |
| Algorithm | DUAL | Dijkstra SPF |
| Metric | Bandwidth + Delay | Cost |
| Convergence | Very Fast | Fast |
| Load Balancing | Equal & Unequal Cost | Equal Cost Only |
| Complexity | Moderate | Higher |

---

# Best Practices

- Disable auto-summary using `no auto-summary`.
- Use meaningful Autonomous System (AS) numbers.
- Verify neighbor relationships after configuration.
- Monitor routing tables regularly.
- Document network addressing before deployment.
- Implement authentication in production environments.

---

# Important Notes

- EIGRP is a Hybrid Routing Protocol.
- It uses the DUAL algorithm for route calculation.
- Successor is the best route.
- Feasible Successor is the backup route.
- EIGRP uses Bandwidth and Delay as the default metric.
- EIGRP converges faster than RIP and OSPF in many scenarios.
- Internal EIGRP routes have an Administrative Distance of **90**.

---

# Conclusion

Enhanced Interior Gateway Routing Protocol (EIGRP) is a high-performance dynamic routing protocol designed for enterprise networks. With its DUAL algorithm, rapid convergence, efficient route calculation, and support for advanced features such as unequal-cost load balancing, EIGRP provides a reliable and scalable routing solution. Mastering EIGRP is an important step for networking professionals preparing for Cisco certifications and real-world enterprise network administration.
