# Access Control Lists (ACL)

## Introduction

Access Control Lists (ACLs) are one of the most important security features available on Cisco routers and Layer 3 switches. ACLs are used to control network traffic by permitting or denying packets based on predefined rules.

ACLs enhance network security by restricting unauthorized access, filtering unwanted traffic, controlling access between networks, and protecting network resources.

ACLs are processed sequentially from top to bottom, and the first matching rule determines whether the packet is permitted or denied.

---

# Objectives

This document covers:

- Introduction to ACL
- Why ACL is Required
- How ACL Works
- Types of ACL
- ACL Number Ranges
- Wildcard Masks
- Standard ACL
- Extended ACL
- Named ACL
- ACL Processing Rules
- Cisco ACL Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is an ACL?

An Access Control List (ACL) is a set of rules configured on a router or Layer 3 switch that determines whether network traffic should be allowed or blocked.

ACLs examine packet information such as:

- Source IP Address
- Destination IP Address
- Protocol
- Port Number

Based on configured rules, packets are either permitted or denied.

---

# Why ACL is Required

ACLs are used to:

- Restrict unauthorized access
- Improve network security
- Filter network traffic
- Protect servers
- Control Internet access
- Reduce unnecessary network traffic

---

# How ACL Works

When a packet reaches a router:

1. Router checks the ACL.
2. ACL reads rules from top to bottom.
3. The first matching rule is applied.
4. Packet is either permitted or denied.
5. If no rule matches, the packet is denied automatically.

---

# Implicit Deny

Every ACL ends with an invisible rule:

```
deny any
```

This is called the **Implicit Deny Rule**.

If no ACL statement matches the packet, it is automatically discarded.

---

# Types of ACL

## Standard ACL

Filters traffic only by **Source IP Address**.

Characteristics

- Simple configuration
- Less flexible
- Usually placed near the destination

Example

```
Permit

192.168.1.0/24
```

---

## Extended ACL

Filters traffic based on:

- Source IP
- Destination IP
- Protocol
- TCP Port
- UDP Port

Characteristics

- More secure
- More flexible
- Usually placed near the source

---

## Named ACL

Instead of using numbers, administrators assign meaningful names.

Example

```
ip access-list extended OFFICE_USERS
```

Named ACLs improve readability and simplify administration.

---

# ACL Number Ranges

## Standard ACL

```
1 – 99

1300 – 1999
```

---

## Extended ACL

```
100 – 199

2000 – 2699
```

---

# Wildcard Mask

Cisco ACLs use Wildcard Masks instead of Subnet Masks.

Formula

```
Wildcard Mask

=

255.255.255.255

-

Subnet Mask
```

Example

Subnet Mask

```
255.255.255.0
```

Wildcard Mask

```
0.0.0.255
```

---

# Common Wildcard Masks

| Subnet Mask | Wildcard Mask |
|--------------|---------------|
|255.0.0.0|0.255.255.255|
|255.255.0.0|0.0.255.255|
|255.255.255.0|0.0.0.255|
|255.255.255.128|0.0.0.127|
|255.255.255.192|0.0.0.63|

---

# Standard ACL Configuration

Allow network:

```
192.168.1.0/24
```

Configuration

```
access-list 10 permit 192.168.1.0 0.0.0.255
```

Apply ACL

```
interface GigabitEthernet0/0

ip access-group 10 in
```

---

# Extended ACL Configuration

Allow HTTP Traffic

```
access-list 100 permit tcp any any eq 80
```

Allow HTTPS

```
access-list 100 permit tcp any any eq 443
```

Deny FTP

```
access-list 100 deny tcp any any eq 21
```

Permit Remaining Traffic

```
access-list 100 permit ip any any
```

---

# Named ACL Configuration

```
ip access-list extended OFFICE

permit tcp any any eq 80

permit tcp any any eq 443

deny ip any any
```

Apply

```
interface GigabitEthernet0/1

ip access-group OFFICE in
```

---

# ACL Direction

ACLs can be applied in two directions.

## Inbound

Traffic is filtered before entering the router.

```
ip access-group 100 in
```

---

## Outbound

Traffic is filtered before leaving the router.

```
ip access-group 100 out
```

---

# Verification Commands

Display ACLs

```
show access-lists
```

Display Running Configuration

```
show running-config
```

Display Interface Information

```
show ip interface
```

Display IP Interface Brief

```
show ip interface brief
```

---

# Example Network

```
PC1

192.168.1.10

        |

GigabitEthernet0/0

Cisco Router

GigabitEthernet0/1

        |

Server

192.168.2.20
```

ACL can restrict PC1 from accessing the server while allowing other network traffic.

---

# ACL Processing Order

ACL rules are processed sequentially.

Example

```
Rule 1

permit tcp any any eq 80

↓

Rule 2

deny ip any any
```

Packets matching Rule 1 are permitted.

All remaining packets are denied.

---

# Advantages

- Enhances network security
- Controls user access
- Reduces unnecessary traffic
- Protects sensitive resources
- Easy to configure
- Supports protocol filtering
- Works with routers and Layer 3 switches

---

# Limitations

- Sequential processing may affect performance in very large ACLs.
- Incorrect rule order can block legitimate traffic.
- Requires proper planning and documentation.
- Standard ACLs filter only Source IP addresses.

---

# Standard ACL vs Extended ACL

| Feature | Standard ACL | Extended ACL |
|----------|--------------|--------------|
|Source IP|Yes|Yes|
|Destination IP|No|Yes|
|Protocol Filtering|No|Yes|
|Port Filtering|No|Yes|
|Security|Basic|Advanced|
|Placement|Near Destination|Near Source|

---

# Best Practices

- Place Standard ACLs close to the destination.
- Place Extended ACLs close to the source.
- Always end ACLs with an explicit permit statement if required.
- Document every ACL rule.
- Test ACLs before deploying in production.
- Remove unused ACL entries.
- Apply ACLs only to necessary interfaces.

---

# Important Notes

- ACL stands for **Access Control List**.
- ACLs are processed from top to bottom.
- The first matching rule is applied.
- Every ACL ends with an implicit **deny any**.
- Standard ACL filters only Source IP addresses.
- Extended ACL filters Source IP, Destination IP, Protocol, and Port Numbers.
- Wildcard Mask is the inverse of the Subnet Mask.

---

# Conclusion

Access Control Lists (ACLs) are a fundamental component of network security, enabling administrators to regulate traffic flow and protect network resources. By filtering packets based on IP addresses, protocols, and port numbers, ACLs provide precise control over communication between devices. Proper planning, rule ordering, and regular verification ensure ACLs effectively secure enterprise networks while maintaining optimal performance.
