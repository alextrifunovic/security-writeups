# Network Routing – Hands-on Lab Writeup

**Topic:** IPv4/IPv6 Subnetting, Static Routing, and Internet Connectivity  
**Context:** Practical networking lab at university level

---

## Overview

In this lab I configured a multi-node network topology from scratch, covering subnetting, static routing, IP forwarding, and internet connectivity — for both IPv4 and IPv6.

### Network Topology

```
internet
   |
 [Node A] (Router)
   |
 [Node B] (Router)
  /     \
[Node C] [Node D]
```

Node B acted as the central router connecting three subnets. Node A connected the internal network to the internet.

---

## What I Learned

### 1. IP Addresses Belong to Interfaces, Not Hosts

A common misconception is that a host "has" an IP address. In reality, IP addresses are always assigned to **network interfaces**. A node with multiple interfaces (like a router) can have multiple IP addresses — one per interface.

### 2. Subnetting

I divided a given IPv4 `/28` block into three `/30` subnets for point-to-point links. Each `/30` provides exactly 2 usable host addresses — one for each end of the link.

For IPv6, subnetting is much simpler. Each network gets a full `/64` block, and new subnets are created by simply incrementing the subnet identifier — no manual boundary calculations needed.

### 3. Routing Tables

Every node (not just routers) has a routing table. It tells the OS where to send packets based on their destination IP. Without a matching route, a packet either goes to the default gateway or gets dropped with "Network is unreachable".

Key insight: **both ends of a connection need a route**. A ping will fail if the request reaches the destination but the reply has no route back.

### 4. IP Forwarding

On Linux, packet forwarding between interfaces is **disabled by default**. A node connected to multiple networks will simply drop packets not addressed to itself unless forwarding is explicitly enabled via a kernel parameter.

This is the key difference between a host and a router — not hardware, but configuration.

### 5. Default Routes

Instead of configuring a specific route for every possible destination, a **default route** (`0.0.0.0/0` for IPv4, `::/0` for IPv6) catches all unmatched packets and forwards them to a gateway. This is how end hosts reach the internet — they just send everything to their router.

### 6. Link-Local vs Global Unicast (IPv6)

IPv6 automatically assigns Link-Local addresses (`fe80::`) to interfaces, but these are only valid on the local link and are not routable. For communication across network boundaries, **Global Unicast Addresses** are required.

### 7. Hosting and Reachability

Once routing and forwarding were configured correctly, nodes deep inside the private network became reachable from the public internet — demonstrating how real server infrastructure works: private subnets, a routing layer, and a public-facing gateway.

---

## Tools Used

| Tool | Purpose |
|------|---------|
| `ipcalc-ng` | Subnet calculation and address info |
| `ip address` | Assign/remove IP addresses on interfaces |
| `ip link` | Bring interfaces up or down |
| `ip route` | View and manage the routing table |
| `sysctl` | Enable IP forwarding (IPv4 and IPv6) |
| `ping` | Test connectivity between nodes |
| `tcpdump` | Capture and inspect network packets |
| `curl` | Send HTTP requests to a web server |

---

## Key Takeaways

- Routing is about knowing the **next hop** toward a destination, not the full path
- A router is just a Linux host with forwarding enabled and multiple network interfaces
- IPv6 makes subnetting significantly easier due to its address structure
- Debugging network issues requires understanding which layer the problem is at — addressing, routing, or forwarding
