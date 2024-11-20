To configure static routing between **Router 0** and **Router 1** in **Packet Tracer**, follow these steps based on your provided IP addresses:

### **Router Configuration**

#### **Router 0 Configuration**
1. Assign IP addresses to interfaces:
   ```bash
   enable
   configure terminal
   interface gigabitEthernet 0/0
   ip address 192.168.1.1 255.255.255.0
   no shutdown
   exit
   
   interface serial 0/0
   ip address 10.0.0.2 255.0.0.0
   no shutdown
   exit
   ```

2. Add a static route for the 192.168.11.0/24 network (connected to Router 1):
   ```bash
   ip route 192.168.11.0 255.255.255.0 10.0.0.3
   ```

#### **Router 1 Configuration**
1. Assign IP addresses to interfaces:
   ```bash
   enable
   configure terminal
   interface gigabitEthernet 0/0
   ip address 192.168.11.1 255.255.255.0
   no shutdown
   exit
   
   interface serial 0/0
   ip address 10.0.0.3 255.0.0.0
   no shutdown
   exit
   ```

2. Add a static route for the 192.168.1.0/24 network (connected to Router 0):
   ```bash
   ip route 192.168.1.0 255.255.255.0 10.0.0.2
   ```

---

### **Verification Commands**
After configuring both routers, verify the connectivity:

1. **On Router 0:**
   ```bash
   ping 192.168.11.1
   ```
   This tests connectivity to Router 1's GigabitEthernet interface.

2. **On Router 1:**
   ```bash
   ping 192.168.1.1
   ```
   This tests connectivity to Router 0's GigabitEthernet interface.

3. Check routing table:
   ```bash
   show ip route
   ```

---

### **Topology Summary**
- **Router 0:**
  - Gig0/0: 192.168.1.1/24
  - Serial0/0: 10.0.0.2/30
  - Static route: `192.168.11.0/24 -> 10.0.0.3`

- **Router 1:**
  - Gig0/0: 192.168.11.1/24
  - Serial0/0: 10.0.0.3/30
  - Static route: `192.168.1.0/24 -> 10.0.0.2`

This configuration establishes communication between the two routers and their respective local networks.
