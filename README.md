# CCNP - Cisco Certified Network Professional (ENCOR + ENARSI)

## 📘 Syllabus
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

---

**Process Switching**

- Process switching refers to a method where the **router’s CPU** is **directly involved in making forwarding decisions** for **every incoming packet**.  
- This is the **slowest** form of packet switching, as each packet is handled individually in software.

#### Steps:
1. When a packet arrives at the router, it is **stored in memory (buffered)**.  
2. The **CPU performs a lookup** in the **global routing table** to determine the **best path** to the destination.  
3. The CPU then **decrements the TTL (Time-To-Live)** field and **recalculates the IP header checksum**.  
4. The CPU **resolves the next-hop IP address** and finds the **corresponding Layer 2 (MAC) address**.  
5. Finally, the CPU **rewrites the Ethernet header** and **forwards the packet** out of the **appropriate egress interface**.

Note - CPU intensive and can led to high latency and 

###