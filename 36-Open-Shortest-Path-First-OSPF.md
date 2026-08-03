# Open Shortest Path First (OSPF)

## Introduction

Open Shortest Path First (OSPF) is a dynamic, link-state routing protocol used to exchange routing information within an Autonomous System (AS). It is defined by the Internet Engineering Task Force (IETF) in **RFC 2328** and is one of the most widely deployed Interior Gateway Protocols (IGPs) in enterprise networks.

Unlike RIP, which uses Hop Count as its routing metric, OSPF uses **Cost**, calculated primarily based on interface bandwidth. OSPF converges much faster than Distance Vector protocols and supports hierarchical network design through Areas, making it highly scalable and efficient.

OSPF operates directly over IP using **Protocol Number 89** and does not use TCP or UDP.

---

# Objectives

This document covers:

- Introduction to OSPF
- Why OSPF is Required
- Link-State Routing
- OSPF Characteristics
- Router ID
- OSPF Areas
- DR and BDR Election
- OSPF Neighbor States
- OSPF Metrics
- Cisco Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is OSPF?

Open Shortest Path First (OSPF) is a Link-State Routing Protocol that dynamically discovers network topology and calculates the shortest path using the **Shortest Path First (SPF)** algorithm developed by Edsger Dijkstra.

Each router builds a complete map of the network and independently calculates the best route to every destination.

---

# Why OSPF is Required

Without OSPF

- Manual routing configuration
- Slow network convergence
- Poor scalability
- Difficult administration

With OSPF

- Automatic route learning
- Fast convergence
- Efficient routing
- High scalability
- Load balancing support

---

# Link-State Routing

Unlike Distance Vector protocols, OSPF exchanges **Link-State Advertisements (LSAs)** instead of complete routing tables.

Every router maintains:

- Neighbor Table
- Link-State Database (LSDB)
- Routing Table

Each router independently calculates the shortest path.

---

# OSPF Metric

OSPF uses **Cost** as its routing metric.

Formula

```
Cost = Reference Bandwidth / Interface Bandwidth
```

Example

| Interface Speed | Cost |
|-----------------|------|
|10 Mbps|10|
|100 Mbps|1|
|1 Gbps|1 (default reference bandwidth)|

Lower Cost = Better Route

---

# Router ID (RID)

Every OSPF router requires a unique **Router ID**.

Selection Order

1. Manually configured Router ID
2. Highest Loopback IP Address
3. Highest Active Physical Interface IP

Example

```
1.1.1.1
```

---

# OSPF Areas

Large OSPF networks are divided into **Areas**.

Benefits

- Reduces routing updates
- Improves scalability
- Faster convergence
- Smaller routing tables

---

## Backbone Area

```
Area 0
```

All other OSPF areas must connect to Area 0.

---

## Regular Area

Contains internal routers connected to Area 0.

Example

```
Area 1

Area 2

Area 3
```

---

# OSPF Router Types

## Internal Router

All interfaces belong to the same area.

---

## Backbone Router

Connected directly to Area 0.

---

## Area Border Router (ABR)

Connects multiple OSPF areas.

---

## Autonomous System Boundary Router (ASBR)

Redistributes routes from another routing protocol into OSPF.

---

# DR and BDR

On multi-access networks, OSPF elects:

- Designated Router (DR)
- Backup Designated Router (BDR)

Purpose

- Reduce LSA traffic
- Improve efficiency

Election Criteria

1. Highest OSPF Priority
2. Highest Router ID

Default Priority

```
1
```

---

# OSPF Neighbor States

Common Neighbor States

- Down
- Init
- Two-Way
- ExStart
- Exchange
- Loading
- Full

A **Full** state indicates successful adjacency.

---

# OSPF Packet Types

| Packet | Purpose |
|----------|----------|
| Hello | Discover Neighbors |
| Database Description (DBD) | Exchange LSDB Summary |
| Link State Request (LSR) | Request Missing LSAs |
| Link State Update (LSU) | Send LSAs |
| Link State Acknowledgment (LSAck) | Acknowledge LSAs |

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

Each router exchanges Link-State information.

---

# Cisco OSPF Configuration

Enable OSPF

```
Router(config)# router ospf 1
```

Advertise Networks

```
Router(config-router)# network 192.168.1.0 0.0.0.255 area 0

Router(config-router)# network 10.0.0.0 0.0.0.3 area 0
```

Configure Router ID

```
Router(config-router)# router-id 1.1.1.1
```

---

# Complete Example

```
enable

configure terminal

router ospf 1

router-id 1.1.1.1

network 192.168.1.0 0.0.0.255 area 0

network 10.0.0.0 0.0.0.3 area 0
```

---

# Verification Commands

Display Routing Table

```
show ip route
```

Display OSPF Neighbor

```
show ip ospf neighbor
```

Display OSPF Interface

```
show ip ospf interface
```

Display OSPF Database

```
show ip ospf database
```

Display OSPF Configuration

```
show ip protocols
```

---

# Example Routing Table

```
O 192.168.2.0/24

[110/2]

via 10.0.0.2
```

Where

- O = OSPF Route
- 110 = Administrative Distance
- 2 = OSPF Cost

---

# Advantages

- Fast convergence
- Scalable architecture
- Supports VLSM and CIDR
- Efficient bandwidth utilization
- Loop-free routing
- Supports Equal Cost Load Balancing
- Open standard protocol

---

# Limitations

- More complex than RIP
- Requires greater CPU and memory
- Proper area design is necessary
- Initial configuration is more involved

---

# OSPF vs RIP

| Feature | RIP | OSPF |
|----------|-----|------|
| Routing Type | Distance Vector | Link-State |
| Metric | Hop Count | Cost |
| Convergence | Slow | Fast |
| Maximum Network Size | Small | Very Large |
| Updates | Every 30 Seconds | Triggered Updates |
| Administrative Distance | 120 | 110 |

---

# Best Practices

- Always use Area 0 as the backbone.
- Configure Router IDs manually.
- Keep Area 0 stable.
- Use Loopback interfaces for Router IDs.
- Verify neighbor relationships after configuration.
- Design hierarchical OSPF areas for large networks.
- Document Area IDs and Router IDs.

---

# Important Notes

- OSPF stands for **Open Shortest Path First**.
- OSPF is a **Link-State Routing Protocol**.
- Uses **Cost** as its routing metric.
- Uses the **Shortest Path First (SPF)** algorithm.
- Operates using **IP Protocol Number 89**.
- Default Administrative Distance is **110**.
- Area 0 is the Backbone Area.
- OSPF supports **CIDR**, **VLSM**, and **Equal Cost Load Balancing**.

---

# Conclusion

Open Shortest Path First (OSPF) is a powerful and scalable Link-State Routing Protocol designed for modern enterprise networks. By using the SPF algorithm, hierarchical area design, and efficient routing updates, OSPF provides fast convergence, optimal path selection, and excellent scalability. Its widespread industry adoption makes it one of the most important routing protocols for network engineers and CCNA/CCNP professionals.
