# Static Routing

## Introduction

Routing is the process of forwarding packets from one network to another. A router determines the best path for data by consulting its routing table. One of the simplest routing methods is **Static Routing**, where routes are manually configured by a network administrator.

Static routing is commonly used in small networks, point-to-point links, branch offices, and environments where the network topology changes infrequently.

---

# Objectives

This document covers:

- Introduction to Static Routing
- How Static Routing Works
- Types of Static Routes
- Static Route Syntax
- Configuration Examples
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is Static Routing?

Static Routing is a routing method in which the administrator manually configures routes on the router.

Unlike dynamic routing, routers do not automatically learn routes from neighboring routers.

Example:

```
PC1
 |
R1 -------- R2
             |
            PC2
```

R1 must be manually configured to reach the network connected to R2.

---

# How Static Routing Works

The routing process follows these steps:

1. A packet reaches the router.
2. The router checks the destination IP address.
3. The router searches its routing table.
4. If a matching static route exists, the packet is forwarded.
5. If no route exists, the packet is dropped.

---

# Static Route Syntax

General Syntax:

```
ip route <destination-network> <subnet-mask> <next-hop-ip>
```

Example:

```
ip route 192.168.2.0 255.255.255.0 10.0.12.2
```

Where:

- Destination Network → `192.168.2.0`
- Subnet Mask → `255.255.255.0`
- Next Hop → `10.0.12.2`

---

# Network Topology

```
LAN 1
192.168.1.0/24
     |
    R1
10.0.12.1
     |
10.0.12.2
    R2
     |
192.168.2.0/24
```

---

# IP Addressing Table

| Device | Interface | IP Address |
|---------|-----------|------------|
| R1 | G0/0 | 192.168.1.1 |
| R1 | S0/0/0 | 10.0.12.1 |
| R2 | S0/0/0 | 10.0.12.2 |
| R2 | G0/0 | 192.168.2.1 |

---

# Configure Router R1

```
enable

configure terminal

interface Serial0/0/0

ip address 10.0.12.1 255.255.255.252

no shutdown

exit

ip route 192.168.2.0 255.255.255.0 10.0.12.2
```

---

# Configure Router R2

```
enable

configure terminal

interface Serial0/0/0

ip address 10.0.12.2 255.255.255.252

no shutdown

exit

ip route 192.168.1.0 255.255.255.0 10.0.12.1
```

---

# Types of Static Routing

## Standard Static Route

Uses the next-hop IP address.

Example:

```
ip route 192.168.2.0 255.255.255.0 10.0.12.2
```

---

## Directly Connected Static Route

Uses the outgoing interface instead of the next-hop IP.

Example:

```
ip route 192.168.2.0 255.255.255.0 Serial0/0/0
```

---

## Default Static Route

Used when no specific route exists.

Syntax:

```
ip route 0.0.0.0 0.0.0.0 <Next-Hop-IP>
```

Example:

```
ip route 0.0.0.0 0.0.0.0 10.0.12.2
```

This route is also called the **Gateway of Last Resort**.

---

# Verification Commands

Display Routing Table

```
show ip route
```

Display Running Configuration

```
show running-config
```

Display Interface Status

```
show ip interface brief
```

Ping Remote Network

```
ping 192.168.2.1
```

Trace Packet Path

```
traceroute 192.168.2.1
```

---

# Routing Table Example

```
R1# show ip route

C 192.168.1.0/24 is directly connected

C 10.0.12.0/30 is directly connected

S 192.168.2.0/24 [1/0] via 10.0.12.2
```

Where:

- **C** = Connected Route
- **S** = Static Route

---

# Advantages of Static Routing

- Easy to configure in small networks
- No routing protocol overhead
- Better security
- Low CPU usage
- Predictable routing paths
- Simple troubleshooting

---

# Limitations

- Manual configuration required
- Not scalable for large networks
- Route updates must be done manually
- Configuration errors can interrupt communication
- Difficult to manage in enterprise environments

---

# Common Errors

- Incorrect destination network
- Wrong subnet mask
- Incorrect next-hop IP address
- Interface shutdown
- Missing return route
- Duplicate or conflicting routes

---

# Best Practices

- Use static routing for small and stable networks.
- Verify IP addressing before configuring routes.
- Always configure return routes.
- Document all configured routes.
- Save the configuration after successful testing.
- Verify routing tables after every configuration.

---

# Important Notes

- Static routes are manually configured.
- Static routes do not update automatically.
- Every static route requires a valid destination network and next-hop.
- Default routes are used when no specific route exists.
- Static routing is ideal for small and simple network environments.

---

# Conclusion

Static Routing is a simple and reliable routing technique where routes are manually configured by network administrators. It provides full control over packet forwarding and is well suited for small, stable networks with predictable traffic patterns. Although it lacks the scalability of dynamic routing protocols, static routing remains an essential networking concept and forms the foundation for understanding advanced routing technologies.
