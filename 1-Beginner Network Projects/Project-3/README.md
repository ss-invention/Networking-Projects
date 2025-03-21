## Project-3 : Campus Area Network Design and Implementation for an University.

Albion University is a large university which has two campuses situated 20 miles apart. The university's students and staff are distributed in 4 faculties; these include the faculties of Health and Sciences; Business; Engineering/Computing and Art/Design. Each member of staff has a PC and students have access to PCs in the labs.

1. Create a network topology with the main components to support the following: 

    *  Main campus: 
        - **Building A:** Administrative staff in the departments of management, HR and finance. The admin staff PCs are distributed in the building offices and it is expected that they will share some networking equipment (Hint: use of VLANs is expected here). The Faculty of Business is also situated in this building. 
       - **Building B:** Faculty of Engineering and Computing and Faculty of Art and Design. 
       - **Building C:** Students' labs and IT department. The IT department hosts the University Web server and other servers. 
       - There is also an email server hosted externally on the cloud. 

    *  Smaller campus: 
       - Faculty of Health and Sciences (staff and students' labs are situated on separate floors). 

2. You will be expected to configure the core devices and few end devices to provide end-to-end connectivity and access to the internal servers and the external server. 
   - Each department/faculty is expected to be on its own separate IP network. 
   - The switches should be configured with appropriate VLANs and security settings. 
   - RIPv2 will be used to provide routing for the routers in the internal network and external server. 
   - The devices in building A will be expected to acquire dynamic IP addresses from a router-based DHCP server.

### Tasks:
- **Task 1 :** Your task is to plan, design, and prototype the network topology for Albion University's network using Cisco Packet Tracer. 
- **Task 2 :** Configure in Packet Tracer the network with appropriate settings to achieve the connectivity and functionalities specified in the requirements.


## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
- [Network Design](#network-design)
- [Network Configuration](#network-configuration)
- [Verification](#verification)
- [Conclusion](#conclusion)
- [Author](#author)
- [License](#license)
- [Contributing](#contributing)

## 1. Introduction
Albion University consists of two campuses located 20 miles apart. This document outlines the network design, configuration, and implementation using Cisco Packet Tracer to support the university’s administrative and academic functions efficiently.

## 2. Installation
To run this file ([ Campus Area Network Design & Implementation.pkt ](Campus%20Area%20Network%20Design%20%26%20Implementation.pkt))), We need a Network Simulation Software Tool - **Cisco Packet Tracer**. 

Click [here](https://archive.org/download/cpt822/CiscoPacketTracer822_64bit_setup_signed.exe) to download the **Cisco Packet Tracer** software tool (for Windows OS).

Click [here](https://archive.org/download/cpt822/CiscoPacketTracer822_amd64_signed.deb) to download the **Cisco Packet Tracer** software tool (for Linux OS).

Click [here](https://archive.org/download/cpt822/CiscoPacketTracer822_setup_mac_signed.dmg) to download the **Cisco Packet Tracer** software tool (for Mac OS).

## 3. Usage
This network design ensures efficient communication among faculty, students, and administrative staff by providing secure, reliable, and scalable connectivity between departments, buildings, and campuses.

## 4. Network Design

### 4.1. Main Components :

- **Routers:** 

   - Cisco Router - 2911 Series (3 unit) - One for Main Campus Network, another one for Branch Campus Network and last one for Cloud of Main Campus Network.

- **Switches:** 

   - Cisco L3 Switch - 3650 Series (2 unit) - One for Main Campus Network, and another one for Branch Campus Network.
   - Cisco L2 Switches - 2960 Series (10 units) - Eight for each Department of Main Campus Network and Two for each Department of Branch Campus Network.

- **PCs & Printer:** 

   - One PC and One Printer for each Department of Main Campus and Branch Campus Network.

- **Servers:**

   - One for WEB and One for FTP in IT Department.

- **Cloud-Based Email Server:** 

   - Hosted externally.

### 4.2. Network Topology :

- Main Campus:

   - **Building A:** VLAN-based network for administrative staff (Admin, HR, Finance) and the Faculty of Business.
   - **Building B:** Faculty of Engineering and Computing, Faculty of Art and Design.
   - **Building C:** Student labs and IT department (hosts University Web Server and other servers).

- Branch Campus:
   - Faculty of Health and Sciences: Separate VLANs for Staff and Student labs.

### 4.3. VLAN Implementation

VLAN implement on switches to separate network traffic.

- For each Departments of the Main Campus Network -->

  |VLAN ID|Department/Faculty|
  |----|----|
  |10|ADMIN|
  |20|HR|
  |30|FINANCE|
  |40|BUSINESS|
  |50|ENGINEERING & COMPUTING|
  |60|ART & DESIGN|
  |70|STUDENT LAB|
  |80|IT|

- For each Departments of the Branch Campus Network -->

  |VLAN ID|Department/Faculty|
  |----|----|
  |90|STAFF|
  |100|STUDENT LAB|

### 4.4. IP Addressing Scheme

Each campus will have its own IP network.

- Connect Main Campus to Branch Campus we use **(10.10.10.0/30)** this IP network.  
- Connect Main Campus to Cloud we use **(10.10.10.4/30)** this IP network. 
- Connect Cloud to Email Server we use **(20.0.0.0/30)** this IP network.

### 4.5. Routing Protocol

- RIPv2 is used for internal routing between campuses and also used in external cloud-based email server.

Here, are the Network Infrastructure for Albion University.

<img src="1-Beginner Network Projects/Project-3/Campus Area Network Design & Implementation.png" alt="Campus Area Network Design & Implementation">

## 5. Network Configuration

### 5.1. VLAN Configuration

Configure VLANs on each L2 Switches of the Main Campus Network -->

- **Admin-Switch:**

      Switch>en
      Switch#config t
      Switch(config)#hostname ADMIN-SWITCH
      ADMIN-SWITCH(config)#vlan 10
      ADMIN-SWITCH(config-vlan)#name ADMIN
      ADMIN-SWITCH(config-vlan)#int range f0/1-24
      ADMIN-SWITCH(config-if-range)#switchport mode access
      ADMIN-SWITCH(config-if-range)#switchport access vlan 10

- **HR-Switch:**

      Switch>en
      Switch#config t
      Switch(config)#hostname HR-Switch
      HR-Switch(config)#vlan 20
      HR-Switch(config-vlan)#name HR
      HR-Switch(config-vlan)#int range f0/1-24
      HR-Switch(config-if-range)#switchport mode access
      HR-Switch(config-if-range)#switchport access vlan 20

- **Finance-Switch:**

      Switch>en
      Switch#config t
      Switch(config)#hostname FINANCE-SWITCH
      FINANCE-SWITCH(config)#vlan 30
      FINANCE-SWITCH(config-vlan)#name FINANCE
      FINANCE-SWITCH(config-vlan)#int range f0/1-24
      FINANCE-SWITCH(config-if-range)#switchport mode access
      FINANCE-SWITCH(config-if-range)#switchport access vlan 30

- **Business-Switch:**

      Switch>en
      Switch#config t
      Switch(config)#hostname BUSINESS-SWITCH
      BUSINESS-SWITCH(config)#vlan 40
      BUSINESS-SWITCH(config-vlan)#name BUSINESS
      BUSINESS-SWITCH(config-vlan)#int range f0/1-24
      BUSINESS-SWITCH(config-if-range)#switchport mode access
      BUSINESS-SWITCH(config-if-range)#switchport access vlan 40

- **Engg&Cmpt-Switch:**

      Switch>en
      Switch#conf t
      Switch(config)#hostname ENGG&CMPT-SWITCH
      ENGG&CMPT-SWITCH(config)#vlan 50
      ENGG&CMPT-SWITCH(config-vlan)#name ENGG&CMPT
      ENGG&CMPT-SWITCH(config-vlan)#int range f0/1-24
      ENGG&CMPT-SWITCH(config-if-range)#switchport mode access
      ENGG&CMPT-SWITCH(config-if-range)#switchport access vlan 50

- **Art&Design-Switch:**

      Switch>en
      Switch#config t
      Switch(config)#hostname ART&DGN-SWITCH
      ART&DGN-SWITCH(config)#vlan 60
      ART&DGN-SWITCH(config-vlan)#name ART&DGN
      ART&DGN-SWITCH(config-vlan)#int range f0/1-24
      ART&DGN-SWITCH(config-if-range)#switchport mode access
      ART&DGN-SWITCH(config-if-range)#switchport access vlan 60

- **Stu-Lab-Switch:**

      Switch>en
      Switch#config t
      Switch(config)#hostname STU-LAB-SWITCH
      STU-LAB-SWITCH(config)#vlan 70
      STU-LAB-SWITCH(config-vlan)#name STU-LAB
      STU-LAB-SWITCH(config-vlan)#int range f0/1-24
      STU-LAB-SWITCH(config-if-range)#switchport mode access
      STU-LAB-SWITCH(config-if-range)#switchport access vlan 70

- **IT-Switch:**

      Switch>en
      Switch#conf t
      Switch(config)#hostname IT-SWITCH
      IT-SWITCH(config)#vlan 80
      IT-SWITCH(config-vlan)#name IT
      IT-SWITCH(config-vlan)#int range f0/1-24
      IT-SWITCH(config-if-range)#switchport mode access
      IT-SWITCH(config-if-range)#switchport access vlan 80

Configure VLANs on each L2 Switches of the Branch Campus Network -->

- **Staff-Switch:**

      Switch>en
      Switch#conf t
      Switch(config)#hostname STAFF-SWITCH
      STAFF-SWITCH(config)#vlan 90
      STAFF-SWITCH(config-vlan)#name STAFF
      STAFF-SWITCH(config-vlan)#int range f0/1-24
      STAFF-SWITCH(config-if-range)#switchport mode access
      STAFF-SWITCH(config-if-range)#switchport access vlan 90

- **Branch-Stu-Switch:**

      Switch>en
      Switch#conf t
      Switch(config)#hostname BRANCH-STU-LAB-SWITCH
      BRANCH-STU-LAB-SWITCH(config)#vlan 100
      BRANCH-STU-LAB-SWITCH(config-vlan)#name STU-LAB
      BRANCH-STU-LAB-SWITCH(config-vlan)#int range f0/1-24
      BRANCH-STU-LAB-SWITCH(config-if-range)#switchport mode access
      BRANCH-STU-LAB-SWITCH(config-if-range)#switchport access vlan 100

VLANs assign to the respective ports of L3 Switch of the Main Campus Network -->

- Enable L3 Switch of the Main Campus Network 

      Switch>en
      Switch#config t
      Switch(config)#hostname MAIN-CAMPUS-L3-SWITCH

- **Admin:**

      MAIN-CAMPUS-L3-SWITCH(config)#vlan 10
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#name ADMIN
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/2
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 10
      MAIN-CAMPUS-L3-SWITCH(config-if)#exit

- **HR:**

      MAIN-CAMPUS-L3-SWITCH(config)#vlan 20
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#name HR
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/3
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 20
      MAIN-CAMPUS-L3-SWITCH(config-if)#exit

- **Finance:**

      MAIN-CAMPUS-L3-SWITCH(config)#vlan 30
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#name FINANCE
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/4
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 30
      MAIN-CAMPUS-L3-SWITCH(config-if)#exit

- **Business:**

      MAIN-CAMPUS-L3-SWITCH(config)#vlan 40
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#name BUSINESS
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/5
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 40
      MAIN-CAMPUS-L3-SWITCH(config-if)#exit

- **Engg&Cmpt:**

      MAIN-CAMPUS-L3-SWITCH(config)#vlan 50
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#name ENGG&CMPT
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/6
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 50
      MAIN-CAMPUS-L3-SWITCH(config-if)#exit

- **Art&Dgn:**

      MAIN-CAMPUS-L3-SWITCH(config)#vlan 60
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#name ART&DGN
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/7
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 60
      MAIN-CAMPUS-L3-SWITCH(config-if)#exit

- **Stu-Lab:**

      MAIN-CAMPUS-L3-SWITCH(config)#vlan 70
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#name STU-LAB
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/8
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 70
      MAIN-CAMPUS-L3-SWITCH(config-if)#exit

- **IT:**

      MAIN-CAMPUS-L3-SWITCH(config)#vlan 80
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#name IT
      MAIN-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/9
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 80
      MAIN-CAMPUS-L3-SWITCH(config-if)#exit

VLANs assign to the respective ports of L3 Switch of the Branch Campus Network -->

- Enable L3 Switch of the Branch Campus Network

      Switch>en
      Switch#config t
      Switch(config)#hostname BRANCH-CAMPUS-L3-SWITCH

- **Staff:**

      BRANCH-CAMPUS-L3-SWITCH(config)#vlan 90
      BRANCH-CAMPUS-L3-SWITCH(config-vlan)#name STAFF
      BRANCH-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/2
      BRANCH-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      BRANCH-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 90
      BRANCH-CAMPUS-L3-SWITCH(config-if)#exit

- **Stu-Lab:**

      BRANCH-CAMPUS-L3-SWITCH(config)#vlan 100
      BRANCH-CAMPUS-L3-SWITCH(config-vlan)#name BRANCH-STU-LAB
      BRANCH-CAMPUS-L3-SWITCH(config-vlan)#int g1/0/3
      BRANCH-CAMPUS-L3-SWITCH(config-if)#switchport mode access
      BRANCH-CAMPUS-L3-SWITCH(config-if)#switchport access vlan 100
      BRANCH-CAMPUS-L3-SWITCH(config-if)#exit

### 5.2. Inter-VLAN Routing Configuration

Configuring Inter-VLAN routing on the Main Campus Router and Branch Campus Router, we must follow these things :

    1. Each VLAN must lie in a different subnet of a Network.

    2. One Port of the L3 Switches should be made a Trunk Port, that port is connected to the Main Campus Router and Branch Campus Router. Except those port that are connected to the different VLANs.

    3. We have to create the Sub-Interfaces on the Router for each VLAN and Assign the different IP addresses for each Sub-Interface.

    4. Each End Device in the different VLANs must use the same IP address as a Gateway-IP, which is already assigned to the respective Sub-Interfaces. So that every VLAN can communicate with each other by applying Inter-VLAN Routing Protocol.

#### 5.2.1. Every VLAN use Different Subnets

- Subnets of each VLANs of the Main Campus Network -->

  |VLAN|	Network Address|	Subnet Mask|
  |---|---|---|
  |10|	192.168.1.0/24|	255.255.255.0|
  |20|	192.168.2.0/24|	255.255.255.0|
  |30|	192.168.3.0/24|	255.255.255.0|
  |40|	192.168.4.0/24|	255.255.255.0|
  |50|	192.168.5.0/24|	255.255.255.0|
  |60|	192.168.6.0/24|	255.255.255.0|
  |70|	192.168.7.0/24|	255.255.255.0|
  |80|	192.168.8.0/24|	255.255.255.0|

- Subnets of each VLANs of the Branch Campus Network -->

  |VLAN|	Network Address|	Subnet Mask|
  |----|----|----|
  |90|	192.168.9.0/24|	255.255.255.0|
  |100|	192.168.10.0/24|	255.255.255.0|

#### 5.2.2. Trunk Configuration

In this project **(GigabitEthernet 0/0)** port are connected to the both Main Campus and Branch Campus Router, so this port will be Trunk Port. 

- Configure Trunk on L3 Switch of the Main Campus Network

      MAIN-CAMPUS-L3-SWITCH(config)#int g1/0/1
      MAIN-CAMPUS-L3-SWITCH(config-if)#switchport mode trunk

- Configure Trunk on L3 Switch of the Branch Campus Network

      BRANCH-CAMPUS-L3-SWITCHexit(config)#int g1/0/1
      BRANCH-CAMPUS-L3-SWITCHexit(config-if)#switchport mode trunk

#### 5.2.3. Sub-Interface Configuration

Configure Sub-Interfaces on each VLANs of the Main Campus Network -->

- **VLAN 10:**

      MAIN-CAMPUS-ROUTER(config)#int g0/0.10
      MAIN-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 10
      MAIN-CAMPUS-ROUTER(config-subif)#ip address 192.168.1.1 255.255.255.0
      MAIN-CAMPUS-ROUTER(config-subif)#exit

- **VLAN 20:**

      MAIN-CAMPUS-ROUTER(config)#int g0/0.20
      MAIN-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 20
      MAIN-CAMPUS-ROUTER(config-subif)#ip address 192.168.2.1 255.255.255.0
      MAIN-CAMPUS-ROUTER(config-subif)#exit

- **VLAN 30:**

      MAIN-CAMPUS-ROUTER(config)#int g0/0.30
      MAIN-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 30
      MAIN-CAMPUS-ROUTER(config-subif)#ip address 192.168.3.1 255.255.255.0
      MAIN-CAMPUS-ROUTER(config-subif)#exit

- **VLAN 40:**

      MAIN-CAMPUS-ROUTER(config)#int g0/0.40
      MAIN-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 40
      MAIN-CAMPUS-ROUTER(config-subif)#ip address 192.168.4.1 255.255.255.0
      MAIN-CAMPUS-ROUTER(config-subif)#exit

- **VLAN 50:**

      MAIN-CAMPUS-ROUTER(config)#int g0/0.50
      MAIN-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 50
      MAIN-CAMPUS-ROUTER(config-subif)#ip address 192.168.5.1 255.255.255.0
      MAIN-CAMPUS-ROUTER(config-subif)#exit

- **VLAN 60:**

      MAIN-CAMPUS-ROUTER(config)#int g0/0.60
      MAIN-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 60
      MAIN-CAMPUS-ROUTER(config-subif)#ip address 192.168.6.1 255.255.255.0
      MAIN-CAMPUS-ROUTER(config-subif)#exit

- **VLAN 70:**

      MAIN-CAMPUS-ROUTER(config)#int g0/0.70
      MAIN-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 70
      MAIN-CAMPUS-ROUTER(config-subif)#ip address 192.168.7.1 255.255.255.0
      MAIN-CAMPUS-ROUTER(config-subif)#exit

- **VLAN 80:**

      MAIN-CAMPUS-ROUTER(config)#int g0/0.80
      MAIN-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 80
      MAIN-CAMPUS-ROUTER(config-subif)#ip address 192.168.8.1 255.255.255.0
      MAIN-CAMPUS-ROUTER(config-subif)#exit

Configure Sub-Interfaces on each VLANs of the Branch Campus Network -->

- **VLAN 90:**

      BRANCH-CAMPUS-ROUTER(config)#int g0/0.90
      BRANCH-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 90
      BRANCH-CAMPUS-ROUTER(config-subif)#ip address 192.168.9.1 255.255.255.0
      BRANCH-CAMPUS-ROUTER(config-subif)#exit

- **VLAN 100:**

      BRANCH-CAMPUS-ROUTER(config)#int g0/0.100
      BRANCH-CAMPUS-ROUTER(config-subif)#encapsulation dot1q 100
      BRANCH-CAMPUS-ROUTER(config-subif)#ip address 192.168.10.1 255.255.255.0
      BRANCH-CAMPUS-ROUTER(config-subif)#exit

#### 5.2.4. End Device Default Gateway IP

Assign Default Gateway IP on the End Devices of the Main Campus Network -->

- **VLAN 10**

   Every End-Device in the VLAN 10 must use **192.168.1.1** as a Default Gateway-IP.

- **VLAN 20**

   Every End-Device in the VLAN 20 must use **192.168.2.1** as a Default Gateway-IP.

- **VLAN 30**

   Every End-Device in the VLAN 30 must use **192.168.3.1** as a Default Gateway-IP.

- **VLAN 40**

   Every End-Device in the VLAN 40 must use **192.168.4.1** as a Default Gateway-IP.

- **VLAN 50**

   Every End-Device in the VLAN 50 must use **192.168.5.1** as a Default Gateway-IP.

- **VLAN 60**

   Every End-Device in the VLAN 60 must use **192.168.6.1** as a Default Gateway-IP.

- **VLAN 70**

   Every End-Device in the VLAN 70 must use **192.168.7.1** as a Default Gateway-IP.

- **VLAN 80**

   Every End-Device in the VLAN 80 must use **192.168.8.1** as a Default Gateway-IP.

Assign Default Gateway IP on the End Devices of the Branch Campus Network -->

- **VLAN 90**

   Every End-Device in the VLAN 90 must use **192.168.9.1** as a Default Gateway-IP.

- **VLAN 100**

   Every End-Device in the VLAN 100 must use **192.168.10.1** as a Default Gateway-IP.

### 5.3. IP Assign for Each Router

- Assign IP Address on the Main Campus Router -->

      Router>en
      Router#conf t
      Router(config)#hostname MAIN-CAMPUS-ROUTER
      MAIN-CAMPUS-ROUTER(config-if)#int se0/2/0
      MAIN-CAMPUS-ROUTER(config-if)#ip address 10.10.10.5 255.255.255.252
      MAIN-CAMPUS-ROUTER(config-if)#no shut
      MAIN-CAMPUS-ROUTER(config-if)#int se0/2/1
      MAIN-CAMPUS-ROUTER(config-if)#clock rate 64000
      MAIN-CAMPUS-ROUTER(config-if)#ip address 10.10.10.1 255.255.255.252
      MAIN-CAMPUS-ROUTER(config-if)#no shut
      MAIN-CAMPUS-ROUTER(config)# int g0/0
      MAIN-CAMPUS-ROUTER(config-if)#no shut

- Assign IP Address on the Branch Campus Router -->

      Router>en
      Router#config t
      Router(config)#hostname BRANCH-CAMPUS-ROUTER
      BRANCH-CAMPUS-ROUTER(config)#int se0/2/0
      BRANCH-CAMPUS-ROUTER(config-if)#ip address 10.10.10.2 255.255.255.252
      BRANCH-CAMPUS-ROUTER(config-if)#no shut
      BRANCH-CAMPUS-ROUTER(config-if)#int g0/0
      BRANCH-CAMPUS-ROUTER(config-if)#no shut

- Assign IP Address on the Cloud Router of Main Campus Network -->

      Router>en
      Router#config t
      Router(config)#hostname CLOUD-ROUTER
      CLOUD-ROUTER(config)#int se0/2/0
      CLOUD-ROUTER(config-if)#clock rate 64000
      CLOUD-ROUTER(config-if)#ip address 10.10.10.6 255.255.255.252
      CLOUD-ROUTER(config-if)#no shut
      CLOUD-ROUTER(config-if)#int g0/0
      CLOUD-ROUTER(config-if)#ip address 20.0.0.1 255.255.255.252
      CLOUD-ROUTER(config-if)#no shut


### 5.4. DHCP Configuration

DHCP configure on the Main Campus and Branch Campus Router for Automatic IP assignment to every End-Devices of the each Departments of Main Campus and Branch Campus Network.

DHCP service "ON" in the Main Campus Router -->

      MAIN-CAMPUS-ROUTER(config)#service dhcp

- **Admin:**

      MAIN-CAMPUS-ROUTER(config)#ip dhcp pool ADMIN
      MAIN-CAMPUS-ROUTER(dhcp-config)#network 192.168.1.0 255.255.255.0
      MAIN-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.1.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.1.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#exit

- **HR:**

      MAIN-CAMPUS-ROUTER(config)#ip dhcp pool HR
      MAIN-CAMPUS-ROUTER(dhcp-config)#network 192.168.2.0 255.255.255.0
      MAIN-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.2.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.2.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#exit

- **Finance:**

      MAIN-CAMPUS-ROUTER(config)#ip dhcp pool FINANCE
      MAIN-CAMPUS-ROUTER(dhcp-config)#network 192.168.3.0 255.255.255.0
      MAIN-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.3.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.3.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#exit

- **Business:**

      MAIN-CAMPUS-ROUTER(config)#ip dhcp pool BUSINESS
      MAIN-CAMPUS-ROUTER(dhcp-config)#network 192.168.4.0 255.255.255.0
      MAIN-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.4.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.4.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#exit

- **Engg&Cmpt:**

      MAIN-CAMPUS-ROUTER(config)#ip dhcp pool ENGG&CMPT
      MAIN-CAMPUS-ROUTER(dhcp-config)#network 192.168.5.0 255.255.255.0
      MAIN-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.5.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.5.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#exit

- **Art&Dgn:**

      MAIN-CAMPUS-ROUTER(config)#ip dhcp pool ART&DGN
      MAIN-CAMPUS-ROUTER(dhcp-config)#network 192.168.6.0 255.255.255.0
      MAIN-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.6.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.6.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#exit

- **Stu-Lab:**

      MAIN-CAMPUS-ROUTER(config)#ip dhcp pool STU-LAB
      MAIN-CAMPUS-ROUTER(dhcp-config)#network 192.168.7.0 255.255.255.0
      MAIN-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.7.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.7.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#exit

- **IT:**

      MAIN-CAMPUS-ROUTER(config)#ip dhcp pool IT
      MAIN-CAMPUS-ROUTER(dhcp-config)#network 192.168.8.0 255.255.255.0
      MAIN-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.8.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.8.1
      MAIN-CAMPUS-ROUTER(dhcp-config)#exit


DHCP service "ON" in the Branch Campus Router -->

      BRANCH-CAMPUS-ROUTER(config)#service dhcp

- **Staff:**

      BRANCH-CAMPUS-ROUTER(config)#ip dhcp pool STAFF
      BRANCH-CAMPUS-ROUTER(dhcp-config)#network 192.168.9.0 255.255.255.0
      BRANCH-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.9.1
      BRANCH-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.9.1
      BRANCH-CAMPUS-ROUTER(dhcp-config)#exit

- **Branch-Stu-Lab:**

      BRANCH-CAMPUS-ROUTER(config)#ip dhcp pool BRANCH-STU-LAB
      BRANCH-CAMPUS-ROUTER(dhcp-config)#network 192.168.10.0 255.255.255.0
      BRANCH-CAMPUS-ROUTER(dhcp-config)#default-router 192.168.10.1
      BRANCH-CAMPUS-ROUTER(dhcp-config)#dns-server 192.168.10.1
      BRANCH-CAMPUS-ROUTER(dhcp-config)#exit

### 5.5. Routing Protocol Configuration

RIP configure to connect different IP networks and enable communication between campuses.

- RIP configure on the Main Campus Router of Main Campus Network

      MAIN-CAMPUS-ROUTER(config)#router rip
      MAIN-CAMPUS-ROUTER(config-router)#version 2
      MAIN-CAMPUS-ROUTER(config-router)#network 10.10.10.0
      MAIN-CAMPUS-ROUTER(config-router)#network 10.10.10.4
      MAIN-CAMPUS-ROUTER(config-router)#network 192.168.1.0
      MAIN-CAMPUS-ROUTER(config-router)#network 192.168.2.0
      MAIN-CAMPUS-ROUTER(config-router)#network 192.168.3.0
      MAIN-CAMPUS-ROUTER(config-router)#network 192.168.4.0
      MAIN-CAMPUS-ROUTER(config-router)#network 192.168.5.0
      MAIN-CAMPUS-ROUTER(config-router)#network 192.168.6.0
      MAIN-CAMPUS-ROUTER(config-router)#network 192.168.7.0
      MAIN-CAMPUS-ROUTER(config-router)#network 192.168.8.0
      MAIN-CAMPUS-ROUTER(config-router)#no auto-summary

- RIP configure on the Brach Campus Router of Branch Campus Network

      BRANCH-CAMPUS-ROUTER(config)#router rip
      BRANCH-CAMPUS-ROUTER(config-router)#version 2
      BRANCH-CAMPUS-ROUTER(config-router)#network 10.10.10.0
      BRANCH-CAMPUS-ROUTER(config-router)#network 192.168.9.0
      BRANCH-CAMPUS-ROUTER(config-router)#network 192.168.10.0
      BRANCH-CAMPUS-ROUTER(config-router)#no auto-summary

- RIP configure on the Cloud Router of Main Campus Network

      CLOUD-ROUTER(config)#router rip
      CLOUD-ROUTER(config-router)#version 2
      CLOUD-ROUTER(config-router)#network 20.0.0.0
      CLOUD-ROUTER(config-router)#network 10.10.10.4
      CLOUD-ROUTER(config-router)#no auto-summary

## 6. Verification

### 6.1. VLAN Verification

- Verify VLANs on the Main Campus L2 and L3 Switch of Main Campus Network -->

      MAIN-CAMPUS-L2-SWITCH# show vlan brief
      MAIN-CAMPUS-L3-SWITCH# show vlan brief

- Verify VLANs on the Branch Campus L2 and L3 Switch of Branch Campus Network -->

      BRANCH-CAMPUS-L2-SWITCH# show vlan brief
      BRANCH-CAMPUS-L3-SWITCH# show vlan brief

### 6.2. DHCP Verification

- Verify DHCP on the Main Campus Router of Main Campus Network -->

      MAIN-CAMPUS-ROUTER# show ip dhcp binding

- Verify DHCP on the Branch Campus Router of Branch Campus Network -->

      BRANCH-CAMPUS-ROUTER# show ip dhcp binding

### 6.3. Inter-VLAN Verification

- Verify Inter-VLAN on the Main Campus Network

  - Ping from **Admin-PC** to **HR-PC**

        Cisco Packet Tracer PC Command Line 1.0
        C:\>ping 192.168.2.2

        Pinging 192.168.2.2 with 32 bytes of data:


        Reply from 192.168.2.2: bytes=32 time<1ms TTL=127
        Reply from 192.168.2.2: bytes=32 time<1ms TTL=127
        Reply from 192.168.2.2: bytes=32 time<1ms TTL=127
        
        Ping statistics for 192.168.2.2:
            Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
        Approximate round trip times in milli-seconds:
            Minimum = 0ms, Maximum = 0ms, Average = 0ms

- Verify Inter-VLAN on the Branch Campus Network

  - Ping from **Staff-PC** to **Stu-Lab-PC**

        Cisco Packet Tracer PC Command Line 1.0
        C:\>ping 192.168.10.2
        
        Pinging 192.168.10.2 with 32 bytes of data:
        
        Reply from 192.168.10.2: bytes=32 time<1ms TTL=127
        Reply from 192.168.10.2: bytes=32 time<1ms TTL=127
        Reply from 192.168.10.2: bytes=32 time<1ms TTL=127
        
        Ping statistics for 192.168.10.2:
            Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
        Approximate round trip times in milli-seconds:
            Minimum = 0ms, Maximum = 0ms, Average = 0ms

### 6.4. Routing Protocol Verification

- Verify RIP on the Main Campus Router of Main Campus Network

      MAIN-CAMPUS-ROUTER# show ip route rip

- Verify RIP on the Branch Campus Router of Branch Campus Network

      BRANCH-CAMPUS-ROUTER# show ip route rip

- Verify RIP on the Cloud Router of Main Campus Network

      CLOUD-ROUTER# show ip route rip 

### 6.5. End-to-End Connectivity Test

- Ping from **Admin-PC** of Main Campus Network to **Staff-PC** of Branch Campus Network

      Cisco Packet Tracer PC Command Line 1.0
      C:\>ping 192.168.9.2

      Pinging 192.168.9.2 with 32 bytes of data:
      
      Reply from 192.168.9.2: bytes=32 time=27ms TTL=126
      Reply from 192.168.9.2: bytes=32 time=2ms TTL=126
      Reply from 192.168.9.2: bytes=32 time=2ms TTL=126
      
      Ping statistics for 192.168.9.2:
          Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
      Approximate round trip times in milli-seconds:
          Minimum = 2ms, Maximum = 27ms, Average = 10ms

- Ping from **Branch-Stu-PC** of Branch Campus Network to **HR-PC** of Main Campus Network

      Cisco Packet Tracer PC Command Line 1.0
      C:\>ping 192.168.2.2
      
      Pinging 192.168.2.2 with 32 bytes of data:
      
      Reply from 192.168.2.2: bytes=32 time=17ms TTL=126
      Reply from 192.168.2.2: bytes=32 time=2ms TTL=126
      Reply from 192.168.2.2: bytes=32 time=2ms TTL=126
      Reply from 192.168.2.2: bytes=32 time=3ms TTL=126
      
      Ping statistics for 192.168.2.2:
          Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
      Approximate round trip times in milli-seconds:
          Minimum = 2ms, Maximum = 17ms, Average = 6ms

- Ping from **IT-PC** of Main Campus Network to **Email-Server** of Main Campus Network

      Cisco Packet Tracer PC Command Line 1.0
      C:\>ping 20.0.0.2
      
      Pinging 20.0.0.2 with 32 bytes of data:
      
      Reply from 20.0.0.2: bytes=32 time=1ms TTL=126
      Reply from 20.0.0.2: bytes=32 time=1ms TTL=126
      Reply from 20.0.0.2: bytes=32 time=1ms TTL=126
      
      Ping statistics for 20.0.0.2:
          Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
      Approximate round trip times in milli-seconds:
          Minimum = 1ms, Maximum = 1ms, Average = 1ms

## 7. Conclusion

This network design efficiently connects Albion University's campuses while ensuring security, scalability, and proper segmentation. VLANs provide isolation and better network management, while RIPv2 ensures efficient routing.

## 8. Author

Prepared by: Surajit Sen

## 9. Licence

This document is open for modification and distribution under the MIT License.

## 10. Contributing

Contributions to enhance network security, redundancy, and performance optimizations are welcome.
