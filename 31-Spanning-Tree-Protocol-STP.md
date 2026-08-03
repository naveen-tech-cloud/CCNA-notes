# Spanning Tree Protocol (STP)

## Introduction

Spanning Tree Protocol (STP) is a Layer 2 network protocol designed to prevent switching loops in Ethernet networks. It was standardized as IEEE 802.1D and is automatically enabled on Cisco switches by default.

In a switched network with redundant links, Ethernet frames can circulate indefinitely, creating broadcast storms, duplicate frames, and MAC address instability. STP eliminates these loops by logically blocking redundant paths while keeping them available as backup links.

If the active path fails, STP automatically activates the blocked path, ensuring continuous network connectivity without creating loops.

---

# Objectives

This document covers:

- Introduction to STP
- Why STP is Required
- Switching Loops
- Broadcast Storm
- MAC Address Table Instability
- Root Bridge Election
- Port Roles
- Port States
- STP Operation
- STP Versions
- Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is STP?

Spanning Tree Protocol (STP) is a Layer 2 protocol that prevents network loops by creating a loop-free logical topology.

Although multiple physical paths may exist between switches, STP ensures that only one active path is used for forwarding traffic.

---

# Why STP is Required

Without STP:

- Switching loops occur.
- Broadcast frames circulate endlessly.
- Duplicate Ethernet frames are created.
- MAC address tables become unstable.
- Network bandwidth is exhausted.

With STP:

- Loop-free topology
- Redundant links remain available
- Automatic failover
- Stable MAC address tables
- Reliable Ethernet communication

---

# Switching Loop

A switching loop occurs when redundant paths exist between switches without loop prevention.

Example

```
       Switch A
       /      \
      /        \
Switch B ---- Switch C
```

Frames continue circulating indefinitely.

---

# Problems Caused by Switching Loops

## Broadcast Storm

Broadcast packets are continuously forwarded throughout the network.

Effects

- High CPU utilization
- Network congestion
- Slow performance
- Complete network outage

---

## Duplicate Frames

The destination device receives multiple copies of the same Ethernet frame.

Effects

- Data corruption
- Poor application performance

---

## MAC Address Table Instability

Switches continuously update MAC address tables because frames arrive from different interfaces.

Effects

- Frequent relearning
- Incorrect forwarding decisions

---

# How STP Works

STP performs the following steps:

1. Elects a Root Bridge.
2. Calculates the shortest path to the Root Bridge.
3. Assigns port roles.
4. Blocks redundant paths.
5. Monitors the network continuously.
6. Recalculates topology after failures.

---

# Root Bridge

The Root Bridge is the central switch in the spanning tree topology.

All path calculations are based on the Root Bridge.

The switch with the **lowest Bridge ID** becomes the Root Bridge.

---

# Bridge ID

Bridge ID consists of:

```
Priority

+

MAC Address
```

Default Priority

```
32768
```

Lower Bridge ID wins the election.

---

# Port Roles

## Root Port (RP)

- One per non-root switch
- Lowest path cost to the Root Bridge
- Forwarding state

---

## Designated Port (DP)

- One per network segment
- Forwards traffic
- Selected based on lowest path cost

---

## Non-Designated Port (Blocked Port)

- Backup path
- Does not forward traffic
- Prevents loops

---

# STP Port States

## Blocking

- Receives BPDUs
- Does not forward frames
- No MAC learning

---

## Listening

- Processes BPDUs
- Determines topology
- No MAC learning

---

## Learning

- Learns MAC addresses
- Does not forward user traffic

---

## Forwarding

- Learns MAC addresses
- Forwards user traffic

---

## Disabled

- Port is administratively shut down or inactive.

---

# BPDU (Bridge Protocol Data Unit)

BPDUs are special messages exchanged between switches.

Purpose

- Elect Root Bridge
- Detect topology changes
- Maintain spanning tree

---

# STP Versions

## IEEE 802.1D

Classic STP

Convergence Time

30–50 Seconds

---

## IEEE 802.1w (RSTP)

Rapid Spanning Tree Protocol

Convergence Time

1–6 Seconds

Recommended for modern networks.

---

## IEEE 802.1s (MSTP)

Multiple Spanning Tree Protocol

Supports multiple VLAN groups using separate spanning tree instances.

---

# Path Cost

STP selects the path with the lowest total cost.

Example

| Link Speed | Cost |
|------------|------|
|10 Mbps|100|
|100 Mbps|19|
|1 Gbps|4|
|10 Gbps|2|

Lower Cost = Better Path

---

# Example Topology

```
          Root Switch

          /        \

      Switch B    Switch C

          \        /

        Blocked Link
```

Only one path remains active.

---

# Configure Root Bridge

```
Switch(config)# spanning-tree vlan 1 root primary
```

Configure Secondary Root

```
Switch(config)# spanning-tree vlan 1 root secondary
```

---

# Enable PortFast

```
interface FastEthernet0/1

spanning-tree portfast
```

Used only on end-device ports.

---

# Enable BPDU Guard

```
interface FastEthernet0/1

spanning-tree bpduguard enable
```

Protects PortFast ports from unauthorized switches.

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

Display Interface Status

```
show spanning-tree interface
```

Display Running Configuration

```
show running-config
```

---

# Advantages

- Prevents switching loops
- Eliminates broadcast storms
- Supports redundant links
- Automatic failover
- Stable Layer 2 topology
- Improves network reliability

---

# Limitations

- Classic STP has slow convergence.
- Some redundant links remain unused.
- Improper configuration can affect network performance.
- Large networks benefit from RSTP or MSTP.

---

# STP vs RSTP

| Feature | STP | RSTP |
|----------|------|------|
|IEEE Standard|802.1D|802.1w|
|Convergence|30–50 Seconds|1–6 Seconds|
|Performance|Moderate|Fast|
|Enterprise Usage|Older Networks|Modern Networks|

---

# Best Practices

- Configure a predictable Root Bridge.
- Enable PortFast on access ports.
- Enable BPDU Guard on PortFast ports.
- Use RSTP in modern enterprise environments.
- Avoid unnecessary physical loops.
- Regularly verify STP topology.
- Document switch priorities.

---

# Important Notes

- STP stands for **Spanning Tree Protocol**.
- STP operates at **OSI Layer 2**.
- STP prevents switching loops.
- IEEE **802.1D** defines STP.
- RSTP (802.1w) provides faster convergence.
- The switch with the lowest Bridge ID becomes the Root Bridge.
- Root Ports and Designated Ports forward traffic.
- Blocked Ports prevent loops.
- BPDUs are exchanged to maintain the spanning tree.

---

# Conclusion

Spanning Tree Protocol (STP) is a critical Layer 2 protocol that ensures loop-free Ethernet networks by intelligently managing redundant links. Through Root Bridge election, port role assignment, and continuous topology monitoring, STP prevents broadcast storms and maintains reliable communication. Modern implementations such as Rapid Spanning Tree Protocol (RSTP) provide significantly faster convergence and are recommended for enterprise network deployments.
