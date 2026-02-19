### Description
This project simulates a realistic corporate network consisting of six departments: IT, Management, Finance, Sales, Staff, and Guest. The network enforces strict access policies:
IT department has unrestricted access to all resources.
Management and Finance can only communicate with IT (and the internet).
Sales and Staff can only reach IT and the central servers.
Guest users are completely isolated and have internet‑only access.
All departments share centralized File and Email servers. The design combines static routing for precise access control and EIGRP for dynamic core routing, demonstrating concepts from Labs 04, 05, and 07 of the course.

###✨ Features
Hierarchical star topology with a central HQ‑Core router (2811).
Static routes enforce isolation between restricted departments.
EIGRP (AS 100) provides dynamic routing between core routers (HQ‑Core, IT, Sales, Staff).
Separate subnets for each department and server network.
Centralized internet access through a dedicated HQ‑Edge router.
Complete end‑to‑end testing verifying all access rules.

### 🛠️ Technologies Used
Cisco Packet Tracer – network simulation and configuration
Routing Protocols:
Static Routing
EIGRP
IP Addressing – private IPv4 addressing (10.0.0.0/8)

### 🗺️ Network Topology
7 Routers: HQ‑Core, HQ‑Edge, IT, Management, Finance, Sales, Staff
6 Switches: One per department
12 PCs: 2 per department
2 Servers: File Server (10.0.2.10), Email Server (10.0.2.20)

### 📡 IP Addressing Scheme
Department	Network	Gateway	PC IPs
IT	10.0.1.0/24	10.0.1.1	.10, .11
Management	10.0.4.0/24	10.0.4.1	.10, .11
Finance	10.0.5.0/24	10.0.5.1	.10, .11
Sales	10.0.6.0/24	10.0.6.1	.10, .11
Staff	10.0.7.0/24	10.0.7.1	.10, .11
Guest	10.0.8.0/24	10.0.8.1	.10, .11
Servers	10.0.2.0/24	10.0.2.1	.10 (File), .20 (Email)
Router‑to‑router links use /30 subnets (10.0.10.0 – 10.0.17.0).

🔧 Configuration Highlights
Static Routing (Access Control)
Management Router (only IT + internet):
ip route 10.0.1.0 255.255.255.0 10.0.13.1
ip route 10.0.2.0 255.255.255.0 10.0.13.1
ip route 200.200.200.200 255.255.255.255 10.0.13.1

Sales Router (only IT + servers):
ip route 10.0.1.0 255.255.255.0 10.0.15.1
ip route 10.0.2.0 255.255.255.0 10.0.15.1

EIGRP Dynamic Routing

HQ‑Core (advertises all point‑to‑point links):
router eigrp 100
 network 10.0.10.0 0.0.0.3
 network 10.0.11.0 0.0.0.3
 network 10.0.13.0 0.0.0.3
 network 10.0.14.0 0.0.0.3
 network 10.0.15.0 0.0.0.3
 network 10.0.16.0 0.0.0.3
 no auto-summary
🧪 Testing Results
All access requirements were verified with ping tests:

### Test	Expected	Result
IT → Management	✅ Success	✅
IT → Sales	✅ Success	✅
Management → Sales	❌ Fail	❌
Sales → Management	❌ Fail	❌
Guest → IT	❌ Fail	❌
Guest → Internet (200.200.200.200)	✅ Success	✅
Screenshots of successful and failed pings are included in the screenshots/ folder.

### 🚀 How to Run
Install Cisco Packet Tracer (version 8.x or later).
Clone this repository or download the .pkt file.
Open .pkt in Packet Tracer.
Explore the configurations or run simulations.
