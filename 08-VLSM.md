# Variable Length Subnet Mask (VLSM)

## Introduction

Variable Length Subnet Mask (VLSM) is an advanced subnetting technique that allows a network administrator to create subnets of different sizes based on the number of hosts required. Unlike Fixed Length Subnet Mask (FLSM), where every subnet has the same size, VLSM allocates IP addresses efficiently by assigning only the required number of addresses to each subnet.

VLSM is widely used in enterprise networks because it minimizes IP address wastage and provides greater flexibility in network design.

---

# Objectives

This document covers:

- Introduction to VLSM
- Why VLSM is Required
- Working Principle
- VLSM Calculation Process
- CIDR and Prefix Length
- Step-by-Step Design
- Practical Examples
- Advantages
- Limitations
- Best Practices

---

# What is VLSM?

Variable Length Subnet Mask (VLSM) is a subnetting method in which different subnet masks are assigned to different subnets according to the number of hosts required.

Instead of dividing a network into equal-sized subnets, VLSM creates subnets of varying sizes.

Example:

```
Available Network

192.168.10.0/24

Departments

IT        → 100 Hosts

HR        → 50 Hosts

Finance   → 20 Hosts

Management→ 10 Hosts
```

Each department receives a subnet based on its actual requirement.

---

# Why VLSM is Required?

Suppose an organization has four departments with different numbers of devices.

| Department | Hosts |
|------------|------:|
| IT | 100 |
| HR | 50 |
| Finance | 20 |
| Management | 10 |

Using FLSM, every department would receive the same subnet size, resulting in many unused IP addresses.

Using VLSM, each department receives only the number of IP addresses it actually needs.

---

# How VLSM Works

VLSM follows a simple process.

### Step 1

List all subnet requirements.

### Step 2

Arrange the required host counts from largest to smallest.

### Step 3

Choose the smallest subnet mask that satisfies each requirement.

### Step 4

Assign networks sequentially without overlap.

---

# Common Prefix Values

| Prefix | Subnet Mask | Usable Hosts |
|---------|-------------|-------------:|
| /25 | 255.255.255.128 | 126 |
| /26 | 255.255.255.192 | 62 |
| /27 | 255.255.255.224 | 30 |
| /28 | 255.255.255.240 | 14 |
| /29 | 255.255.255.248 | 6 |
| /30 | 255.255.255.252 | 2 |

---

# Example 1

Available Network

```
192.168.1.0/24
```

Requirements

```
Sales       100 Hosts

HR           50 Hosts

Accounts     25 Hosts

Server Room  10 Hosts
```

---

### Step 1

Arrange in descending order.

```
100

50

25

10
```

---

### Step 2

Choose suitable subnet sizes.

| Hosts Needed | Prefix |
|--------------|--------|
|100|/25|
|50|/26|
|25|/27|
|10|/28|

---

### Step 3

Allocate subnets.

### Sales

```
Network

192.168.1.0/25

Hosts

192.168.1.1

↓

192.168.1.126

Broadcast

192.168.1.127
```

---

### HR

```
Network

192.168.1.128/26

Hosts

192.168.1.129

↓

192.168.1.190

Broadcast

192.168.1.191
```

---

### Accounts

```
Network

192.168.1.192/27

Hosts

192.168.1.193

↓

192.168.1.222

Broadcast

192.168.1.223
```

---

### Server Room

```
Network

192.168.1.224/28

Hosts

192.168.1.225

↓

192.168.1.238

Broadcast

192.168.1.239
```

Remaining addresses

```
192.168.1.240

↓

192.168.1.255
```

can be reserved for future expansion.

---

# Example 2

Available Network

```
10.10.0.0/24
```

Requirements

```
Engineering 120 Hosts

Admin        30 Hosts

Finance      14 Hosts

WAN Link      2 Hosts
```

Subnet Allocation

| Department | Network |
|------------|---------|
|Engineering|10.10.0.0/25|
|Admin|10.10.0.128/27|
|Finance|10.10.0.160/28|
|WAN|10.10.0.176/30|

---

# Block Size Reference

| Mask | Block Size |
|------|-----------:|
|128|128|
|192|64|
|224|32|
|240|16|
|248|8|
|252|4|

Formula

```
256 − Last Octet
```

---

# Practical Enterprise Example

A company has the following departments.

```
IT

Sales

HR

Accounts

Management

Server Room

Guest Network
```

Instead of assigning equal-sized subnets, each department receives a subnet according to its actual host requirement.

Benefits include:

- Better IP utilization
- Easy future expansion
- Reduced wastage
- Improved network planning

---

# Advantages

- Efficient use of IP addresses
- Reduced address wastage
- Better scalability
- Flexible network design
- Supports future growth
- Ideal for enterprise environments
- Better bandwidth utilization

---

# Limitations

- More complex calculations
- Requires proper planning
- Documentation is essential
- Incorrect allocation may cause overlapping subnets

---

# FLSM vs VLSM

| Feature | FLSM | VLSM |
|----------|------|------|
|Subnet Size|Equal|Variable|
|IP Utilization|Moderate|Excellent|
|Scalability|Limited|High|
|Address Wastage|High|Very Low|
|Complexity|Simple|Moderate|
|Enterprise Usage|Rare|Very Common|

---

# Best Practices

- Always allocate the largest subnet first.
- Leave free address space for future growth.
- Document every subnet assignment.
- Avoid overlapping address ranges.
- Verify calculations before deployment.
- Use VLSM for enterprise and cloud environments.

---

# Important Notes

- VLSM is based on actual host requirements.
- Allocate larger networks before smaller ones.
- Every subnet has one Network Address.
- Every subnet has one Broadcast Address.
- VLSM significantly reduces IP address wastage.
- VLSM is the preferred subnetting technique in modern enterprise networks.

---

# Conclusion

Variable Length Subnet Mask (VLSM) is an advanced subnetting technique that enables efficient utilization of IPv4 address space by creating subnets of different sizes. It offers flexibility, scalability, and better network management, making it the preferred choice for enterprise, cloud, and service provider networks where host requirements vary across departments.
