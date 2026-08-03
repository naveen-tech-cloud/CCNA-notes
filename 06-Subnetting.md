# Subnetting

## Introduction

Subnetting is the process of dividing a large IP network into multiple smaller logical networks called **subnets**. It improves network efficiency, reduces broadcast traffic, enhances security, and allows better utilization of IP address space.

Subnetting is one of the fundamental concepts in computer networking and is extensively used in enterprise, data center, cloud, and service provider networks.

---

# Objectives

This document covers:

- Introduction to Subnetting
- Why Subnetting is Required
- Network Address Structure
- Network ID
- Host ID
- Subnet Mask
- CIDR Notation
- Borrowing Host Bits
- Types of Subnetting
- FLSM
- VLSM
- Advantages
- Best Practices

---

# What is Subnetting?

Subnetting is the technique of dividing one large network into multiple smaller networks.

Instead of using one network for all devices, subnetting creates several smaller subnetworks that improve performance and simplify network management.

Example:

Without Subnetting

```
192.168.1.0/24

254 Hosts
```

With Subnetting

```
192.168.1.0/26

192.168.1.64/26

192.168.1.128/26

192.168.1.192/26
```

Each subnet contains fewer hosts and its own Network ID and Broadcast Address.

---

# Why is Subnetting Required?

Large networks generate excessive broadcast traffic and are difficult to manage.

Subnetting provides:

- Better Network Performance
- Reduced Broadcast Domains
- Improved Security
- Efficient IP Address Utilization
- Simplified Network Administration
- Better Traffic Isolation
- Easier Troubleshooting
- Improved Scalability

---

# IP Address Structure

An IPv4 address consists of **32 bits** divided into four octets.

Example

```
192.168.10.25
```

Binary Representation

```
11000000.10101000.00001010.00011001
```

The address consists of:

- Network Portion
- Host Portion

---

# Network ID

The Network ID identifies the network to which a device belongs.

Example

```
IP Address

192.168.10.25

Subnet Mask

255.255.255.0

Network ID

192.168.10.0
```

Every device within the same subnet shares the same Network ID.

---

# Host ID

The Host ID uniquely identifies an individual device within a network.

Example

```
Network

192.168.10.0

Hosts

192.168.10.1

192.168.10.2

192.168.10.100

192.168.10.254
```

Each Host ID must be unique.

---

# Broadcast Address

The Broadcast Address is used to send packets to all devices within a subnet.

Example

```
Network

192.168.10.0/24

Broadcast

192.168.10.255
```

The broadcast address cannot be assigned to a host.

---

# Subnet Mask

A Subnet Mask separates the Network Portion from the Host Portion of an IP address.

Example

```
255.255.255.0
```

Binary

```
11111111.11111111.11111111.00000000
```

1 = Network Bit

0 = Host Bit

---

# CIDR Notation

CIDR (Classless Inter-Domain Routing) represents the subnet mask using prefix length.

Examples

| CIDR | Subnet Mask |
|------|-------------|
| /8 | 255.0.0.0 |
| /16 | 255.255.0.0 |
| /24 | 255.255.255.0 |
| /25 | 255.255.255.128 |
| /26 | 255.255.255.192 |
| /27 | 255.255.255.224 |
| /28 | 255.255.255.240 |
| /29 | 255.255.255.248 |
| /30 | 255.255.255.252 |

---

# Borrowing Host Bits

Subnetting works by borrowing bits from the Host Portion.

Example

Original Network

```
192.168.1.0/24
```

Borrow 2 Host Bits

```
/26
```

Result

```
4 Subnets

62 Hosts per Subnet
```

---

# Formula Used in Subnetting

Number of Subnets

```
2^n
```

Where

n = Number of Borrowed Bits

---

Hosts Per Subnet

```
2^h - 2
```

Where

h = Number of Host Bits

Subtracting 2 accounts for:

- Network Address
- Broadcast Address

---

# Types of Subnetting

Subnetting is divided into two categories:

## Fixed Length Subnet Mask (FLSM)

All subnets use the same subnet mask and contain an equal number of hosts.

Example

```
192.168.1.0/24

↓

4 Subnets

↓

/26
```

Each subnet has:

```
62 Hosts
```

---

## Variable Length Subnet Mask (VLSM)

Each subnet can use a different subnet mask based on host requirements.

Example

```
Department A

100 Hosts

↓

/25

Department B

30 Hosts

↓

/27

Department C

10 Hosts

↓

/28
```

This minimizes IP address wastage.

---

# Practical Example

A company has three departments.

- HR → 20 Hosts
- Finance → 50 Hosts
- IT → 120 Hosts

Instead of assigning a /24 network to each department, VLSM allocates subnet sizes according to the number of hosts required.

This improves address utilization and network efficiency.

---

# Advantages of Subnetting

- Efficient IP Address Management
- Reduced Broadcast Traffic
- Better Security
- Easier Administration
- Improved Performance
- Scalable Network Design
- Better Traffic Control

---

# Limitations

- Requires subnetting knowledge
- Incorrect calculations can cause connectivity issues
- More complex network planning
- Additional documentation required

---

# Best Practices

- Plan IP addressing before deployment.
- Allocate IP addresses based on future growth.
- Use VLSM in enterprise environments.
- Document every subnet.
- Avoid overlapping IP ranges.
- Reserve address space for expansion.

---

# Important Notes

- Every subnet has one Network Address.
- Every subnet has one Broadcast Address.
- Host addresses begin after the Network Address.
- Host addresses end before the Broadcast Address.
- FLSM uses equal-sized subnets.
- VLSM uses variable-sized subnets.
- CIDR is the modern method of subnet representation.

---

# Conclusion

Subnetting is a critical networking technique that divides large networks into smaller, manageable subnetworks. Proper subnetting improves performance, reduces unnecessary broadcast traffic, enhances security, and optimizes IP address utilization. A strong understanding of subnetting forms the foundation for advanced routing, switching, and enterprise network design.
