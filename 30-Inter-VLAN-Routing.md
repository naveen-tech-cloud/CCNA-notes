# Inter-VLAN Routing

## Introduction

Inter-VLAN Routing is the process of enabling communication between devices located in different VLANs. By default, VLANs are isolated Layer 2 broadcast domains, meaning devices in separate VLANs cannot communicate directly. To allow communication between VLANs, a Layer 3 device such as a Router or Layer 3 Switch is required.

Inter-VLAN Routing is an essential technology in enterprise networks where departments such as Human Resources, Finance, Sales, and IT are placed in separate VLANs while still requiring controlled communication between them.

---

# Objectives

This document covers:

- Introduction to Inter-VLAN Routing
- Why Inter-VLAN Routing is Required
- How Inter-VLAN Routing Works
- Methods of Inter-VLAN Routing
- Router-on-a-Stick (ROAS)
- Layer 3 Switch Routing
- Subinterfaces
- IEEE 802.1Q Encapsulation
- Cisco Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is Inter-VLAN Routing?

Inter-VLAN Routing is the process of routing network traffic between different VLANs using a Layer 3 device.

Example

```
VLAN 10

PC1

192.168.10.10

↓

Router

↓

VLAN 20

PC2

192.168.20.10
```

Without routing, these two devices cannot communicate.

---

# Why Inter-VLAN Routing is Required

Without Inter-VLAN Routing

- VLANs remain isolated.
- Departments cannot communicate.
- Servers cannot be accessed across VLANs.
- Network resources remain unavailable.

With Inter-VLAN Routing

- Communication between VLANs.
- Centralized resource sharing.
- Controlled access using ACLs.
- Better network management.

---

# How Inter-VLAN Routing Works

1. A device sends traffic to another VLAN.
2. The frame reaches the switch.
3. The switch forwards the frame to the router through a trunk link.
4. The router determines the destination network.
5. The router forwards the packet to the appropriate VLAN.
6. The destination device receives the packet.

---

# Methods of Inter-VLAN Routing

## Legacy Inter-VLAN Routing

Uses one physical router interface for each VLAN.

Example

```
Router

↓

Fa0/0 → VLAN10

Fa0/1 → VLAN20

Fa0/2 → VLAN30
```

Disadvantages

- Requires multiple router interfaces.
- Not scalable.
- Expensive.

---

## Router-on-a-Stick (ROAS)

Uses a single physical router interface divided into multiple logical subinterfaces.

Example

```
Router

Gi0/0

↓

Gi0/0.10

↓

VLAN10

------------

Gi0/0.20

↓

VLAN20
```

Advantages

- One physical interface
- Easy configuration
- Cost effective
- Most common CCNA method

---

## Layer 3 Switch Routing

A Layer 3 Switch performs routing internally using Switch Virtual Interfaces (SVIs).

Advantages

- Very fast
- No external router required
- High performance
- Enterprise solution

---

# Router-on-a-Stick (ROAS)

Router-on-a-Stick uses:

- One Router Interface
- One Trunk Link
- Multiple Subinterfaces

Each subinterface belongs to one VLAN.

Example

```
Gi0/0.10

↓

VLAN10

----------------

Gi0/0.20

↓

VLAN20
```

---

# IEEE 802.1Q Encapsulation

Each subinterface must use IEEE 802.1Q tagging.

Example

```
encapsulation dot1Q 10
```

This command identifies VLAN 10 traffic.

---

# Example Network

```
PC1

192.168.10.10

↓

VLAN10

↓

Cisco Switch

↓

Trunk

↓

Router

↓

Trunk

↓

Cisco Switch

↓

VLAN20

↓

PC2

192.168.20.10
```

---

# Switch Configuration

Create VLANs

```
enable

configure terminal

vlan 10

name SALES

vlan 20

name HR
```

Assign Ports

```
interface FastEthernet0/1

switchport mode access

switchport access vlan 10
```

```
interface FastEthernet0/2

switchport mode access

switchport access vlan 20
```

Configure Trunk

```
interface GigabitEthernet0/1

switchport mode trunk
```

---

# Router Configuration

Enable Interface

```
interface GigabitEthernet0/0

no shutdown
```

Subinterface VLAN 10

```
interface GigabitEthernet0/0.10

encapsulation dot1Q 10

ip address 192.168.10.1 255.255.255.0
```

Subinterface VLAN 20

```
interface GigabitEthernet0/0.20

encapsulation dot1Q 20

ip address 192.168.20.1 255.255.255.0
```

---

# Configure Default Gateway

For VLAN10 Devices

```
192.168.10.1
```

For VLAN20 Devices

```
192.168.20.1
```

---

# Verification Commands

Display Interfaces

```
show ip interface brief
```

Display Subinterfaces

```
show running-config
```

Display VLAN Information

```
show vlan brief
```

Display Trunk Information

```
show interfaces trunk
```

Display Routing Table

```
show ip route
```

---

# Example Routing Table

```
C 192.168.10.0/24

C 192.168.20.0/24
```

---

# Advantages

- Enables communication between VLANs.
- Efficient use of network resources.
- Improves scalability.
- Supports centralized routing.
- Works with ACLs for security.
- Easy to implement using ROAS.

---

# Limitations

- Router-on-a-Stick can become a bottleneck.
- Single trunk link may limit bandwidth.
- Legacy routing requires multiple interfaces.
- Additional configuration required.

---

# Router-on-a-Stick vs Layer 3 Switch

| Feature | Router-on-a-Stick | Layer 3 Switch |
|-----------|------------------|----------------|
| Routing Device | Router | Layer 3 Switch |
| Performance | Moderate | High |
| Cost | Low | Higher |
| Scalability | Medium | Excellent |
| Enterprise Usage | Small Networks | Large Networks |

---

# Best Practices

- Use Router-on-a-Stick for small and medium networks.
- Use Layer 3 Switches in enterprise environments.
- Configure descriptive VLAN names.
- Verify trunk links before routing.
- Assign correct default gateways.
- Document VLAN IDs and IP addressing.
- Test connectivity using ping after configuration.

---

# Important Notes

- Inter-VLAN Routing enables communication between different VLANs.
- VLANs are isolated Layer 2 broadcast domains.
- A Router or Layer 3 Switch is required for routing.
- Router-on-a-Stick uses subinterfaces.
- IEEE 802.1Q provides VLAN tagging.
- Each VLAN must have a unique gateway IP address.
- Trunk ports carry traffic for multiple VLANs.

---

# Conclusion

Inter-VLAN Routing is a critical networking technology that allows devices in separate VLANs to communicate while maintaining logical network segmentation. Router-on-a-Stick offers a simple and cost-effective solution for smaller networks, whereas Layer 3 switches provide high-performance routing for enterprise environments. Proper VLAN configuration, trunking, and gateway assignment ensure secure and efficient communication across VLANs.
