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

The same network can also be written using CIDR notation: `192.168.1.20/24`

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

## 7. TCP & UDP

### TCP

TCP stands for Transmission Control Protocol

TCP provides reliable communication between devices.

It helps ensure:
- Data is delivered reliably
- Data arrives in the correct order
- Lost data can be retransmitted

TCP is connection-oriented, meaning a connection is established before data is exchanged.

> **Remember**  
> TCP = reliable and connection-oriented

*Common Examples:*  
- HTTP/HTTPS
- SSH
- RDP

---

#### TCP 3-Way Handshake

Before TCP communication begins, the client and server establish a connection.

The simplified process is:

```text
Client                      Server
    SYN  ------------------->

         <-------------------  SYN-ACK

    ACK  -------------------->

Connection established
```

> **Remember**  
> SYN → SYN-ACK → ACK

---

### UDP

UDP stands for User Datagram Protocol.

UDP is connectionless and has lower overhead than TCP.

It does not provide the same reliability and ordering guarantees as TCP.

UDP is useful when speed and low overhead are more important than guaranteed delivery.

*Examples:*
- DNS queries
- Voice/video communication
- Online gaming
- Real-time applications

> **Remember**  
> UDP = lightweight and connectionless

---

### TCP vs UDP

| TCP | UDP |
|---|---|
| Connection-oriented | Connectionless |
| Reliable delivery | No delivery guarantee |
| Data is ordered | No guarantee of order |
| More overhead | Lower overhead |

---

## 8. Ports

An IP address identifies a device/interface.

A port identifies a service or application endpoint on that device.

Think of it like:

IP = Building  
Port = Door

*Example: `192.168.1.50:443`*

This means port 443 on the device with IP address `192.168.1.50`.

---

### Common Ports

| Port | Service |
|---|---|
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 389 | LDAP |
| 445 | SMB |
| 1433 | Microsoft SQL Server |
| 3306 | MySQL |
| 3389 | RDP |
| 5432 | PostgreSQL |

---

## 9. Testing a Port

On Windows, PowerShell can be used to test whether a TCP connection can be established to a specific port.

```powershell
Test-NetConnection 192.168.1.50 -Port 443
```

If the result shows:

```text
TcpTestSucceeded : True
```

The TCP connection to that port succeeded.

If the result shows:

```text
TcpTestSucceeded : False
```

The TCP connection to that port failed.

Possible causes include:
- Firewall blocking the port
- Service is not listening
- Wrong port
- Network security rule
- Application configuraiton problem

### Important

A successful ping does not mean that every port on the server is reachable.

For Example:

```text
ping 192.168.1.50
→ Works

TCP port 443
→ Fails
```

This means the server can be reachable while port 443 is unavailable.

---

## 10. HTTP & HTTPS

### HTTP

HTTP stands for Hypertext Transfer Protocol.

It is commonly used for web communication.

Default port: `80`

HTTP does not provide encryption by itself.

### HTTPS

HTTPS stands for Hypertext Transfer Protocol Secure.

It is HTTP communicaiton secured using TLS encryption.

Default port: `443`

> **Remember**  
> ```text
> HTTP  → 80
> HTTPS → 443
> ```

---

## 11. Firewall

A firewall controls network traffic based on configured rules.

It can allow or block trafic based on things such as:
- Source IP
- Destination IP
- Port
- Protocol
- Network profile
- Application or service

A firewall can sit between a client and a server and decide whether the connection is allowed.

*Example:*

```text
Client → TCP 443 → Firewall → Web Server
```

If the firewall allows TCP 443, the connection can continue.

If the firewall blocks TCP 443, the connection will fail.

> **Important**  
> A server can be:
> - Powered on
> - Reachable by ping
> - Running normally
>
> and still be inaccessible on a specific port because firewall is blocking the traffic.

### Windows Firewall

Windows includes a built-in firewall called: **Windows Defender Firewall**

PowerShell can be used to inspect firewall rules.

```powershell
Get-NetFirewallRule
```

You can also use:

```powershell
Get-NetFirewallProfile
```

to view firewall profiles and their settings.

#### Common firewall profiles

- Domain
- Private
- Public

---

## 12. Network Troubleshooting

When troubleshooting a network problem, don't immediately assume that the server or application is broken.

Start by identifying where the failure occurs.

A simplified troubleshooting approach:

1. Check the device/server status
2. Check the IP configuration
3. Check the network reachability
4. Check DNS/name resolution
5. Check whether the required port is reachable
6. Check whether the required service is running
7. Check firewall and security rules
8. Check application configuration and logs

Use the results of each test to narrow down the possible cause.

### Example

A user cannot access:
```text
https://server.company.com
```

You check:
```text
Ping server.company.com
→ Works

nslookup server.company.com
→ Returns the correct IP

Test-NetConnection server.company.com -Port 443
→ TcpTestSucceeded: False
```

This tells us:

- The server is reachable
- DNS resolution is working
- TCP port 443 cannot be reached

Next, investigate:

- Firewall rules
- whether the web service is listening on port 443
- Network security rules
- Server/application configuration

---

## Networking Quick Reference

| Concept | Main Purpose |
|---|---|
| IP Address | Identifies a device/interface|
| Private IP | Address used inside private networks |
| Loopback | Refers to the local computer |
| Subnet Mask | Determines network/host portions |
| Gateway | Provides a path to other networks |
| DNS | Resolves hostname → IP |
| DHCP | Automatically provides network configuration |
| TCP | Reliable, connection-oriented communication |
| UDP | Connectionless, lightweight communication |
| Port | Identifies a service/application endpoint |
| Firewall | Controls network traffic |
| HTTP | Web communication, port 80 |
| HTTPS | Secure wev communication, port 443 |

---
