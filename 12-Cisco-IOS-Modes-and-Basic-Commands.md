# Cisco IOS Modes and Basic Commands

## Introduction

Cisco Internetwork Operating System (Cisco IOS) is the operating system used on Cisco routers and switches. It provides a Command Line Interface (CLI) that enables administrators to configure, manage, monitor, and troubleshoot networking devices.

Cisco IOS is organized into different operational modes. Each mode provides a specific level of access and allows administrators to perform particular configuration and management tasks.

Understanding Cisco IOS modes and frequently used commands is one of the most important skills for network engineers and CCNA candidates.

---

# Objectives

This document covers:

- Introduction to Cisco IOS
- Cisco CLI Overview
- Cisco IOS Modes
- Mode Navigation
- Basic Cisco Commands
- Verification Commands
- Configuration Commands
- Command Shortcuts
- Best Practices

---

# What is Cisco IOS?

Cisco IOS (Internetwork Operating System) is the software that runs on Cisco networking devices.

It is responsible for:

- Device Configuration
- Routing
- Switching
- Security
- Network Monitoring
- Interface Management

Administrators interact with Cisco IOS through the Command Line Interface (CLI).

---

# Cisco CLI

CLI stands for **Command Line Interface**.

Instead of using graphical menus, Cisco devices are managed by entering commands.

Example:

```
Router>
```

---

# Cisco IOS Modes

Cisco IOS contains several operating modes.

1. User EXEC Mode
2. Privileged EXEC Mode
3. Global Configuration Mode
4. Interface Configuration Mode
5. Line Configuration Mode
6. Router Configuration Mode

---

# User EXEC Mode

This is the first mode displayed after logging into the router.

Prompt

```
Router>
```

Purpose

- Basic monitoring
- Limited commands
- No configuration changes

Common Commands

```
enable

ping

logout

exit
```

---

# Privileged EXEC Mode

Accessed by typing:

```
enable
```

Prompt

```
Router#
```

Purpose

- Access advanced commands
- View configurations
- Save configurations
- Enter configuration mode

Common Commands

```
show running-config

show startup-config

show ip interface brief

show version

show interfaces

copy running-config startup-config

reload
```

---

# Global Configuration Mode

Enter using:

```
configure terminal
```

Prompt

```
Router(config)#
```

Purpose

Used to configure the entire router.

Examples

```
hostname Router1

enable secret Cisco123

service password-encryption

banner motd #Authorized Users Only#
```

---

# Interface Configuration Mode

Enter using:

```
interface GigabitEthernet0/0
```

Prompt

```
Router(config-if)#
```

Purpose

Configure individual interfaces.

Examples

```
ip address 192.168.1.1 255.255.255.0

description LAN Interface

no shutdown

shutdown
```

---

# Line Configuration Mode

Enter using:

```
line console 0

or

line vty 0 4
```

Prompt

```
Router(config-line)#
```

Purpose

Configure console and remote access.

Examples

```
password Cisco123

login

exec-timeout 10

transport input ssh
```

---

# Router Configuration Mode

Used for configuring routing protocols.

Example

```
router rip

router ospf 1

router eigrp 100
```

Prompt

```
Router(config-router)#
```

---

# Mode Navigation

```
Router>

↓

enable

↓

Router#

↓

configure terminal

↓

Router(config)#

↓

interface GigabitEthernet0/0

↓

Router(config-if)#
```

Return one level

```
exit
```

Return directly to Privileged Mode

```
end

or

Ctrl + Z
```

---

# Basic Show Commands

Display IOS Version

```
show version
```

Display Running Configuration

```
show running-config
```

Display Startup Configuration

```
show startup-config
```

Display Interface Status

```
show ip interface brief
```

Display Routing Table

```
show ip route
```

Display Connected Devices

```
show cdp neighbors
```

Display MAC Address Table (Switch)

```
show mac address-table
```

---

# Configuration Commands

Change Hostname

```
hostname BranchRouter
```

Configure Password

```
enable secret Cisco123
```

Configure Banner

```
banner motd #Unauthorized Access Prohibited#
```

Save Configuration

```
copy running-config startup-config
```

Erase Startup Configuration

```
erase startup-config
```

Reload Device

```
reload
```

---

# Interface Commands

Enter Interface

```
interface GigabitEthernet0/0
```

Assign IP Address

```
ip address 192.168.1.1 255.255.255.0
```

Enable Interface

```
no shutdown
```

Disable Interface

```
shutdown
```

Add Description

```
description Connected to LAN Switch
```

---

# Command Shortcuts

| Shortcut | Full Command |
|----------|--------------|
| en | enable |
| conf t | configure terminal |
| sh run | show running-config |
| sh ip int br | show ip interface brief |
| wr | write memory |
| do | Execute EXEC command from configuration mode |

---

# Configuration Files

Cisco routers maintain two important configuration files.

## Running Configuration

- Stored in RAM
- Active configuration
- Lost after reboot if not saved

View

```
show running-config
```

---

## Startup Configuration

- Stored in NVRAM
- Loaded during boot
- Permanent configuration

View

```
show startup-config
```

---

# Best Practices

- Save configurations regularly.
- Use meaningful hostnames.
- Configure strong passwords.
- Disable unused interfaces.
- Document configuration changes.
- Verify commands before applying them.

---

# Important Notes

- `>` indicates User EXEC Mode.
- `#` indicates Privileged EXEC Mode.
- `(config)#` indicates Global Configuration Mode.
- `(config-if)#` indicates Interface Configuration Mode.
- Use **enable** to enter Privileged EXEC Mode.
- Use **configure terminal** to enter Global Configuration Mode.
- Save configurations using **copy running-config startup-config**.

---

# Conclusion

Cisco IOS provides a structured command-line environment for configuring and managing Cisco networking devices. Understanding IOS modes, navigation, and commonly used commands is essential for network administrators and CCNA professionals. Mastering these commands forms the foundation for advanced routing, switching, security, and network troubleshooting.
