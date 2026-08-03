# IP Address Assignment Rules on Cisco Routers

## Introduction

IP addressing is one of the most fundamental aspects of configuring Cisco routers. Every router interface that participates in network communication must be assigned a valid IP address and subnet mask. Proper IP address assignment ensures successful communication between networks and enables routers to forward packets accurately.

Understanding the rules for assigning IP addresses is essential for designing, configuring, and troubleshooting enterprise networks.

---

# Objectives

This document covers:

- Introduction to IP Address Assignment
- Importance of IP Addressing
- Rules for Assigning IP Addresses
- Interface Configuration
- Practical Examples
- Common Mistakes
- Verification Commands
- Best Practices

---

# What is IP Address Assignment?

IP address assignment is the process of configuring a unique IP address and subnet mask on each router interface.

Every active router interface represents a separate network and requires its own valid IP address.

Example:

```
PC -------- Router -------- Server

192.168.1.10     192.168.1.1
                 10.10.10.1
```

---

# Why is IP Address Assignment Important?

Proper IP addressing allows routers to:

- Identify connected networks
- Forward packets correctly
- Communicate with neighboring routers
- Build routing tables
- Prevent IP conflicts

---

# Rules for Assigning IP Addresses

## Rule 1: Every Interface Requires a Unique IP Address

Each active interface on the router must have a unique IP address.

Correct Example:

```
G0/0

192.168.1.1

G0/1

192.168.2.1
```

Incorrect Example:

```
G0/0

192.168.1.1

G0/1

192.168.1.1
```

Duplicate IP addresses cause communication failures.

---

## Rule 2: Each Interface Must Belong to a Different Network

A router connects multiple networks.

Therefore, every interface should belong to a separate subnet.

Correct Example

```
G0/0

192.168.1.1/24

G0/1

192.168.2.1/24
```

Incorrect Example

```
G0/0

192.168.1.1/24

G0/1

192.168.1.2/24
```

Both interfaces cannot belong to the same network.

---

## Rule 3: Use a Valid Subnet Mask

Every IP address must be configured with the correct subnet mask.

Example

```
192.168.10.1

255.255.255.0
```

---

## Rule 4: Do Not Use Network Address

Network addresses cannot be assigned to hosts or router interfaces.

Example

```
Network

192.168.10.0/24
```

Cannot be assigned.

---

## Rule 5: Do Not Use Broadcast Address

Broadcast addresses are reserved for broadcasting packets.

Example

```
192.168.10.255
```

Cannot be assigned to any interface.

---

## Rule 6: Avoid Duplicate IP Addresses

Every device in a network must have a unique IP address.

Duplicate addresses cause IP conflicts and communication problems.

---

## Rule 7: Enable the Interface

After assigning an IP address, activate the interface using:

```
no shutdown
```

Otherwise, the interface remains administratively down.

---

# Basic Interface Configuration

```
Router> enable

Router# configure terminal

Router(config)# interface GigabitEthernet0/0

Router(config-if)# ip address 192.168.1.1 255.255.255.0

Router(config-if)# no shutdown
```

---

# Multiple Interface Configuration

```
interface GigabitEthernet0/0

ip address 192.168.1.1 255.255.255.0

no shutdown

exit

interface GigabitEthernet0/1

ip address 192.168.2.1 255.255.255.0

no shutdown
```

---

# Practical Example

Network Diagram

```
PC1

192.168.1.10

|

|

G0/0

Router

G0/1

|

|

Server

192.168.2.20
```

Router Configuration

```
interface GigabitEthernet0/0

ip address 192.168.1.1 255.255.255.0

no shutdown

interface GigabitEthernet0/1

ip address 192.168.2.1 255.255.255.0

no shutdown
```

---

# Verification Commands

Display Interface Status

```
show ip interface brief
```

Display Running Configuration

```
show running-config
```

Display Routing Table

```
show ip route
```

Display Interface Details

```
show interfaces
```

---

# Common Mistakes

- Assigning duplicate IP addresses
- Using incorrect subnet masks
- Assigning network addresses
- Assigning broadcast addresses
- Forgetting the `no shutdown` command
- Configuring two router interfaces in the same subnet
- Incorrect default gateway configuration on hosts

---

# Best Practices

- Plan the IP addressing scheme before configuration.
- Use private IP addresses for internal networks.
- Document all assigned IP addresses.
- Use meaningful interface descriptions.
- Verify configurations after assigning addresses.
- Save the configuration after successful testing.

---

# Important Notes

- Every router interface requires a unique IP address.
- Router interfaces should belong to different networks.
- Never assign network or broadcast addresses.
- Always configure the correct subnet mask.
- Use the **no shutdown** command to activate interfaces.
- Verify configurations using Cisco IOS show commands.

---

# Conclusion

Correct IP address assignment is essential for successful routing and communication in Cisco networks. Following standard IP addressing rules helps prevent configuration errors, ensures reliable connectivity, and simplifies troubleshooting. Proper planning, verification, and documentation are key practices for maintaining a stable and scalable enterprise network.
