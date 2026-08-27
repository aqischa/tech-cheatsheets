# Networking Fundamentals

A quick reference for networking concepts, troubleshooting, and common commands.

---

## 1. IP Address

### What is an IP address?

An IP address is a unique address used to identify a device/interface on a network.

Think of it like a home address:
- The IP tells the network where the device is.
- Other devices use the IP to send data to it.

*Example: `192.168.1.20`*

### Private IP addresses

Private IP addresses are commonly used inside local/private networks.

Common private ranges:
- 10.x.x.x
- 172.16.x.x - 172.31.x.x
- 192.168.x.x

*Example: `192.168.1.20`*

Private IP addresses are normally not directly reachable from public internet.

---

## 2. Loopback

Loopback refers to the local computer itself

Common loopback address: `127.0.0.1`

You may also see: `localhost`

*Example: `http://localhost:8080`*

This means the computer is trying to access port 8080 on itself.

> **Remember**  
> 127.0.0.1 == this computer

---

## 3. Subnet Mask

A subnet mask helps determine which part of an IP address represents the network and which part represents the host/device.

*Example:*

*IP address:*
*`192.168.1.20`*

*Subnet mask:*
*`255.255.255.0`*

The same network can also be written using CIDR notation: `192.168.1.29/24`

> For now, **remember**:  
> - /24 commonly corresponds to `255.255.255.0`
> - Devices in the same subnet can normally communicate directly with each other.

---

## 4. Default Gateway

The default gateway is the device that forwards traffic from the local network to other network.

Usually this is a router.

*Example:*

```text
┌─────────────────┐       ┌─────────────────┐       ┌──────────────┐
│ PC              │       │ Gateway         │       │ Internet     │
│ 192.168.1.20    │ ────► │ 192.168.1.1     │ ────► │              │
└─────────────────┘       └─────────────────┘       └──────────────┘
```

> **Remember:**  
> Gateway == the way out of your local network.  
> If the destination is outside your local network, the computer normally sends the traffic to the default gateway.

--- 

## 5. DNS

DNS stands for Domain Name System.

DNS translates/resolves human-readable hostnames into IP addresses.

*Example:*

```text
google.com
    ⇓
   DNS
    ⇓
IP address
```

Instead of remembering an IP address, users can use a hostname such as:  
`google.com`

### Useful command

```powershell
nslookup google.com
```

This can be used to check DNS resolution

### Troubleshooting clue

If:

```text
ping 8.8.8.8    → works
ping google.com → fails
```

DNS/name resolution is one of the first things to investigate.

> **Remember**  
> DNS = hostname → IP address

---

## 6. DHCP

DHCP stands for Dynamic Host Configuration Protocol.

DHCP automatically provides network configuration to devices.

It can provide:
- IP address
- Subnet mask
- Default gateway
- DNS server

Without DHCP, these settings may need to be configured manually.

### Common troubleshooting clue

If a Windows computer has an address such as:

`169.254.x.x`

It may indicate that the computer could not obtain an IP address from the DHCP server.

This is called an APIPA address.

> **Remember**  
> DHCP = automatic network configuration

---

## Quick Comparison

| Concept | Main Purpose |
|---|---|
| IP Address | Identifies a device/interface|
| Private IP | Address used inside private networks |
| Loopback | Refers to the local computer |
| Subnet Mask | Determines network/host portions |
| Gateway | Provides a path to other networks |
| DNS | Resolves hostname → IP |
| DHCP | Automatically provides network configuration |

---

## Troubleshooting Mindset

When troubleshooting a network problem, don't immediately assume the server or application is broken.

Start by identifying which layer is failing.

A simplified approach:

1. Is the device/server reachable?
2. Does it have the correct IP configuration?
3. Does the hostname resolve correctly?
4. Can the required port be reached?
5. Is the service running?
6. Is the application working?
7. Are there firewall or security rules blocking the connection?
8. Check relevant logs and configuration.

Use the evidence from each test to narrow down the problem.

---
