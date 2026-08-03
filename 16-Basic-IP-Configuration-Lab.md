# Basic IP Configuration Lab

## Introduction

This lab demonstrates how to configure IP addresses on Cisco router interfaces and end devices. It also explains how to verify connectivity using Cisco IOS commands and basic troubleshooting techniques. IP addressing is the foundation of network communication, and every network administrator must understand how to configure and verify IP settings correctly.

---

# Objectives

After completing this lab, you will be able to:

- Configure IP addresses on Cisco router interfaces
- Configure IP settings on a PC
- Enable router interfaces
- Verify interface status
- Test network connectivity
- Troubleshoot basic IP configuration issues

---

# Lab Topology

```
          +----------------+
          |      PC1       |
          |192.168.10.10   |
          +-------+--------+
                  |
                  |
          GigabitEthernet0/0
          +-------+--------+
          | Cisco Router   |
          |     R1         |
          +----------------+
```

---

# Lab Requirements

### Hardware

- Cisco Router
- One PC
- Ethernet Cable

### Software

- Cisco Packet Tracer
- Cisco IOS

---

# IP Addressing Table

| Device | Interface | IP Address | Subnet Mask | Default Gateway |
|----------|-----------|------------|-------------|-----------------|
| R1 | G0/0 | 192.168.10.1 | 255.255.255.0 | N/A |
| PC1 | NIC | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |

---

# Step 1: Enter Privileged EXEC Mode

```
Router> enable
```

Output

```
Router#
```

---

# Step 2: Enter Global Configuration Mode

```
Router# configure terminal
```

Output

```
Router(config)#
```

---

# Step 3: Configure Router Interface

```
Router(config)# interface GigabitEthernet0/0
```

Assign IP Address

```
Router(config-if)# ip address 192.168.10.1 255.255.255.0
```

Enable the Interface

```
Router(config-if)# no shutdown
```

Exit Interface Mode

```
Router(config-if)# exit
```

---

# Step 4: Save Configuration

```
Router# copy running-config startup-config
```

Expected Output

```
Destination filename [startup-config]?

Press Enter

Building configuration...

[OK]
```

---

# Step 5: Configure PC IP Address

Open the PC Network Settings.

Configure the following:

```
IP Address

192.168.10.10

Subnet Mask

255.255.255.0

Default Gateway

192.168.10.1
```

---

# Step 6: Verify Router Interface

```
show ip interface brief
```

Expected Output

```
Interface              IP Address        Status

GigabitEthernet0/0     192.168.10.1      up
```

---

# Step 7: Verify Running Configuration

```
show running-config
```

Verify:

- Interface IP Address
- Subnet Mask
- Interface Status

---

# Step 8: Test Connectivity

From PC

```
ping 192.168.10.1
```

Expected Result

```
Reply from 192.168.10.1

Packets: Sent = 4

Received = 4

Lost = 0
```

Success Rate

```
100%
```

---

# Step 9: Verify from Router

Ping the PC

```
ping 192.168.10.10
```

Expected Result

```
!!!!!

Success rate is 100 percent
```

---

# Useful Verification Commands

Display Interface Summary

```
show ip interface brief
```

Display Running Configuration

```
show running-config
```

Display Startup Configuration

```
show startup-config
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

# Common Configuration Errors

### Interface is Administratively Down

Solution

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

### Incorrect Subnet Mask

Check both:

- Router
- PC

Both must use the same subnet mask.

---

### Wrong Default Gateway

The PC Default Gateway must be the IP address of the connected router interface.

Example

```
192.168.10.1
```

---

### Cable Issues

Verify:

- Ethernet cable connection
- Interface LEDs
- Packet Tracer cable type

---

# Troubleshooting Checklist

- Verify cable connections.
- Verify IP address.
- Verify subnet mask.
- Verify default gateway.
- Ensure interface is enabled.
- Use `show ip interface brief`.
- Use `ping` to test connectivity.

---

# Best Practices

- Assign IP addresses according to an IP addressing plan.
- Always configure meaningful interface descriptions.
- Verify interface status after configuration.
- Save the configuration after successful testing.
- Document all assigned IP addresses.
- Test connectivity after every configuration change.

---

# Important Notes

- Router interfaces remain disabled until the `no shutdown` command is applied.
- Every interface must have a unique IP address.
- Devices must be in the same subnet to communicate directly.
- Always configure the correct default gateway on end devices.
- Verify configurations before proceeding to advanced routing.

---

# Conclusion

This lab demonstrated the basic process of configuring IP addresses on Cisco routers and end devices. Correct IP addressing, interface activation, and connectivity verification are essential skills for every network administrator. Mastering these tasks provides the foundation for advanced routing, switching, and enterprise network configuration.
