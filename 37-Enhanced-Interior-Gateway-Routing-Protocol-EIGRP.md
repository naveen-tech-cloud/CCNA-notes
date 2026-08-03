# Enhanced Interior Gateway Routing Protocol (EIGRP)

## Introduction

Enhanced Interior Gateway Routing Protocol (EIGRP) is an advanced dynamic routing protocol developed by Cisco Systems. It combines the advantages of both Distance Vector and Link-State routing protocols, making it a Hybrid Routing Protocol.

EIGRP uses the Diffusing Update Algorithm (DUAL) to calculate the best path to a destination, providing rapid convergence, loop-free routing, and efficient bandwidth utilization. It supports classless routing, unequal-cost load balancing, route summarization, and authentication.

EIGRP is widely used in enterprise networks due to its fast convergence and scalability.

---

# Objectives

This document covers:

- Introduction to EIGRP
- Why EIGRP is Required
- Hybrid Routing
- DUAL Algorithm
- EIGRP Metrics
- Neighbor Discovery
- Feasible Distance
- Reported Distance
- Successor & Feasible Successor
- Cisco Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is EIGRP?

Enhanced Interior Gateway Routing Protocol (EIGRP) is a Cisco-developed advanced routing protocol that automatically exchanges routing information between routers and selects the best available path using the DUAL algorithm.

Unlike RIP, EIGRP supports faster convergence and more efficient routing decisions.

---

# Why EIGRP is Required

Without EIGRP

- Slow convergence
- Limited scalability
- Manual route management
- Inefficient bandwidth usage

With EIGRP

- Fast convergence
- Automatic route learning
- Efficient bandwidth utilization
- Loop-free routing
- Load balancing

---

# Hybrid Routing Protocol

EIGRP combines features of:

- Distance Vector Routing
- Link-State Routing

This combination provides:

- Faster convergence
- Lower bandwidth consumption
- Efficient route calculation

---

# DUAL Algorithm

EIGRP uses the **Diffusing Update Algorithm (DUAL)**.

Functions

- Selects the best path.
- Maintains backup routes.
- Prevents routing loops.
- Provides rapid convergence.

---

# EIGRP Metrics

EIGRP calculates routes using:

- Bandwidth
- Delay

Optional Metrics

- Reliability
- Load
- MTU

Default Formula

```
Metric = Bandwidth + Delay
```

The path with the lowest metric is selected.

---

# Neighbor Discovery

Routers discover neighbors by exchanging Hello Packets.

Default Hello Interval

```
5 Seconds
```

On slower WAN links

```
60 Seconds
```

---

# Successor

The Successor is the primary best route selected by DUAL.

Only one Successor is installed in the routing table unless load balancing is enabled.

---

# Feasible Successor

A Feasible Successor is a backup route that satisfies the Feasibility Condition.

Advantages

- Immediate failover
- No route recalculation
- Faster convergence

---

# Feasible Distance (FD)

The total metric from the local router to the destination.

---

# Reported Distance (RD)

The metric advertised by a neighboring router to reach a destination.

---

# Administrative Distance

| Route Type | Administrative Distance |
|-------------|-------------------------|
| Internal EIGRP | 90 |
| External EIGRP | 170 |

---

# EIGRP Packet Types

| Packet | Purpose |
|----------|----------|
| Hello | Neighbor Discovery |
| Update | Route Information |
| Query | Search for Routes |
| Reply | Respond to Query |
| Acknowledgment | Confirm Updates |

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

Each router exchanges EIGRP routing information.

---

# Cisco EIGRP Configuration

Enable EIGRP

```
Router(config)# router eigrp 100
```

Advertise Networks

```
Router(config-router)# network 192.168.1.0 0.0.0.255

Router(config-router)# network 10.0.0.0 0.0.0.3
```

Disable Automatic Summarization

```
Router(config-router)# no auto-summary
```

---

# Complete Example

```
enable

configure terminal

router eigrp 100

no auto-summary

network 192.168.1.0 0.0.0.255

network 10.0.0.0 0.0.0.3
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

Display Protocol Information

```
show ip protocols
```

Display Running Configuration

```
show running-config
```

---

# Example Routing Table

```
D 192.168.2.0/24

[90/30720]

via 10.0.0.2
```

Where

- D = EIGRP Route
- 90 = Administrative Distance
- 30720 = Metric

---

# Advantages

- Fast convergence
- Loop-free routing
- Supports VLSM and CIDR
- Unequal-cost load balancing
- Efficient bandwidth usage
- Low CPU utilization
- Backup routes available

---

# Limitations

- Originally Cisco proprietary
- More complex than RIP
- Requires memory for topology table
- Proper planning needed for large deployments

---

# EIGRP vs OSPF

| Feature | EIGRP | OSPF |
|----------|-------|------|
| Routing Type | Hybrid | Link-State |
| Algorithm | DUAL | SPF |
| Metric | Bandwidth + Delay | Cost |
| Administrative Distance | 90 | 110 |
| Convergence | Very Fast | Fast |
| Load Balancing | Equal & Unequal Cost | Equal Cost Only |

---

# Best Practices

- Disable automatic summarization.
- Use authentication in enterprise environments.
- Configure passive interfaces where appropriate.
- Monitor neighbor relationships.
- Document Autonomous System (AS) numbers.
- Use route summarization to reduce routing updates.
- Regularly verify the topology table.

---

# Important Notes

- EIGRP stands for **Enhanced Interior Gateway Routing Protocol**.
- EIGRP is a **Hybrid Routing Protocol**.
- Uses the **DUAL Algorithm**.
- Default Administrative Distance is **90** (Internal).
- Supports **VLSM**, **CIDR**, and **Unequal-Cost Load Balancing**.
- Neighbor discovery uses **Hello Packets**.
- Successor is the primary route.
- Feasible Successor is the backup route.

---

# Conclusion

Enhanced Interior Gateway Routing Protocol (EIGRP) is a highly efficient and scalable routing protocol designed for enterprise networks. By combining the strengths of Distance Vector and Link-State protocols, EIGRP delivers rapid convergence, intelligent path selection, and reliable backup routing through the DUAL algorithm. Its advanced features and high performance make it a preferred choice for Cisco-based network infrastructures.
