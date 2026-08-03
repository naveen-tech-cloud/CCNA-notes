# Fixed Length Subnet Mask (FLSM)

## Introduction

Fixed Length Subnet Mask (FLSM) is a subnetting technique in which all subnets use the same subnet mask and contain an equal number of host addresses. Every subnet created from the original network has identical size, making FLSM simple to design, configure, and manage.

FLSM is suitable for networks where each department or subnet requires approximately the same number of hosts.

---

# Objectives

This document covers:

- What is FLSM?
- Why FLSM is Used
- Working Principle
- Subnetting Formulas
- Binary Concepts
- Step-by-Step Calculations
- Practical Examples
- Advantages
- Limitations
- Best Practices

---

# What is FLSM?

Fixed Length Subnet Mask (FLSM) divides a network into multiple equal-sized subnets.

Every subnet has:

- Same Network Size
- Same Subnet Mask
- Same Number of Hosts
- Same Broadcast Size

Example

Original Network

```
192.168.1.0/24
```

Divide into 4 equal subnets

Result

```
192.168.1.0/26

192.168.1.64/26

192.168.1.128/26

192.168.1.192/26
```

Each subnet supports exactly **62 usable host addresses**.

---

# Why Use FLSM?

FLSM is useful when every department or network segment requires the same number of devices.

Example

```
HR

60 Devices

Finance

60 Devices

Sales

60 Devices

IT

60 Devices
```

Since every department requires approximately the same number of hosts, FLSM is an ideal choice.

---

# How FLSM Works

Subnetting is performed by borrowing bits from the Host Portion of an IP address.

Example

```
Original Network

192.168.1.0/24

Host Bits

8
```

Borrow

```
2 Bits
```

New Prefix

```
/26
```

---

# Formula

## Number of Subnets

```
2^n
```

Where

n = Number of Borrowed Bits

---

## Hosts per Subnet

```
2^h − 2
```

Where

h = Remaining Host Bits

Subtract 2 for:

- Network Address
- Broadcast Address

---

# Common FLSM Values

| Prefix | Subnet Mask | Subnets (/24 Base) | Usable Hosts |
|---------|-------------|-------------------|--------------|
| /25 | 255.255.255.128 | 2 | 126 |
| /26 | 255.255.255.192 | 4 | 62 |
| /27 | 255.255.255.224 | 8 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 32 | 6 |
| /30 | 255.255.255.252 | 64 | 2 |

---

# Example 1

Given Network

```
192.168.1.0/24
```

Requirement

```
4 Subnets
```

### Step 1

Find borrowed bits

```
2² = 4
```

Borrow

```
2 Bits
```

---

### Step 2

New Prefix

```
/26
```

Subnet Mask

```
255.255.255.192
```

---

### Step 3

Block Size

```
256 − 192 = 64
```

---

### Step 4

Subnets

| Network | First Host | Last Host | Broadcast |
|----------|------------|-----------|-----------|
|192.168.1.0/26|192.168.1.1|192.168.1.62|192.168.1.63|
|192.168.1.64/26|192.168.1.65|192.168.1.126|192.168.1.127|
|192.168.1.128/26|192.168.1.129|192.168.1.190|192.168.1.191|
|192.168.1.192/26|192.168.1.193|192.168.1.254|192.168.1.255|

---

# Example 2

Network

```
10.10.10.0/24
```

Requirement

```
8 Subnets
```

Borrow

```
3 Bits
```

New Prefix

```
/27
```

Subnet Mask

```
255.255.255.224
```

Block Size

```
32
```

Subnets

```
10.10.10.0

10.10.10.32

10.10.10.64

10.10.10.96

10.10.10.128

10.10.10.160

10.10.10.192

10.10.10.224
```

Usable Hosts

```
30 per subnet
```

---

# Binary Representation

Subnet Mask

```
255.255.255.192
```

Binary

```
11111111

11111111

11111111

11000000
```

Network Bits

```
26
```

Host Bits

```
6
```

---

# Block Size Shortcut

Formula

```
256 − Last Octet
```

Examples

| Mask | Block Size |
|------|------------|
|192|64|
|224|32|
|240|16|
|248|8|
|252|4|

---

# Practical Scenario

An organization has four departments.

Each department requires approximately **50 computers**.

Available Network

```
192.168.100.0/24
```

Solution

Divide into four equal /26 subnets.

Each department receives:

- One Network Address
- 62 Usable Hosts
- One Broadcast Address

---

# Advantages

- Easy to calculate
- Simple network design
- Easy troubleshooting
- Uniform subnet sizes
- Straightforward documentation
- Suitable for equal-sized networks

---

# Limitations

- Wastes IP addresses
- Not suitable for different-sized departments
- Poor address utilization
- Limited scalability

---

# FLSM vs VLSM

| Feature | FLSM | VLSM |
|----------|------|------|
|Subnet Size|Equal|Different|
|IP Utilization|Moderate|Efficient|
|Complexity|Low|High|
|Scalability|Limited|Excellent|
|Enterprise Usage|Rare|Very Common|

---

# Best Practices

- Use FLSM only when all networks require similar host counts.
- Reserve additional address space for future expansion.
- Document subnet allocations clearly.
- Verify calculations before deployment.

---

# Important Notes

- Every subnet has one Network Address.
- Every subnet has one Broadcast Address.
- Hosts cannot use the Network or Broadcast Address.
- FLSM creates equal-sized subnets.
- Enterprise environments generally prefer VLSM due to better address efficiency.

---

# Conclusion

Fixed Length Subnet Mask (FLSM) is a simple and effective subnetting technique for environments where all subnetworks require an equal number of hosts. Although easy to implement and manage, it can lead to IP address wastage when subnet requirements vary. For modern enterprise networks with different host requirements, Variable Length Subnet Mask (VLSM) is generally the preferred approach.
