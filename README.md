# CCNP - Cisco Certified Network Professional (ENCOR + ENARSI)

## Syllabus
- Types of Planes  
- Packet Switching  

---

### Type of Plane

**Management Plane**  
- **Purpose:** Used to **manage, monitor, and configure** the device.  
- **Traffic Type:** **Administrative traffic** between a network administrator and the device.  
- **Examples:** SSH, Telnet, SNMP, Syslog, NTP  
- **Handled by:** CPU  

**Control Plane**  
- **Purpose:** Responsible for building and maintaining routing and switching tables — it’s the **brain** of the device.  
- **Traffic Type:** Traffic generated **by the device** for network control purposes.  
- **Examples:** Routing Protocols (OSPF, EIGRP, BGP), STP, ARP, CDP, LLDP  
- **Function:** Updates tables used by the Data Plane.  
- **Handled by:** CPU  

**Data Plane**  
- **Purpose:** Forwards **user data packets** based on the information built by the control plane.  
- **Traffic Type:** Real user or application traffic.  
- **Examples:** Forwarding packets using routing/MAC tables, QoS marking, ACL filtering, NAT translation.  
- **Handled by:** **ASICs** (hardware chips designed to perform specific tasks very efficiently).  

---

### Packet Switching

- When a router **receives a packet** on an **ingress interface**, it decides the **appropriate egress interface** to forward that packet — this process is called **packet switching**.  
- Packet switching performance is mainly influenced by the **Control Plane** and the **Data Plane**.

**Process Switching**

- Process switching refers to a method where the **router’s CPU** is **directly involved in making forwarding decisions** for **every incoming packet**.  
- This is the **slowest** form of packet switching
- **Per-Packet Load Balancing**

**Steps:**
1. When a packet arrives at the router, it is **stored in memory (buffered)**.  
2. The **CPU performs a lookup** in the **global routing table** to determine the **best path** to the destination.  
3. The CPU then **decrements the TTL (Time-To-Live)** field and **recalculates the IP header checksum**.  
4. The CPU **resolves the next-hop IP address** and finds the **corresponding Layer 2 (MAC) address**.  
5. Finally, the CPU **rewrites the Ethernet header** and **forwards the packet** out of the **appropriate egress interface**.

To enable -

```bash
ip route-cache switching process
```

Note:
processs switching can also be enabled if you disable fast switching & CEF
To disable fast switching - no ip route-cache
To disable cef switching - no ip cef

Note - CPU intensive lead to high latency and reduce throughput

What is latency and throughput?

Latency
- time delay between when a request is sent and when the response begins to arrive. 
- how long it takes the first drop of water to travel through the pipe.

Throughput 
- amount of data successfully transferred over a network per unit time. 
- how much water flows per second.

**Fast Switching**
- Aka **“process once and switch many times”**
- **Load balancing:** per-destination
- **How it works:**
  1. First packet of a flow goes to **CPU / route processor** to check the **RIB** (control plane)
  2. Router saves **next-hop & outgoing interface** in **fast cache / Switch Engine** (data plane)
  3. **Susequent packets to same destination** use this **cache**, no CPU needed


Drawback of Fast Switching
- Cache entries expiry
- Limited cache size
- Not synchronized to RIB which can create issue dynamic network changes


**CEF - Cisco Express Forwarding**
- Maintain two table in data plane - FIB (Forwarding Information Base)