# EtherChannel

## Introduction

EtherChannel is a Layer 2 technology that combines multiple physical Ethernet links into a single logical link. By bundling multiple interfaces together, EtherChannel increases bandwidth, provides redundancy, and improves network reliability without creating switching loops.

Instead of forwarding traffic through individual interfaces, EtherChannel treats all bundled interfaces as one logical interface called a **Port Channel**.

EtherChannel is widely used between switches, routers, and servers in enterprise networks to improve performance and fault tolerance.

---

# Objectives

This document covers:

- Introduction to EtherChannel
- Why EtherChannel is Required
- How EtherChannel Works
- Load Balancing
- EtherChannel Protocols
- LACP
- PAgP
- Port Channel
- Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is EtherChannel?

EtherChannel is a technology that logically combines multiple physical Ethernet interfaces into one logical interface called a Port Channel.

Example

```
Switch A

Gi0/1

Gi0/2

Gi0/3

Gi0/4

↓

Port-Channel 1

↓

Switch B
```

All four links work together as one connection.

---

# Why EtherChannel is Required

Without EtherChannel

- Limited bandwidth
- Single point of failure
- STP blocks redundant links
- Lower network performance

With EtherChannel

- Higher bandwidth
- Redundant links remain active
- Load balancing
- Better fault tolerance

---

# How EtherChannel Works

Instead of blocking redundant links, EtherChannel bundles them together.

Traffic is distributed across all active links using load balancing algorithms.

If one link fails, traffic automatically continues through the remaining links without interrupting communication.

---

# EtherChannel Requirements

All interfaces in an EtherChannel must have:

- Same Speed
- Same Duplex Mode
- Same VLAN Configuration
- Same Switchport Mode
- Same Native VLAN
- Same Allowed VLANs
- Same STP Settings

---

# EtherChannel Protocols

## PAgP (Port Aggregation Protocol)

- Cisco Proprietary
- Automatically negotiates EtherChannel

Modes

```
Auto

Desirable
```

---

## LACP (Link Aggregation Control Protocol)

- IEEE 802.3ad / 802.1AX Standard
- Vendor Independent
- Recommended for modern networks

Modes

```
Active

Passive
```

---

## Static EtherChannel

No negotiation protocol is used.

Interfaces are manually configured.

Mode

```
On
```

---

# EtherChannel Modes

| Protocol | Mode 1 | Mode 2 |
|-----------|--------|--------|
|PAgP|Auto|Desirable|
|LACP|Passive|Active|
|Static|On|On|

---

# Port Channel

After configuration, all bundled interfaces appear as one logical interface.

Example

```
Port-channel1
```

Configuration is applied to the Port Channel instead of individual interfaces.

---

# Load Balancing

EtherChannel distributes traffic using hashing algorithms.

Common Load Balancing Methods

- Source MAC Address
- Destination MAC Address
- Source IP Address
- Destination IP Address
- Source and Destination IP
- Source and Destination MAC

---

# Example Topology

```
        Switch A

Gi0/1 ========= Gi0/1

Gi0/2 ========= Gi0/2

Gi0/3 ========= Gi0/3

Gi0/4 ========= Gi0/4

        Switch B

↓

Port-Channel 1
```

---

# LACP Configuration

Select Interfaces

```
interface range GigabitEthernet0/1-2
```

Assign Channel Group

```
channel-group 1 mode active
```

Configure Port Channel

```
interface Port-channel1

switchport mode trunk
```

---

# PAgP Configuration

```
interface range GigabitEthernet0/1-2

channel-group 1 mode desirable
```

---

# Static EtherChannel Configuration

```
interface range GigabitEthernet0/1-2

channel-group 1 mode on
```

---

# Verification Commands

Display EtherChannel Summary

```
show etherchannel summary
```

Display Port Channel

```
show interfaces port-channel
```

Display LACP Information

```
show lacp neighbor
```

Display PAgP Information

```
show pagp neighbor
```

Display Running Configuration

```
show running-config
```

---

# Example Output

```
Group: 1

Port-channel: Po1

Protocol: LACP

Ports:

Gi0/1

Gi0/2
```

---

# Advantages

- Increased bandwidth
- Link redundancy
- Automatic failover
- Load balancing
- STP treats bundled links as one logical interface
- Improved network reliability
- Easy scalability

---

# Limitations

- All interfaces must have identical configurations.
- Misconfiguration prevents channel formation.
- Does not increase single-session bandwidth.
- Requires compatible devices.

---

# LACP vs PAgP

| Feature | LACP | PAgP |
|----------|------|------|
|Standard|IEEE 802.3ad / 802.1AX|Cisco Proprietary|
|Compatibility|Multi-Vendor|Cisco Only|
|Recommended|Yes|Legacy Cisco Networks|
|Modes|Active / Passive|Desirable / Auto|

---

# Best Practices

- Use LACP for new deployments.
- Verify interface configurations before bundling.
- Configure trunk settings on the Port Channel interface.
- Monitor EtherChannel status regularly.
- Use descriptive Port Channel numbers.
- Document EtherChannel connections.
- Test redundancy after deployment.

---

# Important Notes

- EtherChannel combines multiple physical links into one logical link.
- The logical interface is called a **Port Channel**.
- LACP is the IEEE standard protocol.
- PAgP is Cisco proprietary.
- Static EtherChannel uses **mode on**.
- STP views an EtherChannel as a single logical interface.
- EtherChannel provides bandwidth aggregation and redundancy.

---

# Conclusion

EtherChannel is a powerful Layer 2 technology that enhances network performance by aggregating multiple physical links into a single logical connection. It improves bandwidth utilization, provides redundancy, supports load balancing, and prevents unnecessary link blocking by STP. Using LACP as the preferred standard ensures compatibility, scalability, and high availability in modern enterprise networks.
