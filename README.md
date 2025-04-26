# traction-network-integration

<h1>🏢 Traction Solutions – Centralized Network Integration</h1>

> 📡 A full enterprise network design and integration project connecting four South African city branches with centralized administration and optimized traffic management.

---



## 🧠 Project Summary

Designed and implemented a centralized network infrastructure for Traction Solutions, connecting branches in Johannesburg, Durban, Cape Town, and Bloemfontein using VLANs, RIP v2 routing, centralized DHCP, and WAN leased lines. Security, scalability, and traffic prioritization were key design goals.

---

## 🛠 Technologies & Concepts Used

- **Cisco Packet Tracer**
- **RIP v2 Routing Protocol**
- **VLAN Segmentation & Inter-VLAN Routing**
- **Centralized DHCP Server (Bloemfontein)**
- **WAN Leased Line Connections (Point-to-Point)**
- **Wireless LAN Controller (WLC) Setup**
- **QoS for Traffic Prioritization**

---

## 🧩 Environment Overview

- **Johannesburg Office**: 3 VLANs — Finance (VLAN 10), Sales (VLAN 20), HR (VLAN 30)
- **Cape Town Office**: 2 VLANs — Warehouse (VLAN 100), Manufacturing (VLAN 200)
- **Durban Office**: OFFICE LAN setup
- **Bloemfontein Office**: DHCP Server, Mail Server, centralized services
- **Internet Access**: Web Server hosted externally (200.20.20.10)

---

## 📸 Network Design Walkthrough

<p align="center">

Full Network Topology: <br/>
<img src="https://imgur.com/DbCtgv1.png" height="70%" width="70%" alt="Full Network Topology"/>


<br/><br/>
JHB_R1 pinging DBN_R1 AND CPT_R1: <br/>
<img src="https://imgur.com/FJM1kfZ.png" height="70%" width="70%" alt="Full Network Topology"/>


I configured all routers with the IP addresses as specified in the table and tested connectivity between
the routers. Im choosing to just showcase JHB_R1's results to avoid making this READ long. All the Routers have the same or similar results.


<br/><br/>
VLAN and Inter-VLAN Routing Setup: <br/>
<img src="https://imgur.com/sEkbH9W.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/bl8kZWY.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/bjvouAh.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/Viaqxi2.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/ZoEfzuv.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/1qCFvoK.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/nXXpbAI.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/mWBvxsj.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/EblJkMx.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/oK1xe8o.png" height="70%" width="70%" alt="VLAN Configuration"/>
<img src="https://imgur.com/VsusY7n.png" height="70%" width="70%" alt="VLAN Configuration"/>


**Verifying that the PCs in different vlans in JHB and CPT offices can communicate**
<img src="https://imgur.com/xfU73Qb.png" height="70%" width="70%" alt="VLAN Configuration"/>


PC3 of Vlan 10 in JHB can ping: <br/>
•	PC4 of Vlan 20 with IP 192.168.2.4 <br/>
•	PC7 of Vlan 200 with IP 192.168.200.3 in CPT <br/>

<img src="https://imgur.com/AcdfhH6.png" height="70%" width="70%" alt="VLAN Configuration"/>
PC6 of Vlan 100 in CPT can ping: <br/>
•	PC9 of Vlan 200 with IP 192.168.200.4 <br/>
•	PC5 of Vlan 30 with IP 192.168.3.4 in JHB <br/>


<br/><br/>
Centralized DHCP Server Setup: <br/>
<img src="https://imgur.com/SFimnA9.png" height="70%" width="70%" alt="Central DHCP"/>
<img src="https://imgur.com/cQB7wXj.png" height="70%" width="70%" alt="Central DHCP"/>
<img src="https://imgur.com/W8IHcmX.png" height="70%" width="70%" alt="Central DHCP"/>

Configured the DHCP Server with a static IP address and the pools to assign IP addresses and other
parameters to JHB, DBN and CPT computers. The Default pool (serverpool) assigns IP addresses to devices that are in
the local Subnet (BLM).

<br/><br/>
ROUTING Configuration: <br/>
**JHB_R1** <br/> 
router rip <br/>
 version 2 <br/>
 network 192.168.1.0 <br/>
 network 192.168.2.0 <br/>
 network 192.168.3.0 <br/>
 network 30.0.0.0 <br/>
 network 20.0.0.0 <br/>
 no auto-summary <br/>
**DHCP IP helper address on the routers** <br/>
**JHB_R1** <br/>
interface fa0/0 <br/>
no ip address  <br/>
exit <br/>
interface fa0/0.10 <br/>
 encapsulation dot1Q 10 <br/>
 ip address 192.168.1.1 255.255.255.0 <br/>
 ip helper-address 192.168.10.4 <br/>
 exit <br/>
interface fa0/0.20 <br/>
 encapsulation dot1Q 20 <br/>
 ip address 192.168.2.1 255.255.255.0 <br/>
 ip helper-address 192.168.10.4 <br/>
 exit <br/>
interface fa0/0.30 <br/>
 encapsulation dot1Q 30 <br/>
 ip address 192.168.3.1 255.255.255.0 <br/>
 ip helper-address 192.168.10.4 <br/>
 exit

 **Showing all routes configured and learnt using RIPv2 on JHB_R1** <br/>
 <img src="https://imgur.com/HT0gD6K.png" height="70%" width="70%" alt="learned RIPv2 routes"/>
 <img src="https://imgur.com/hOxWInK.png" height="70%" width="70%" alt="learned RIPv2 routes"/>

 **Showing all devices in Johannesburg got IP adresses from DHCP server due to DHCP helper address on JHB_R1** <br/>
 <img src="https://imgur.com/6sLgi91.png" height="70%" width="70%" alt="DHCP IP"/>
 <img src="https://imgur.com/tX4R8RY.png" height="70%" width="70%" alt="DHCP IP"/>
 <img src="https://imgur.com/vmdlcnn.png" height="70%" width="70%" alt="DHCP IP"/>
 

 ps. Again just using JHB_R1 to make the read shorter, all the Routers have the same or similar configurations


<br/><br/>
Wireless LAN Controller Configuration: <br/>
<img src="https://imgur.com/DmDt67c.png" height="70%" width="70%" alt="Wireless LAN Controller"/>
<img src="https://imgur.com/liEYCIn.png" height="70%" width="70%" alt="Wireless LAN Controller"/>
<img src="https://imgur.com/crJ4BIu.png" height="70%" width="70%" alt="Wireless LAN Controller"/>
<img src="https://imgur.com/h2FNTXx.png" height="70%" width="70%" alt="Wireless LAN Controller"/>

 **Configured security settings on the Wireless networks.** <br/>
<img src="https://imgur.com/gMQPscP.png" height="70%" width="70%" alt="Wireless LAN Controller"/>
<img src="https://imgur.com/4GCSdF6.png" height="70%" width="70%" alt="Wireless LAN Controller"/>


<br/><br/>
QoS Implementation for VoIP and Video Conferencing: <br/>
**This part of the project was theoretical so, I used the Johannesburg and Durban networks to illustrate my answer:** <br/>

For JHB_R1 and DBN_R1 <br/>
 Identify and mark traffic types. <br/>
Set priorities and bandwidth for each traffic type. <br/>
As for Interface Configuration, we should apply QoS policies to the outbound interface connecting to DBN_R1 in JHB_R1. In DBN_R1 we should apply QoS policies to the outbound interface connecting to JHB_R1. <br/>

QoS Configuration Details <br/>
Priority Queueing: <br/>
Traffic Type: VoIP, Video Conferencing <br/>
Priority: High <br/>
Class-Based Weighted Fair Queueing: <br/>
Traffic Type: Standard Data <br/>
Priority: Medium <br/>
Low-Latency Queueing: <br/>

Traffic Type: Real-time traffic <br/>
Priority: Highest <br/>

<br/><br/>
ACL Configuration: <br/>
**In this project a constraint that was present was that users of all regions except the Manufacturing VLAN will have access to the WebServer and Mail server.** <br/>
<img src="https://imgur.com/jTs9kyZ.png" height="70%" width="70%" alt="ACL Manufacturing"/>
<img src="https://imgur.com/ZVfsBCH.png" height="70%" width="70%" alt="ACL Manufacturing"/>
<img src="https://imgur.com/oC5sk1P.png" height="70%" width="70%" alt="ACL Manufacturing"/>
<img src="https://imgur.com/jI8LHve.png" height="70%" width="70%" alt="ACL Manufacturing"/>
<img src="https://imgur.com/iLvSgK5.png" height="70%" width="70%" alt="ACL Manufacturing"/>




</p>

---

## 🔒 Key Features Implemented

- RIP v2 dynamic routing across four branches
- Inter-VLAN Routing enabled in Johannesburg and Cape Town
- Centralized DHCP service from Bloemfontein
- Wireless LAN Controller with two SSIDs: **STAFF-WIFI** and **GUEST-WIFI**
- QoS configuration to prioritize VoIP and video traffic
- Web Server and Mail Server reachable from all VLANs except Manufacturing VLAN

---

## 💡 What I Learned

- Configuring RIP v2 for multi-site dynamic routing
- Setting up centralized DHCP across different VLANs and sites
- Managing VLANs and trunking across multi-site enterprise networks
- Implementing Quality of Service (QoS) to optimize network traffic flow
- Deploying and securing Wireless LAN Controllers for enterprise Wi-Fi management

---

## ⚙️ Tools

- **Cisco Packet Tracer**
- **Subnetting and IP Address Planning on Notepad**
- **Packet Tracer Simulation Tools**

---

> 📝 *This repository contains project documentation and screenshots only. Real `.pkt` files and config scripts are not shared publicly to maintain academic integrity and security.*

