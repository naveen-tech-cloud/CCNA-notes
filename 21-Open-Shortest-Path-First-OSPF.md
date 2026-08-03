# Open Shortest Path First (OSPF)

## Introduction

Open Shortest Path First (OSPF) is a **Link-State Dynamic Routing Protocol** developed to overcome the limitations of RIP. It is one of the most widely used Interior Gateway Protocols (IGPs) in enterprise networks due to its fast convergence, scalability, and efficient route calculation.

OSPF uses the **Shortest Path First (SPF)** algorithm, also known as **Dijkstra's Algorithm**, to calculate the best path to a destination. Unlike RIP, OSPF uses **Cost** as its routing metric instead of hop count.

---

# Objectives

This document covers:

- Introduction to OSPF
- Features of OSPF
- How OSPF Works
- OSPF Terminology
- OSPF Packet Types
- OSPF Areas
- OSPF Metric (Cost)
- Configuration
- Verification
- Advantages
- Limitations
- Best Practices

---

# What is OSPF?

OSPF (Open Shortest Path First) is a **Link-State Routing Protocol** used to exchange routing information within an autonomous system.

Instead of sending the entire routing table periodically, OSPF sends updates only when network topology changes occur, making it more efficient than RIP.

---

# Features of OSPF

- Link-State Routing Protocol
- Uses SPF (Dijkstra) Algorithm
- Fast Convergence
- Supports VLSM and CIDR
- Supports Authentication
- Supports Load Balancing
- Hierarchical Network Design
- Uses Cost as Metric
- Classless Routing Protocol

---

# How OSPF Works

OSPF follows these steps:

1. Routers discover neighboring OSPF routers.
2. Neighbor relationships are established.
3. Routers exchange Link-State Advertisements (LSAs).
4. Each router builds a Link-State Database (LSDB).
5. The SPF algorithm calculates the shortest path.
6. The routing table is updated automatically.

---

# OSPF Terminology

### Router ID (RID)

A unique identifier assigned to every OSPF router.

Example:

```
1.1.1.1
```

---

### Neighbor

A router that exchanges OSPF information with another router.

---

### Adjacency

A full relationship established between OSPF neighbors after successful communication.

---

### Link-State Database (LSDB)

A database containing complete information about the network topology.

---

### SPF Tree

A shortest-path tree calculated using Dijkstra's algorithm.

---

# OSPF Areas

OSPF divides large networks into logical areas.

## Area 0 (Backbone Area)

- Central area
- Mandatory in OSPF
- Connects all other areas

Example:

```
Area 1 ---- Area 0 ---- Area 2
```

---

## Regular Area

Contains normal OSPF routers.

---

## Stub Area

Blocks external routing updates to reduce routing table size.

---

## Totally Stubby Area

Receives only a default route from Area 0.

---

## NSSA (Not So Stubby Area)

Allows limited external routes while functioning as a stub area.

---

# OSPF Packet Types

OSPF uses five packet types.

| Packet | Purpose |
|----------|----------|
| Hello | Discover Neighbors |
| Database Description (DBD) | Exchange Database Summary |
| Link-State Request (LSR) | Request Missing Information |
| Link-State Update (LSU) | Send LSAs |
| Link-State Acknowledgment (LSAck) | Confirm Receipt |

---

# OSPF Metric

OSPF uses **Cost** as its routing metric.

Formula:

```
Cost = Reference Bandwidth / Interface Bandwidth
```

Default Reference Bandwidth

```
100 Mbps
```

Example

| Interface | Cost |
|-----------|------|
| Fast Ethernet | 1 |
| Gigabit Ethernet | 1 (default) |
| Serial | Higher Cost |

Lower Cost = Better Route

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

# Basic OSPF Configuration

## Router R1

```
enable

configure terminal

router ospf 1

network 192.168.1.0 0.0.0.255 area 0

network 10.0.12.0 0.0.0.3 area 0
```

---

## Router R2

```
router ospf 1

network 10.0.12.0 0.0.0.3 area 0

network 10.0.23.0 0.0.0.3 area 0
```

---

## Router R3

```
router ospf 1

network 10.0.23.0 0.0.0.3 area 0

network 192.168.2.0 0.0.0.255 area 0
```

---

# Verification Commands

Display Routing Table

```
show ip route
```

Display OSPF Neighbors

```
show ip ospf neighbor
```

Display OSPF Database

```
show ip ospf database
```

Display OSPF Interface

```
show ip ospf interface
```

Display OSPF Configuration

```
show ip protocols
```

---

# Routing Table Example

```
R1# show ip route

O 192.168.2.0/24

C 192.168.1.0/24

C 10.0.12.0/30
```

Legend

- O = OSPF Route
- C = Connected Route

---

# Advantages

- Fast convergence
- Efficient bandwidth usage
- Supports large enterprise networks
- Supports VLSM and CIDR
- Scalable architecture
- Supports authentication
- Hierarchical routing using areas

---

# Limitations

- More complex than RIP
- Higher CPU and memory usage
- Requires proper area planning
- Initial configuration is more detailed

---

# OSPF vs RIP

| Feature | RIP | OSPF |
|----------|-----|------|
| Protocol Type | Distance Vector | Link-State |
| Metric | Hop Count | Cost |
| Maximum Hops | 15 | Unlimited |
| Convergence | Slow | Fast |
| Scalability | Small Networks | Large Networks |
| Updates | Every 30 Seconds | Only on Topology Changes |

---

# Best Practices

- Always use Area 0 as the backbone.
- Assign meaningful Router IDs.
- Keep network documentation updated.
- Verify neighbor relationships after configuration.
- Monitor OSPF status regularly.
- Use authentication in production environments.

---

# Important Notes

- OSPF is a Link-State Routing Protocol.
- OSPF uses Dijkstra's SPF Algorithm.
- OSPF uses Cost as its routing metric.
- Area 0 is mandatory in multi-area OSPF networks.
- OSPF converges much faster than RIP.
- OSPF supports VLSM, CIDR, and authentication.

---

# Conclusion

Open Shortest Path First (OSPF) is one of the most powerful and widely deployed dynamic routing protocols in enterprise networking. Its fast convergence, hierarchical design, efficient bandwidth utilization, and scalability make it the preferred choice for medium and large organizations. A solid understanding of OSPF is essential for network engineers preparing for CCNA, CCNP, and enterprise networking roles.
