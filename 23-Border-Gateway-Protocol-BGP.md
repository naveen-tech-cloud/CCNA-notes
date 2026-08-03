# Border Gateway Protocol (BGP)

## Introduction

Border Gateway Protocol (BGP) is the standard **Exterior Gateway Protocol (EGP)** used to exchange routing information between different Autonomous Systems (AS) on the Internet. It is considered the backbone routing protocol of the Internet because it enables communication between Internet Service Providers (ISPs), cloud providers, and large enterprise networks.

Unlike Interior Gateway Protocols (IGPs) such as RIP, OSPF, and EIGRP, which operate within a single Autonomous System, BGP is designed to exchange routing information between multiple Autonomous Systems.

BGP is a **Path Vector Routing Protocol** that makes routing decisions based on various path attributes instead of metrics such as hop count or bandwidth.

---

# Objectives

This document covers:

- Introduction to BGP
- Features of BGP
- Autonomous System (AS)
- Types of BGP
- How BGP Works
- BGP Attributes
- BGP Neighbor Relationship
- Basic Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is BGP?

Border Gateway Protocol (BGP) is a dynamic routing protocol used to exchange routing information between different Autonomous Systems (AS).

It is responsible for determining the most efficient path for data across the Internet.

Example

```
Company A (AS 65001)
        |
        |
      Internet
        |
        |
ISP (AS 65010)
        |
        |
Company B (AS 65020)
```

---

# What is an Autonomous System (AS)?

An Autonomous System (AS) is a collection of IP networks managed by a single organization that follows a common routing policy.

Each AS is identified by a unique Autonomous System Number (ASN).

Examples

```
Google

AS15169

Cloudflare

AS13335

Amazon

AS16509
```

---

# Features of BGP

- Path Vector Routing Protocol
- Internet Standard Routing Protocol
- Highly Scalable
- Policy-Based Routing
- Loop Prevention
- Incremental Updates
- Supports CIDR
- Supports Route Aggregation
- Reliable Communication using TCP

---

# Types of BGP

## External BGP (eBGP)

Used between routers in different Autonomous Systems.

Example

```
AS65001 -------- AS65002
```

---

## Internal BGP (iBGP)

Used between routers within the same Autonomous System.

Example

```
AS65001

R1 -------- R2 -------- R3
```

---

# How BGP Works

The routing process follows these steps:

1. Establishes a TCP session.
2. Exchanges routing information with neighbors.
3. Advertises available routes.
4. Compares multiple paths.
5. Selects the best path.
6. Updates the routing table.

---

# BGP Uses TCP

Unlike RIP and OSPF, BGP uses **TCP Port 179** for reliable communication.

```
Protocol

TCP

Port

179
```

---

# BGP Path Attributes

BGP selects the best route using various path attributes.

## AS Path

List of Autonomous Systems through which a route passes.

Shorter AS Path is preferred.

---

## Next Hop

Indicates the next router used to reach the destination.

---

## Local Preference

Used inside an Autonomous System.

Higher Local Preference is preferred.

---

## MED (Multi Exit Discriminator)

Suggests the preferred entry point into an AS.

Lower MED is preferred.

---

## Weight (Cisco Proprietary)

Used only within a Cisco router.

Higher Weight is preferred.

---

# BGP Neighbor Relationship

Routers exchange routing information only after becoming BGP neighbors.

Example

```
Router A

Neighbor

10.0.0.2

Remote AS

65002
```

---

# Network Topology

```
LAN A

|

R1

AS65001

|

Internet

|

R2

AS65002

|

LAN B
```

---

# Basic BGP Configuration

## Router R1

```
enable

configure terminal

router bgp 65001

neighbor 10.0.0.2 remote-as 65002

network 192.168.1.0 mask 255.255.255.0
```

---

## Router R2

```
router bgp 65002

neighbor 10.0.0.1 remote-as 65001

network 192.168.2.0 mask 255.255.255.0
```

---

# Verification Commands

Display BGP Summary

```
show ip bgp summary
```

Display BGP Routes

```
show ip bgp
```

Display Neighbor Information

```
show ip bgp neighbors
```

Display Routing Table

```
show ip route
```

Display Running Configuration

```
show running-config
```

---

# Routing Table Example

```
B 192.168.2.0/24

C 192.168.1.0/24
```

Legend

- B = BGP Route
- C = Connected Route

---

# BGP Route Selection Order

When multiple routes exist, BGP generally prefers:

1. Highest Weight
2. Highest Local Preference
3. Locally Originated Route
4. Shortest AS Path
5. Lowest Origin Type
6. Lowest MED
7. eBGP over iBGP
8. Lowest IGP Cost to Next Hop
9. Lowest Router ID

---

# Advantages

- Internet-scale routing
- Highly scalable
- Policy-based routing
- Loop prevention using AS Path
- Reliable communication using TCP
- Supports route aggregation
- Efficient path selection

---

# Limitations

- Complex configuration
- High memory usage
- Higher CPU utilization
- Slower convergence than some IGPs
- Requires detailed network planning

---

# BGP vs OSPF

| Feature | BGP | OSPF |
|----------|------|------|
| Protocol Type | Path Vector | Link-State |
| Scope | Between AS | Within AS |
| Metric | Path Attributes | Cost |
| Transport | TCP Port 179 | IP Protocol 89 |
| Scalability | Internet Scale | Enterprise Networks |
| Convergence | Moderate | Fast |

---

# Best Practices

- Use meaningful Autonomous System Numbers.
- Configure neighbor authentication where supported.
- Filter unnecessary route advertisements.
- Implement route summarization.
- Monitor BGP neighbor status regularly.
- Document AS numbers and routing policies.
- Regularly back up router configurations.

---

# Important Notes

- BGP stands for Border Gateway Protocol.
- BGP is the standard Exterior Gateway Protocol (EGP).
- BGP uses TCP Port 179.
- BGP exchanges routes between Autonomous Systems.
- AS Path helps prevent routing loops.
- eBGP connects different Autonomous Systems.
- iBGP operates within the same Autonomous System.
- BGP is the routing protocol used across the Internet.

---

# Conclusion

Border Gateway Protocol (BGP) is the foundation of Internet routing, enabling communication between Autonomous Systems across the globe. Its policy-based routing, scalability, and advanced path selection mechanisms make it the preferred protocol for ISPs, cloud providers, and large enterprises. A strong understanding of BGP is essential for networking professionals pursuing advanced certifications such as CCNP Enterprise, CCIE, and careers in Internet Service Provider (ISP) and data center networking.
