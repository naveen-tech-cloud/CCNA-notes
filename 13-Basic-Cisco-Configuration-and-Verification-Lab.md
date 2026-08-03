# Basic Cisco Configuration and Verification Lab

## Introduction

This lab demonstrates the fundamental configuration of a Cisco router. It covers the initial setup, hostname configuration, password protection, interface configuration, configuration saving, and verification commands. These tasks are essential for every network administrator and serve as the foundation for more advanced Cisco networking concepts.

---

# Lab Objectives

After completing this lab, you will be able to:

- Access the Cisco CLI
- Configure the router hostname
- Secure the router using passwords
- Configure a banner message
- Assign an IP address to an interface
- Enable network interfaces
- Save the router configuration
- Verify the configuration using Cisco IOS commands

---

# Lab Topology

```
        +-------------+
        |    PC-1     |
        |192.168.1.10 |
        +------+------+
               |
               |
        GigabitEthernet0/0
        +------+------+
        | Cisco Router|
        +-------------+
```

---

# Lab Requirements

### Hardware

- Cisco Router (ISR Series or Packet Tracer Router)
- One PC
- Console Cable
- Ethernet Cable

### Software

- Cisco Packet Tracer
- Cisco IOS
- Terminal Emulator (PuTTY/Tera Term)

---

# Network Addressing

| Device | Interface | IP Address | Subnet Mask |
|---------|-----------|------------|-------------|
| Router | G0/0 | 192.168.1.1 | 255.255.255.0 |
| PC | NIC | 192.168.1.10 | 255.255.255.0 |

Default Gateway for PC

```
192.168.1.1
```

---

# Step 1 – Access the Router

Connect the console cable between the PC and the router.

Open the terminal emulator and press **Enter**.

CLI appears as:

```
Router>
```

---

# Step 2 – Enter Privileged EXEC Mode

```
Router> enable
```

Output

```
Router#
```

---

# Step 3 – Enter Global Configuration Mode

```
Router# configure terminal
```

Output

```
Router(config)#
```

---

# Step 4 – Configure Hostname

```
Router(config)# hostname BranchRouter
```

Output

```
BranchRouter(config)#
```

---

# Step 5 – Configure Enable Secret Password

```
BranchRouter(config)# enable secret Cisco@123
```

---

# Step 6 – Configure Console Password

```
BranchRouter(config)# line console 0
BranchRouter(config-line)# password Cisco123
BranchRouter(config-line)# login
BranchRouter(config-line)# exit
```

---

# Step 7 – Configure VTY Password

```
BranchRouter(config)# line vty 0 4
BranchRouter(config-line)# password Cisco123
BranchRouter(config-line)# login
BranchRouter(config-line)# exit
```

---

# Step 8 – Configure MOTD Banner

```
BranchRouter(config)# banner motd # Authorized Access Only #
```

---

# Step 9 – Configure Interface IP Address

```
BranchRouter(config)# interface GigabitEthernet0/0

BranchRouter(config-if)# ip address 192.168.1.1 255.255.255.0

BranchRouter(config-if)# no shutdown

BranchRouter(config-if)# exit
```

Expected Message

```
Interface changed state to up
```

---

# Step 10 – Save Configuration

```
BranchRouter# copy running-config startup-config
```

Output

```
Destination filename [startup-config]?

Press Enter

Building configuration...

[OK]
```

---

# Step 11 – Verify Router Configuration

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

Expected Output

```
Interface              IP Address      Status

GigabitEthernet0/0     192.168.1.1     up
```

Display Routing Table

```
show ip route
```

---

# Step 12 – Verify PC Connectivity

From the PC Command Prompt

```
ping 192.168.1.1
```

Expected Output

```
Reply from 192.168.1.1

Packets Sent = 4

Packets Received = 4

Success Rate = 100%
```

---

# Common Verification Commands

| Command | Purpose |
|----------|----------|
| show version | Display IOS version |
| show running-config | View current configuration |
| show startup-config | View saved configuration |
| show ip interface brief | View interface status |
| show interfaces | Display interface details |
| show ip route | Display routing table |
| ping | Test connectivity |
| traceroute | Trace packet path |

---

# Troubleshooting Tips

If the interface is down:

```
no shutdown
```

If the IP address is incorrect:

```
show running-config
```

If the PC cannot communicate:

- Verify IP address
- Verify subnet mask
- Verify default gateway
- Check interface status
- Check cable connections

---

# Best Practices

- Assign meaningful hostnames.
- Configure secure passwords.
- Save the configuration after every major change.
- Verify interface status before testing connectivity.
- Document IP addressing.
- Use descriptive interface names where possible.

---

# Important Notes

- Interfaces remain **administratively down** until the `no shutdown` command is issued.
- Running Configuration is stored in **RAM**.
- Startup Configuration is stored in **NVRAM**.
- Always verify configurations after applying changes.
- Save the running configuration to avoid losing changes after a reboot.

---

# Conclusion

This lab introduced the basic configuration and verification of a Cisco router. By completing this exercise, you learned how to configure device identity, secure administrative access, assign IP addresses, activate interfaces, save configurations, and verify network connectivity. These foundational tasks are essential for managing Cisco devices in both academic labs and enterprise environments.
