# Three Router Configuration Lab

## Introduction

This lab demonstrates how to configure three Cisco routers to communicate with each other using static routing. It covers IP address assignment, interface configuration, route configuration, connectivity verification, and troubleshooting.

This is one of the fundamental routing labs for CCNA learners and helps in understanding how packets travel across multiple networks.

---

# Objectives

After completing this lab, you will be able to:

- Configure IP addresses on router interfaces
- Configure Serial interfaces
- Configure Static Routes
- Verify routing tables
- Test end-to-end connectivity
- Troubleshoot routing issues

---

# Network Topology

```
        LAN 1
 192.168.1.0/24
        |
      PC1
        |
    G0/0
     R1
S0/0/0 |
--------|----------------
        |
     S0/0/0
       R2
S0/0/1 |
--------|----------------
        |
     S0/0/0
       R3
    G0/0
        |
      PC2
        |
192.168.3.0/24
```

---

# IP Addressing Table

| Device | Interface | IP Address | Subnet Mask |
|---------|-----------|------------|-------------|
| R1 | G0/0 | 192.168.1.1 | 255.255.255.0 |
| R1 | S0/0/0 | 10.0.12.1 | 255.255.255.252 |
| R2 | S0/0/0 | 10.0.12.2 | 255.255.255.252 |
| R2 | S0/0/1 | 10.0.23.1 | 255.255.255.252 |
| R3 | S0/0/0 | 10.0.23.2 | 255.255.255.252 |
| R3 | G0/0 | 192.168.3.1 | 255.255.255.0 |
| PC1 | NIC | 192.168.1.10 | 255.255.255.0 |
| PC2 | NIC | 192.168.3.10 | 255.255.255.0 |

---

# Configure Router R1

```
enable

configure terminal

hostname R1

interface GigabitEthernet0/0

ip address 192.168.1.1 255.255.255.0

no shutdown

exit

interface Serial0/0/0

ip address 10.0.12.1 255.255.255.252

clock rate 64000

no shutdown

exit
```

Configure Static Route

```
ip route 192.168.3.0 255.255.255.0 10.0.12.2
```

---

# Configure Router R2

```
enable

configure terminal

hostname R2

interface Serial0/0/0

ip address 10.0.12.2 255.255.255.252

no shutdown

exit

interface Serial0/0/1

ip address 10.0.23.1 255.255.255.252

clock rate 64000

no shutdown

exit
```

Configure Static Routes

```
ip route 192.168.1.0 255.255.255.0 10.0.12.1

ip route 192.168.3.0 255.255.255.0 10.0.23.2
```

---

# Configure Router R3

```
enable

configure terminal

hostname R3

interface GigabitEthernet0/0

ip address 192.168.3.1 255.255.255.0

no shutdown

exit

interface Serial0/0/0

ip address 10.0.23.2 255.255.255.252

no shutdown

exit
```

Configure Static Route

```
ip route 192.168.1.0 255.255.255.0 10.0.23.1
```

---

# Configure PC1

```
IP Address

192.168.1.10

Subnet Mask

255.255.255.0

Default Gateway

192.168.1.1
```

---

# Configure PC2

```
IP Address

192.168.3.10

Subnet Mask

255.255.255.0

Default Gateway

192.168.3.1
```

---

# Save Configuration

Execute on each router

```
copy running-config startup-config
```

---

# Verification Commands

Display Interface Summary

```
show ip interface brief
```

Display Routing Table

```
show ip route
```

Display Running Configuration

```
show running-config
```

Verify Connected Interfaces

```
show interfaces
```

---

# Connectivity Test

From PC1

```
ping 192.168.3.10
```

Expected Result

```
Reply from 192.168.3.10

Packets Sent = 4

Packets Received = 4

Success Rate = 100%
```

---

Trace the Packet Path

```
tracert 192.168.3.10
```

Expected Path

```
PC1

↓

R1

↓

R2

↓

R3

↓

PC2
```

---

# Routing Table Example

```
show ip route
```

Output

```
C    192.168.1.0/24

S    192.168.3.0/24

C    10.0.12.0/30
```

---

# Troubleshooting

### Interface Down

```
no shutdown
```

---

### Incorrect IP Address

Verify

```
show running-config
```

---

### Static Route Missing

Verify

```
show ip route
```

If required, reconfigure the missing route.

---

### Serial Interface Issue

Check:

- Cable Connection
- Clock Rate (DCE Side)
- Interface Status

Verify

```
show controllers serial
```

---

### Ping Failure

Verify:

- Interface IP Address
- Subnet Mask
- Default Gateway
- Static Routes
- Interface Status

---

# Best Practices

- Assign IP addresses according to a documented addressing plan.
- Configure meaningful hostnames.
- Label router interfaces.
- Save configurations after every successful change.
- Verify routing tables before testing connectivity.
- Document all static routes.

---

# Important Notes

- Every router interface must belong to a different network.
- Serial links commonly use **/30 subnet masks** for point-to-point communication.
- Configure **clock rate** only on the DCE end of the serial connection.
- Static routes must be configured on each router to enable communication between remote networks.
- Always verify configurations using **show** commands before testing connectivity.

---

# Conclusion

This lab demonstrated the complete configuration of a three-router network using static routing. By assigning IP addresses, enabling interfaces, configuring static routes, and verifying connectivity, multiple LANs can communicate successfully through intermediate routers. This exercise provides a strong foundation for understanding routing concepts before progressing to dynamic routing protocols such as RIP, OSPF, and EIGRP.
