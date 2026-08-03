# Rapid Spanning Tree Protocol (RSTP)

## Introduction

Rapid Spanning Tree Protocol (RSTP) is an enhanced version of the original Spanning Tree Protocol (STP). It is standardized as IEEE 802.1w and is designed to provide much faster convergence in switched Ethernet networks while maintaining loop-free Layer 2 topology.

Unlike traditional STP, which may take 30–50 seconds to recover from a topology change, RSTP can typically restore connectivity within 1–6 seconds. This makes RSTP the preferred choice for modern enterprise networks where high availability and minimal downtime are essential.

RSTP is backward compatible with STP and automatically adapts when connected to legacy switches.

---

# Objectives

This document covers:

- Introduction to RSTP
- Why RSTP is Required
- STP vs RSTP
- RSTP Features
- RSTP Port Roles
- RSTP Port States
- Link Types
- Topology Changes
- Cisco Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is RSTP?

Rapid Spanning Tree Protocol (RSTP) is a Layer 2 protocol that prevents switching loops while providing much faster recovery from network failures compared to traditional STP.

It builds a loop-free topology and quickly activates backup paths when failures occur.

---

# Why RSTP is Required

Traditional STP has slow convergence.

Problems include:

- Long recovery time
- Temporary network outages
- Slow failover
- Reduced application availability

RSTP solves these problems by providing:

- Fast convergence
- Immediate topology updates
- Faster network recovery
- Improved reliability

---

# STP vs RSTP

| Feature | STP | RSTP |
|----------|-----|------|
| IEEE Standard | 802.1D | 802.1w |
| Convergence Time | 30–50 Seconds | 1–6 Seconds |
| Port States | 5 | 3 |
| Performance | Moderate | High |
| Enterprise Usage | Legacy Networks | Modern Networks |

---

# How RSTP Works

RSTP continuously exchanges Bridge Protocol Data Units (BPDUs) between switches.

When a topology change occurs:

1. Detects link failure.
2. Selects an alternate path.
3. Immediately activates the backup port.
4. Restores communication.

---

# RSTP Port Roles

## Root Port (RP)

- Best path toward the Root Bridge.
- One per non-root switch.

---

## Designated Port (DP)

- Forwards traffic for a network segment.

---

## Alternate Port

- Backup path to the Root Bridge.
- Quickly becomes active if the Root Port fails.

---

## Backup Port

- Backup for another Designated Port on the same network segment.
- Rarely used in switched Ethernet networks.

---

# RSTP Port States

RSTP simplifies the original STP port states.

## Discarding

- Does not forward traffic.
- Does not learn MAC addresses.

---

## Learning

- Learns MAC addresses.
- Does not forward user traffic.

---

## Forwarding

- Learns MAC addresses.
- Forwards user traffic.

---

# Link Types

RSTP classifies links into three categories.

## Edge Port

Connected to end devices.

Examples:

- PCs
- Printers
- IP Phones

Equivalent to Cisco PortFast.

---

## Point-to-Point Link

Full-duplex connection between switches.

Provides rapid convergence.

---

## Shared Link

Half-duplex connection.

Behaves similarly to traditional STP.

---

# Topology Change Detection

RSTP rapidly detects:

- Link failures
- New switch connections
- Port status changes

Topology information is immediately propagated across the network.

---

# BPDU Operation

Unlike STP, every switch running RSTP generates BPDUs.

Benefits:

- Faster failure detection
- Rapid convergence
- Improved synchronization

---

# Example Topology

```
        Root Switch

        /        \

   Switch B     Switch C

        \        /

     Alternate Link
```

If one active link fails, the alternate link immediately begins forwarding traffic.

---

# Cisco Configuration

Enable RSTP

```
Switch(config)# spanning-tree mode rapid-pvst
```

Configure Root Bridge

```
Switch(config)# spanning-tree vlan 1 root primary
```

Configure Secondary Root

```
Switch(config)# spanning-tree vlan 1 root secondary
```

Enable PortFast

```
interface FastEthernet0/1

spanning-tree portfast
```

Enable BPDU Guard

```
interface FastEthernet0/1

spanning-tree bpduguard enable
```

---

# Verification Commands

Display STP Information

```
show spanning-tree
```

Display Root Bridge

```
show spanning-tree root
```

Display Interface Details

```
show spanning-tree interface
```

Display Running Configuration

```
show running-config
```

---

# Advantages

- Fast convergence
- Prevents Layer 2 loops
- Supports redundant links
- Minimal downtime
- Better network availability
- Compatible with STP
- Recommended for enterprise networks

---

# Limitations

- Cisco enhancements may differ from IEEE implementation.
- Requires compatible switches for best performance.
- More complex than traditional STP.
- Proper planning is required for large deployments.

---

# RSTP vs STP Port States

| STP | RSTP |
|------|------|
| Blocking | Discarding |
| Listening | Discarding |
| Learning | Learning |
| Forwarding | Forwarding |
| Disabled | Discarding |

---

# Best Practices

- Use RSTP instead of traditional STP.
- Configure Root Bridge manually.
- Enable PortFast only on end-device ports.
- Enable BPDU Guard on access ports.
- Verify spanning tree status regularly.
- Document switch priorities and VLAN mappings.
- Avoid unnecessary physical loops.

---

# Important Notes

- RSTP stands for **Rapid Spanning Tree Protocol**.
- RSTP is defined by **IEEE 802.1w**.
- Operates at **OSI Layer 2**.
- Provides convergence within **1–6 seconds**.
- Uses **Discarding**, **Learning**, and **Forwarding** states.
- Supports **Alternate** and **Backup** port roles.
- Backward compatible with STP.
- Cisco implementation is called **Rapid PVST+**.

---

# Conclusion

Rapid Spanning Tree Protocol (RSTP) is a modern Layer 2 protocol that significantly improves network availability by reducing convergence time and providing rapid recovery from topology changes. Through efficient port roles, simplified port states, and intelligent BPDU processing, RSTP ensures loop-free Ethernet networks with minimal downtime, making it the preferred spanning tree protocol for enterprise environments.
