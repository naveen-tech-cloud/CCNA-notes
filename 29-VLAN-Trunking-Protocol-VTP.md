# VLAN Trunking Protocol (VTP)

## Introduction

VLAN Trunking Protocol (VTP) is a Cisco proprietary Layer 2 protocol that simplifies VLAN management in switched networks. It allows VLAN information to be created, modified, and deleted on one switch and automatically synchronized with other switches in the same VTP domain.

Without VTP, network administrators must manually configure VLANs on every switch. In large enterprise environments, this process is time-consuming and increases the risk of configuration errors. VTP automates VLAN distribution, ensuring consistent VLAN configurations across multiple switches.

VTP operates only between Cisco switches connected through trunk links.

---

# Objectives

This document covers:

- Introduction to VTP
- Why VTP is Required
- How VTP Works
- VTP Components
- VTP Modes
- VTP Versions
- VTP Advertisements
- VTP Domain
- Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is VTP?

VLAN Trunking Protocol (VTP) is a Cisco proprietary protocol used to distribute VLAN configuration information between switches within the same VTP domain.

Example

```
Switch A

↓

Creates VLAN 10

↓

VTP Advertisement

↓

Switch B

↓

VLAN 10 Created Automatically

↓

Switch C

↓

VLAN 10 Created Automatically
```

---

# Why VTP is Required

Without VTP

- VLANs must be created manually on every switch.
- Increased configuration time.
- Higher chance of configuration errors.
- Difficult management in large networks.

With VTP

- Centralized VLAN management.
- Automatic VLAN synchronization.
- Reduced administrative effort.
- Consistent VLAN configuration.

---

# How VTP Works

The process is as follows:

1. A VLAN is created or modified on a VTP Server.
2. The server increments the Configuration Revision Number.
3. VTP advertisements are sent through trunk links.
4. Client switches compare revision numbers.
5. If the received revision number is higher, clients update their VLAN database automatically.

---

# VTP Components

## VTP Domain

A VTP Domain is a group of switches that share VLAN information.

Example

```
Domain Name

CORPORATE
```

All participating switches must use the same domain name.

---

## Configuration Revision Number

A revision number that tracks VLAN database changes.

Higher revision numbers overwrite lower revision numbers.

---

## VTP Password

Provides authentication between VTP switches.

Only switches with the correct password exchange VLAN information.

---

# VTP Modes

## Server Mode

Default mode on Cisco switches.

Capabilities

- Create VLANs
- Modify VLANs
- Delete VLANs
- Advertise VLAN information
- Store VLAN database in NVRAM

Configuration

```
vtp mode server
```

---

## Client Mode

Receives VLAN information from the server.

Capabilities

- Cannot create VLANs
- Cannot delete VLANs
- Cannot modify VLANs
- Receives automatic updates

Configuration

```
vtp mode client
```

---

## Transparent Mode

Does not participate in VTP synchronization.

Capabilities

- Creates local VLANs only
- Does not synchronize VLAN database
- Forwards VTP advertisements

Configuration

```
vtp mode transparent
```

---

# VTP Versions

| Version | Features |
|----------|----------|
| Version 1 | Basic VLAN Synchronization |
| Version 2 | Supports Token Ring VLANs |
| Version 3 | Enhanced Security, Extended VLAN Support, Primary Server |

Recommended Version

```
Version 3
```

---

# VTP Advertisements

VTP exchanges VLAN information using advertisements.

Types

### Summary Advertisement

Sent every 5 minutes.

Contains:

- Domain Name
- Revision Number
- Version

---

### Subset Advertisement

Contains detailed VLAN information.

Sent whenever VLAN changes occur.

---

### Advertisement Request

Sent by switches requesting updated VLAN information.

---

# Network Topology

```
             Switch A
          (VTP Server)

                |

         Trunk Connection

                |

             Switch B
          (VTP Client)

                |

         Trunk Connection

                |

             Switch C
          (VTP Client)
```

---

# Basic Configuration

## Configure VTP Domain

```
Switch(config)# vtp domain CORPORATE
```

---

## Configure VTP Mode

```
Switch(config)# vtp mode server
```

---

## Configure Password

```
Switch(config)# vtp password Cisco123
```

---

## Configure Version

```
Switch(config)# vtp version 3
```

---

## Create VLAN

```
Switch(config)# vlan 10

Switch(config-vlan)# name SALES
```

The VLAN is automatically propagated to all VTP Clients.

---

# Verification Commands

Display VTP Status

```
show vtp status
```

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

---

# Example Output

```
VTP Version : 3

VTP Domain : CORPORATE

Configuration Revision : 5

Operating Mode : Server
```

---

# Advantages

- Centralized VLAN management.
- Automatic VLAN synchronization.
- Reduces configuration errors.
- Saves administrative time.
- Simplifies large network deployments.
- Easy VLAN distribution.

---

# Limitations

- Cisco proprietary protocol.
- Incorrect revision numbers can overwrite VLAN databases.
- Requires trunk links.
- Limited usefulness in multi-vendor environments.
- Misconfiguration can affect the entire VTP domain.

---

# VTP Server vs Client vs Transparent

| Feature | Server | Client | Transparent |
|----------|--------|--------|-------------|
| Create VLAN | Yes | No | Yes (Local Only) |
| Delete VLAN | Yes | No | Yes (Local Only) |
| Receive Updates | Yes | Yes | No |
| Send Updates | Yes | No | Forwards Only |
| Store VLAN Database | Yes | No | Yes (Local Only) |

---

# Best Practices

- Use VTP Version 3 in production environments.
- Configure VTP passwords for authentication.
- Verify revision numbers before connecting switches.
- Use meaningful VTP domain names.
- Back up VLAN configurations regularly.
- Use Transparent Mode when centralized management is not required.
- Ensure trunk links are operational before enabling VTP.

---

# Important Notes

- VTP stands for **VLAN Trunking Protocol**.
- VTP is a Cisco proprietary protocol.
- VTP distributes VLAN information automatically.
- VTP works only over trunk links.
- Switches must belong to the same VTP domain.
- VTP Server manages VLAN configurations.
- VTP Client receives VLAN updates.
- Transparent Mode does not synchronize VLAN databases.
- VTP Version 3 is the recommended version.

---

# Conclusion

VLAN Trunking Protocol (VTP) simplifies VLAN administration by automatically distributing VLAN information across Cisco switches within the same VTP domain. It reduces administrative effort, ensures consistent VLAN configurations, and improves scalability in enterprise networks. Proper understanding of VTP modes, revision numbers, and security practices is essential to avoid synchronization issues and maintain a stable switching infrastructure.
