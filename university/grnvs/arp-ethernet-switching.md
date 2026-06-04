# ARP & Ethernet Switching — GRNVS Praxis Lab

**Platform:** TUM Testbed  
**Course:** IN0010 GRNVS — Prof. Dr.-Ing. Georg Carle  
**Topics:** ARP, Ethernet Switching, Linux Bridge  
**Tags:** `ARP` `Ethernet` `Layer2` `tcpdump` `Wireshark` `Linux` `Networking`  
**Goal:** Configure a network topology, analyze ARP and ICMP traffic, and enable communication between multiple nodes via a software-defined switch.

---

## What I Did

**1. IP Configuration**
Assigned valid IPv4 addresses from a /28 subnet to each testbed node
using the `ip address` command.

**2. Traffic Capture & Analysis**
Used `tcpdump` to capture ARP and ICMP traffic between nodes and 
analyzed it with Wireshark. Observed the full ARP resolution process — 
the OS automatically sends an ARP broadcast request to resolve an IP 
address to a MAC address before sending the first Ethernet frame.

**3. Neighbor Cache**
Flushed the neighbor cache to force a fresh ARP exchange, then observed 
the resulting IP → MAC mappings using `ip neighbor`.

**4. Linux Bridge (Software Switch)**
Configured a node as a software-defined switch by creating a Linux bridge 
interface and attaching physical interfaces as ports. Analyzed the 
switching table to observe how the switch dynamically learns MAC addresses 
from passing traffic.

**5. End-to-End Communication**
Successfully pinged between all nodes through the switch.

---

## Tools Used

- `tcpdump` — packet capture
- `Wireshark` — traffic analysis
- `ip` — network interface configuration
- `bridge` — switching table inspection

---

## Security Angle

**ARP Spoofing**
ARP has no authentication — any node can reply to an ARP request with a
forged MAC address. This allows a Man-in-the-Middle attack where an
attacker intercepts traffic intended for another node.

Mitigation: Dynamic ARP Inspection (DAI) on managed switches, static ARP
entries for critical hosts.

---


## Lessons Learned

- ARP resolution happens automatically before the first packet is sent
- The neighbor cache prevents redundant ARP requests
- A Linux host can function as a software switch using bridge interfaces
- ARP has no built-in security — a fundamental weakness of Layer 2
