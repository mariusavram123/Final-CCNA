README.md

This is the documentation for my Final CCNA project.
* This project uses a bit more technologies than their are described in the CCNA 200-301 Cisco's Exam Blueprint:Route redistributions, Point-to-Point Protocol with CHAP authentication.

This project has been build using the Cisco Packet Tracer simulator. You need to have Cisco Packet Tracer installed in order to open the .pkt file provided in this folder.

The configuration for network devices will be added as .txt files.

Description:

Company A, Company B and Company C have just started building their internal networks.
Help them build the configuration and enable connectivity with the data center.


The internal network structures of the companies follows the guidelines offered by cisco:
- Three-tier network design architecture(Core, Distribution and Access layers)
- The collapsed core network design architecture(Core-Distribution layer and Access layer)
- The spine-leaf network design architecture for data centers(Spine and leaf switches)
The Core routers run BGP in different autonomous systems which will enable connectivity between the three companies and the data center.

Company A:

- All PCs in the Company A are in the same VLAN(subnet).
- The routers CA-CORE1 and CA-CORE2 run an HSRP group to provide redundant gateways to client in the network
- Use static and default routes to enable connectivity with the WAN.
- Clients have static IP addresses.
- Uses the collapsed core network design architecture

Company B:
- The company is using 6 VLANs for internal data traffic and the VLAN 70 as a management VLAN for the network.
- Uses EIGRP as an internal routing protocol
- The core switch 2(CS2) acts as a layer 3 inter-vlan routing device
- The CS2 switch also have predetermined DHCP pools for all VLAN's in the company.
- Uses the Three-Tier network design architecture.

Company C:
- The PCs in the Company C are divided into 4 VLANs. VLAN 40 is used for network management and it is used as a native VLAN for the trunk links. The VLANs 10, 20, and 30 are used for data traffic.
- The CC-CORE, company's core router acts as a router-on-a-stick and enable inter-vlan communication.
- Use static routes for connectivity with the WAN.
- Clients have static IP addresses, for every VLAN in the company
- Uses the collapsed core network design architecture

Data Center:
- Uses the Spine-Leaf data center design architecture
- All of the connected ports on the Layer 3 switches acts as a layer 3 port
- Uses OSPF as the internal routing protocol

BGP core routers:

- Uses static routes to enable connectivity
- Uses PPP on serial links
- The PPP links uses CHAP authentication

The final objective:

These companies should be able to reach the web sites on the Data Center branch: google.com and cisco.com using web browsers on their PC's. 
The PC's should also be able to ping the DNS server at 14.0.0.2, and ping google.com and cisco.com using their names.
The network devices should also be able to ping the DNS server at 14.0.0.2 and the web sites cisco.com and google.com using their names.

Technologies used:

- Spanning-tree optimizations
- SSH and Telnet
- EtherChannel
- Subnetting and VLSM
- HSRP
- VLAN's and Inter-VLAN routing on a layer 3 switch and using "router on a stick".
- NAT
- DHCP and static IP addressing
- Static routes
- BGP
- OSPF
- EIGRP
- PPP with CHAP authentication
- Route Redistributions

Objective descriptions:

Company A:
(CCNA-CA-Screenshoot.jpg)

- Configure IP addressing as per diagram. The company is using 192.168.1.0/24 as the internal subnet and 198.51.100.0/30 and 198.51.100.4/30 for WAN link connectivity
- Configure an IP address on the VLAN 1 interface on the switches for management
- Configure the ports between switches as trunks where needed (disable DTP negociations), and the ports between hosts and access layer switches as access ports in vlan 1.
- Configure the CA-D1 switch to be the route bridge for VLAN 1 and set the spanning-tree mode to rapid PVST in all switches in the network
- Configure the last IP address in the subnet on the physical router interface on router CA-CORE1
- Configure the second-last IP address in the subnet on the physical router interface on router CA-CORE2
- Configure the HSRP group 1 between the router interfaces connected to the internal network of the company and use 192.168.1.100 as the virtual IP address
- configure an EtherChannel using the F0/1 and F0/2 interfaces on both CA-D1 and CA-D2 switches and use LACP as the protocol
- Configure NAT/PAT on CA-CORE1 and CA-CORE2 routers and permit all hosts in the subnet 192.168.1.0/24 to be translated to the IP address existent on G0/0/0 interfaces of routers
- Configure static routes so that internal routers can perform HSRP(the two routers have connectivity), and a default route to reach the internet.
- Activate SSH version 2 for management

Company B:
(CCNA-CB-Screenshoot.jpg)

- Configure IP addresses as per diagram.
- You have been allocated the 192.168.2.0/24 range by your ISP to assign on the hosts and network devices of the company, subnet it for your need without wasting addresses. You need minimum 20 addresses for each VLAN
- configure VLANs on all the switches (VLAN 10 to 70) and subnet the IP address range allocated by your ISP. Note that you need another subnet for the connection with the WAN router
- VLAN 70 is used as a management VLAN for network devices and hosts, configure it as native VLAN for the trunk links in the network.
- Configure the trunk links where needed, disable DTP negotiations and set VLAN 70 as native VLAN
- Configure CS2 as the spanning-tree root bridge for all VLANs and the CS1 switch as a secondary root for all VLAN's
- Configure an EtherChannel using the G 1/0/1 and G1/0/2 interfaces on switches both CS2 and CS1
- The CS2 switch should be configured with DHCP pools for each VLAN in the network.(192.168.2.x/27) range for each pool. 
- Exclude the first 5 addresses from each DHCP pool and set the default-gateway of the pool as CS2 VLAN interface IP address.
- Configure an IP address for management on each switches on the VLAN 70 interfaces
- Activate IP routing on the CS2 switch so that it can route traffic between the VLANS
- Activate EIGRP in the Autonomous System 200 on the CB-CORE router and CS2 and advertise all internal VLAN routes and the network between CS2 and CB-CORE router in it.
- Configure NAT/PAT translations and allow all the subnetworks in the 192.168.2.0/24 network to be translated on the IP addressed configured on the G 0/0/0 interface's configured IP address. Enable Overloading.
- Activate SSH version 2 for management

Company C:
(CCNA-CC-Screenshoot.jpg)

- Configure IP addresses as per diagram.
- You have been allocated the 192.168.3.0/24 range by your ISP for internal traffic. Your network is segmented into 4 VLAN's, and you need to have minimum 40 hosts in a subnet. 
- You should use the VLAN 40 as the management VLAN and the native VLAN on the trunk links
- Create all needed VLAN's on the switches
- Optimize spanning-tree so the switch CC-CD1 should be the the primary root bridge for VLANs 10 and 20 and the secondary root bridge for VLANs 30 and 40
- Configure spanning-tree so that the CC-CD2 switch should be the primary root bridge for VLANs 30 and 40 and the secondary root bridge for VLANs 10 and 20
- Configure the G0/0/1 interface on CC-CORE router for router-on-a-stick Inter-VLAN routing using the following network addresses for subinterfaces: 
    Vlan 10: 192.168.3.0/26
    Vlan 20: 192.168.3.64/26
    Vlan 30: 192.168.3.128/26
    Vlan 40: 192.168.3.192/26
- Configure the G0/0/0 interface on CC-CORE router with the IP address as shown in the diagram
- Configure NAT/PAT on the CC-CORE router subinterfaces to translate the internal IP addresses into the G0/0/0 interface's IP address
- Configure a management IP address and activate SSH version 2 for the management of networking devices in the internal network
- Configure a default static route for the network traffic.

Data Center
(Final-CCNA-DC-screenshoot.jpg)

- The data center design resides in Cisco's Spine-Leaf architecture
- The ports between the switches runs as layer 3 ports and they are using public IP addresses
- Configure IP addressing as follows:
    DC-SS1 -> DC-LS1 11.0.0.0/30
    DC-SS1 -> DC-LS2 12.0.0.0/30
    DC-SS1 -> DC-LS3 13.0.0.0/30
    DC-SS2 -> DC-LS1 21.0.0.0/30
    DC-SS2 -> DC-LS2 22.0.0.0/30
    DC-SS2 -> DC-LS3 23.0.0.0/30
    DC-SS3 -> DC-LS1 31.0.0.0/30
    DC-SS3 -> DC-LS2 32.0.0.0/30
    DC-SS3 -> DC-LS3 33.0.0.0/30
    DC-LS1- G1/0/10 14.0.0.0/30- DNS Server
    DC-LS2- G1/0/10 15.0.0.0/30- google.com server
    DC-LS3- G1/0/10 16.0.0.0/30- cisco.com server
- Enable IP routing on switches
- Enable OSPF process ID 1 for all the switches inside the data center and on the Data Center router
- Configure the IP address on the G0/0/0 interface of the Data Center router using the diagram
- Configure a default static route pointing to the ISP router R4 and insert it into OSPF process ID.
- Enable the DNS service on the 14.0.0.2 server and configure IP addressing
- Enable the HTTP and HTTPS services on the 15.0.0.2 and 16.0.0.2 servers and configure IP addressing

BGP Core routers:
(Final-CCNA-BGP-CORE-screenshoot.jpg)

The BGP core routers R1, R2, R3 and R4 run BGP in different autonomous systems.
The connection between serial links is made using Point-to-Point Protocol(PPP), and is using CHAP(Challenge Handshake Authentication Protocol) to for authentication. 
To enable the connection, the routers are using static routes.
- Configure IP addressing as per diagram
- Configure static routes, so that every router can access all the four networks in the BGP core.
- Configure static eBGP peers
- Advertise the public networks into BGP
- On router R1 redistribute the static routes from 198.51.100.0/30 and 198.51.100.4/30 into BGP process for AS 100
- On router R2 redistribute the EIGRP process for AS 200 into BGP AS 200 and vice-versa. Set the metric for EIGRP redistribution as follows 100000 10 255 10 1500 (K1, K2, K3, K4, K5)
- On router R3 redistribute the static routes from the 209.165.202.0/30 and the default routes from the router, into BGP process for AS 300
- On router R4 redistribute the OSPF process ID 1 onto BGP for AS 400 so that all BGP neighbors will learn about the data center networks.
- Enable SSH v2 on all BGP Core routers so that they can be accessed for management.

Final test and verifying the connectivity

- Open a PC's command prompt, from Company A, Company B or Company C and ping 14.0.0.2(DNS server)
- Ping 15.0.0.2 and 16.0.0.2 servers by using domain names(google.com and cisco.com)
- Open an web browser on the pc and browse to google.com and cisco.com. 
- Using a PC, the hosts should be able to ssh into the routers and switches in the topology.

Bugs and other features will be resolved/added in later builds of the project.
