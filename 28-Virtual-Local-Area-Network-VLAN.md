# Virtual Local Area Network (VLAN)

## Introduction

A Virtual Local Area Network (VLAN) is a logical segmentation of a physical network that allows devices to be grouped together regardless of their physical location. VLANs improve network performance, enhance security, simplify management, and reduce broadcast traffic.

Without VLANs, all devices connected to a switch belong to the same broadcast domain. By creating VLANs, administrators can divide a single physical switch into multiple logical networks.

VLAN technology is widely used in enterprise, campus, and data center networks to separate departments such as Human Resources, Finance, Sales, and IT.

---

# Objectives

This document covers:

- Introduction to VLAN
- Why VLAN is Required
- How VLAN Works
- Broadcast Domain
- Collision Domain
- Types of VLANs
- Access Port
- Trunk Port
- IEEE 802.1Q
- VLAN Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is VLAN?

A VLAN (Virtual Local Area Network) is a logical grouping of network devices within the same broadcast domain, regardless of their physical location.

Example

Without VLAN

```
PC1
PC2
PC3
PC4

↓

One Broadcast Domain
```

With VLAN

```
VLAN 10

PC1
PC2

------------

VLAN 20

PC3
PC4
```

Each VLAN acts as an independent network.

---

# Why VLAN is Required

Without VLANs:

- Large broadcast traffic
- Reduced network performance
- Lower security
- Difficult network management

With VLANs:

- Reduced broadcasts
- Better security
- Easy management
- Improved performance
- Department-wise separation

---

# How VLAN Works

A managed switch assigns each switch port to a VLAN.

Devices connected to ports belonging to the same VLAN can communicate directly.

Devices in different VLANs require a Layer 3 device (Router or Layer 3 Switch) for communication.

---

# Broadcast Domain

A Broadcast Domain is a group of devices that receive broadcast frames.

Without VLAN

```
Entire Switch

↓

One Broadcast Domain
```

With VLAN

```
VLAN 10

↓

Broadcast Domain 1

-------------------

VLAN 20

↓

Broadcast Domain 2
```

Each VLAN creates a separate broadcast domain.

---

# Collision Domain

A Collision Domain is a network segment where packet collisions can occur.

Modern switches create one collision domain per port.

---

# VLAN ID Range

| VLAN Type | VLAN ID |
|------------|----------|
| Default VLAN | 1 |
| Normal Range | 1–1005 |
| Extended Range | 1006–4094 |

---

# Types of VLANs

## Default VLAN

Every Cisco switch has VLAN 1 by default.

All switch ports initially belong to VLAN 1.

---

## Data VLAN

Carries user-generated traffic.

Examples

- Computers
- Printers
- Servers

---

## Voice VLAN

Dedicated VLAN for IP Phones.

Advantages

- Better Quality of Service (QoS)
- Reduced voice delay
- Improved call quality

---

## Management VLAN

Used for switch administration.

Protocols

- SSH
- Telnet
- SNMP

---

## Native VLAN

Used on trunk links for untagged traffic.

Default Native VLAN

```
VLAN 1
```

---

# VLAN Ports

## Access Port

An Access Port belongs to only one VLAN.

Typically connected to:

- PC
- Printer
- IP Phone

Configuration

```
switchport mode access
```

---

## Trunk Port

A Trunk Port carries traffic for multiple VLANs.

Typically connected between:

- Switch to Switch
- Switch to Router
- Switch to Layer 3 Switch

Configuration

```
switchport mode trunk
```

---

# IEEE 802.1Q

IEEE 802.1Q is the standard VLAN tagging protocol.

It inserts a VLAN tag into Ethernet frames so that multiple VLANs can travel over the same physical link.

Frame Format

```
Ethernet Frame

↓

802.1Q Tag

↓

Destination
```

---

# Inter-VLAN Communication

Devices in different VLANs cannot communicate directly.

A Router or Layer 3 Switch is required.

Example

```
VLAN10

↓

Router

↓

VLAN20
```

This process is known as **Inter-VLAN Routing**.

---

# Basic VLAN Configuration

## Create VLAN

```
enable

configure terminal

vlan 10

name SALES
```

---

## Create Another VLAN

```
vlan 20

name HR
```

---

## Assign Port to VLAN

```
interface FastEthernet0/1

switchport mode access

switchport access vlan 10
```

---

## Configure Trunk Port

```
interface GigabitEthernet0/1

switchport mode trunk
```

---

# Verification Commands

Display VLAN Information

```
show vlan brief
```

Display Trunk Information

```
show interfaces trunk
```

Display Running Configuration

```
show running-config
```

Display Interface Status

```
show interfaces status
```

---

# Example Network

```
           Switch

----------------------------

Fa0/1 → VLAN10 → PC1

Fa0/2 → VLAN10 → PC2

Fa0/3 → VLAN20 → PC3

Fa0/4 → VLAN20 → PC4

Gi0/1 → Trunk → Router
```

---

# Advantages

- Improves security
- Reduces broadcast traffic
- Better network performance
- Easy administration
- Flexible network design
- Department-wise isolation
- Supports Quality of Service (QoS)

---

# Limitations

- Devices in different VLANs require routing.
- Incorrect VLAN configuration can interrupt communication.
- VLAN hopping attacks are possible if security is not implemented.
- Additional planning is required in large networks.

---

# VLAN vs Physical LAN

| Feature | Physical LAN | VLAN |
|----------|--------------|------|
| Network Type | Physical | Logical |
| Broadcast Domain | Single | Multiple |
| Security | Basic | High |
| Flexibility | Limited | High |
| Management | Difficult | Easy |

---

# Best Practices

- Use descriptive VLAN names.
- Avoid using VLAN 1 for user traffic.
- Secure unused switch ports.
- Configure trunk ports only where required.
- Document VLAN IDs and their purpose.
- Use separate Management VLANs.
- Regularly verify VLAN assignments.

---

# Important Notes

- VLAN stands for **Virtual Local Area Network**.
- VLANs logically divide a physical network.
- Each VLAN is a separate broadcast domain.
- Access Ports belong to a single VLAN.
- Trunk Ports carry multiple VLANs.
- IEEE 802.1Q is the standard VLAN tagging protocol.
- Inter-VLAN communication requires a Router or Layer 3 Switch.

---

# Conclusion

Virtual Local Area Networks (VLANs) are a fundamental technology for modern enterprise networking. By logically segmenting networks, VLANs improve security, reduce broadcast traffic, enhance performance, and simplify network management. Proper VLAN planning and implementation are essential for building scalable, secure, and efficient campus and enterprise networks.
