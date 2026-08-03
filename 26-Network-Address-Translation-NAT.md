# Network Address Translation (NAT)

## Introduction

Network Address Translation (NAT) is a networking technique that enables private IP addresses used within a local network to communicate with public networks, such as the Internet, by translating private IP addresses into public IP addresses.

NAT conserves the limited IPv4 address space and provides an additional layer of security by hiding internal network addresses from external networks. It is implemented on routers and firewalls and is widely used in home, enterprise, and Internet Service Provider (ISP) environments.

---

# Objectives

This document covers:

- Introduction to NAT
- Why NAT is Required
- How NAT Works
- Types of NAT
- NAT Terminology
- NAT Operation
- Cisco NAT Configuration
- Verification Commands
- Advantages
- Limitations
- Best Practices

---

# What is NAT?

Network Address Translation (NAT) is the process of modifying the source or destination IP address of packets as they pass through a router or firewall.

It enables devices using private IP addresses to access public networks by translating their addresses into one or more public IP addresses.

Example

```
Private Network

PC1

192.168.1.10

        |

Cisco Router (NAT)

Public IP

203.0.113.10

        |

Internet
```

The router translates:

```
192.168.1.10

↓

203.0.113.10
```

---

# Why NAT is Required

Without NAT:

- Every device requires a unique public IP address.
- IPv4 addresses would be exhausted rapidly.
- Internal devices would be directly exposed to the Internet.

With NAT:

- Conserves public IPv4 addresses.
- Hides private IP addresses.
- Enables Internet access for private networks.
- Reduces deployment costs.

---

# How NAT Works

1. A device sends data to the Internet.
2. The router receives the packet.
3. NAT replaces the private source IP with a public IP.
4. The packet is forwarded to the Internet.
5. The destination replies to the public IP.
6. The router translates the public IP back to the original private IP.
7. The packet is delivered to the internal device.

---

# NAT Terminology

## Inside Local Address

The private IP address assigned to a device within the internal network.

Example

```
192.168.1.10
```

---

## Inside Global Address

The public IP address representing the internal device on the Internet.

Example

```
203.0.113.10
```

---

## Outside Local Address

The IP address of the external destination as viewed from the internal network.

---

## Outside Global Address

The actual public IP address of the external destination.

Example

```
142.250.183.206
```

---

# Types of NAT

## Static NAT

Static NAT creates a permanent one-to-one mapping between a private IP address and a public IP address.

Example

```
192.168.1.10

↓

203.0.113.10
```

### Applications

- Web Servers
- Mail Servers
- DNS Servers

---

## Dynamic NAT

Dynamic NAT maps private IP addresses to available public IP addresses from a predefined pool.

Example

```
Private Pool

192.168.1.10

↓

Public Pool

203.0.113.10
```

The mapping changes depending on available addresses.

---

## PAT (Port Address Translation)

PAT allows multiple private devices to share a single public IP address by using different port numbers.

Also known as:

- NAT Overload

Example

```
PC1

192.168.1.10:1025

↓

203.0.113.10:3001

---------------------

PC2

192.168.1.20:1030

↓

203.0.113.10:3002
```

PAT is the most commonly used form of NAT.

---

# Comparison of NAT Types

| Feature | Static NAT | Dynamic NAT | PAT |
|----------|------------|-------------|-----|
| Mapping | One-to-One | Many-to-Many | Many-to-One |
| Public IP Usage | One per Device | Pool of IPs | Single IP |
| Internet Sharing | No | Limited | Yes |
| Common Usage | Servers | Medium Networks | Home & Enterprise Networks |

---

# Cisco NAT Configuration

## Configure Inside Interface

```
interface GigabitEthernet0/0

ip nat inside
```

---

## Configure Outside Interface

```
interface GigabitEthernet0/1

ip nat outside
```

---

## Configure Access List

```
access-list 1 permit 192.168.1.0 0.0.0.255
```

---

## Configure PAT (NAT Overload)

```
ip nat inside source list 1 interface GigabitEthernet0/1 overload
```

---

## Complete Configuration Example

```
interface GigabitEthernet0/0

ip address 192.168.1.1 255.255.255.0

ip nat inside

no shutdown

interface GigabitEthernet0/1

ip address 203.0.113.10 255.255.255.252

ip nat outside

no shutdown

access-list 1 permit 192.168.1.0 0.0.0.255

ip nat inside source list 1 interface GigabitEthernet0/1 overload
```

---

# Verification Commands

Display NAT Translations

```
show ip nat translations
```

Display NAT Statistics

```
show ip nat statistics
```

Display Running Configuration

```
show running-config
```

Display Interface Summary

```
show ip interface brief
```

---

# Example NAT Translation Table

```
Inside Local

192.168.1.10

↓

Inside Global

203.0.113.10
```

---

# Advantages

- Conserves IPv4 addresses.
- Hides internal network addresses.
- Improves network security.
- Allows multiple devices to share one public IP.
- Simplifies internal IP address management.
- Reduces Internet service costs.

---

# Limitations

- Does not provide complete security.
- Can complicate troubleshooting.
- Some applications require additional NAT configuration.
- End-to-end connectivity may be affected.
- Adds processing overhead on the router.

---

# NAT vs PAT

| Feature | NAT | PAT |
|----------|-----|-----|
| Public IPs Required | Multiple | Single |
| Translation | IP Address Only | IP Address + Port |
| Scalability | Moderate | High |
| Internet Access | Limited | Excellent |

---

# Best Practices

- Use PAT for Internet access in enterprise and home networks.
- Reserve Static NAT for publicly accessible servers.
- Document all NAT mappings.
- Monitor NAT translation tables regularly.
- Use firewalls in addition to NAT for enhanced security.
- Verify NAT configuration after deployment.

---

# Important Notes

- NAT stands for **Network Address Translation**.
- NAT translates private IP addresses into public IP addresses.
- PAT is also known as **NAT Overload**.
- Static NAT provides one-to-one mapping.
- Dynamic NAT uses a pool of public IP addresses.
- PAT allows multiple devices to share a single public IP address.
- NAT is commonly configured on routers and firewalls.

---

# Conclusion

Network Address Translation (NAT) is a fundamental technology that enables private networks to communicate with public networks while conserving IPv4 address space. By translating private IP addresses into public addresses, NAT enhances scalability, improves address utilization, and provides an additional layer of privacy for internal devices. Understanding Static NAT, Dynamic NAT, and PAT is essential for configuring modern enterprise and Internet-connected networks.
