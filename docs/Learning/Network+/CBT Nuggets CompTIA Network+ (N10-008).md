# CBT Nuggets CompTIA Network+ (N10-008)

## Network Models

### Open Systems Interconnection (OSI) Model

| Layer Number | Layer Name |
| --- | --- |
| 7 | Application |
| 6 | Presentation |
| 5 | Session | 
| 4 | Transport | 
| 3 | Network | 
| 2 | Data Link | 
|1 | Physical | 

*Please Do Not Throw Sausage Pizza Away*
*All People Seem To Need Data Processing*

The OSI reference model is a model. The protocol the infrastructure is built on it TCP/IP. 

In the TCP/IP implementation Layers 5-7 are typically grouped together and referenced just as the application layer. 

The TCP/IP protocol stacks gets its name from the technologies that work together used in Layer 4 (TCP)  and Layer 3 (IP). 

[Wireshark](https://www.wireshark.org/) is a protocol analyzer that shows each layer of network traffic. 
#### Application Layer

The Application Layer is the initial request for a service. 

Service requests can include web browsing, streaming, printing, and DNS. 

DNS (Domain Name System)
: Performs name-to-address translation (e.g. gets IP address of google.com)

#### Transport Layer

The Transport Layer wraps the Application request in a protocol header. 

Protocols: 
- TCP (Transmission Control Protocol)
	- TCP is a protocol that cares; meaning it includes a series of receipts and verification to ensure data is transferred successfully. 
- UDP (User Datagram Protocol)
	- UDP is a protocol that doesn't care; i.e. doesn't verify request processes successfully

The user doesn't get to choose the protocol used. 

The protocol selected is based on which service makes the request. 

Example: The DNS service uses the UDP protocol. 

segment: a chunk of data

TCP Receipts/Verification completes a 3-Way Handshake
1. `[SYN]` request asking is server is available
2. `[SYN, ACK]` acknowledgement from the server
3. `[ACK]` me find acknowledgement from client back to the server

Port numbers in the TCP/UDP headers indicate the type of service requested: 
- DNS used UDP Port #53
- HTTP (Web Browsing) uses TCP Port #80
- HTTPS/SSL/TLS (secure web browsing) uses TCP Port #443

#### Network Layer

The Network Layer adds the IP Address information of both the source and destination. 

#### Data Link Layer

The Data Link layer adds MAC Address information. 

Every network device has a unique identifier burned onto it's network card called a MAC Address. 

The Address Resolution Protocol (ARP) can be used to discovered the MAC Address of the next device in the traffic chain. 

Routers forward based on IP Address and data in packets. 
Switches forward based on MAC Addresses and data in frames. 

A gateway is a network node that serves as an access point to another network. 

A default gateway is the network node that serves as the forwarding host to other networks when no other route specification matches the destination IP address of a packet. 

The default gateway is typically the local router. 

#### Physical Layer

The Physical Layer is the physical Network Interface Card (NIC) and cables sending the information. 

### Encapsulation / Decapsulation

Encapsulation Example: Making a DNS Request
- The computer needs to know the IP Address of a Website (e.g. cbtnuggets.com)
- **Application**: The Application Layer Service of DNS is being used. 
- **Transport**: The Application Layer Services is encapsulated with a UDP Header that includes the paths involved. 
- **Network**: This is encapsulated by an IP Header that includes the source and destination IP Addresses. Routers use these IPs to make forwarding decisions. 
- **Data Link**: This is encapsulated by a Layer 2 (Data Link) Header that includes the source and destination MAC Addresses on the local network. The destination MAC address is typically the default gateway in most cases. 
- **Physical**: This data is then sent onto the network through the Network Interface Card (NIC). 

---

## Network Topologies and Types

### Underlay vs. Overlay

Underlay Network: the physical network equipment and devices responsible for packet delivery

Overlay Network: the logical network layout / virtualization of the network

Physical connections such as copper, fiber, Coax (Cable), DSL (Phone Lines), Leased Lines, Demarcation Points, Smart Jacks, and Optical Connectors are all part of the Underlay Network. 

Wireless connection, such as Cellular Data (5G) and Satellite technologies are also part of the Underlay Network. 

Demarcation Point (Demarc)
: the point at which the clients equipment connects to the service providers equipment

Protocols that determine how network traffic is sent, such as GRE and IPSec, are part of the Overlay Network. 

Generic Routing Encapsulation (GRE)
: tunneling protocol that encapsulates a variety of network layer protocols

IPSec
: a set of communication protocols for setting up secure network connections (each packet is encrypted before being sent)

### Network Topologies

A topology describes how parts are arranged. A network topology describes how a network is arranged. 

#### Local Area Network (LAN) Topologies

##### Bus Topology

![[busTopology.png]]

In the early days of network, building would have a long coaxial cable ran across the building that's terminated at both ends. 

Along the cable would be Ethernet taps for each computer

Defined as a 10Base2 network: 
- 10 - Stands for 10 Mbps
- Base - Stands for Base Bond; meaning only 1 signal/frequency at a time is present on the shared network segment
- 2- The maximum length of the network (in hundreds of meters; i.e 2 in this case)

1 Collision Domain - Only 1 devices can talk on the network at a time

1 Broadcast Domain - All devices on the network see a broadcast transmission

A major con of the Bus Topology is a single fault in the cabling takes the entire network down. 

##### Star Topology

The Star Topology is also known as Hub and Spoke. 

Network devices are connected to a central Hub or Switch. 

###### Hub

![[hub.png]]

Hub
: a network node that broadcasts data to every devices connected to it

Any signal sent to a port on a hub is then repeated and sent out to all the other ports on that hub. 

This topology logically acts like the Bus topology, but is laid out like a Star. 

1 Collision Domain

1 Broadcast Domain

Uses Unshielded Twisted Pair (UTP) cabling instead of coax. 

A 10BaseT network
- The 10 and Base portions hold the same meaning as the Bus Topology. 
- T - stands for Twisted Pair (i.e. the cabling being used)

###### Switch

![[layer2Switch.png]]

Switches are also laid out in a physical star topology. 

Because switches are aware of the L2 address of each device connected to it, hosts can communicate directly to specific hosts. Every port is its own collision domain (e.g. a 4-port switch has 4 collision domains)

Number of collision domains is equal to the number of ports on the switch. 

1 Broadcast Domain

Switches have a physical Star topology, but logically acts like a Bus (albeit with the benefit of each port having its own collision domain). 

##### Ring Topology

![[ringTopology.png]]

Each network device is connected to each other in a ring. 

Example: A -> B -> C -> D; If A needs to send data to C, then data goes to B first, which passes it to C. 

###### Token Ring

![[tokenRing.png]]

Devices are connected to a hub (physically a Star Topology), but data is passed between devices like a Ring Topology. 

#### Wide Area Network (WAN) Topologies

![[wanTopology.png]]

Clients aren't able to change the network infrastructure between sites. This is handled by the ISPs. In diagrams network between our client defined sites is referred to as the Cloud. 

##### Hub and Spoke Topology

![[wanTopology.png]]

In a Hub and Spoke WAN Topology, a central site acts as a headquarters. All other site communication is routed through the HQ. 

##### Full Mesh Topology

![[fullMesh.png]]

In a Full Mesh Topology every site has a connection to every other site. 

This topology isn't practical when there's a large number of sites. 

##### Hybrid Topology

![[hybrid.png]]

Hybrid Topologies use a combination of Hub and Spoke and Full Mesh Topologies. 

### Network Types

#### Peer-to-Peer

![[peerToPeer.png]]

Devices sharing data between each other, with neither device having a dedicated role (client/server) assigned. 

#### Client-to-Server

![[clientToServer.png]]

Clients (devices that consume data) receiving data from servers (devices that host the data). 

#### Personal Area Network (PAN)

![[PAN.png]]

Devices in close proximity sharing data directly to each other. 

Examples: Bluetooth, ifrared, NFC (Near Field Communication)

#### Corporate Networks

![[corporateNetwork(3TierAccess).png]]

Corporations typically implement 3-tier access. 

For wireless communication (WiFi), the Access and Distribution Layers will have connections to Wireless Access Points (WAPs). 

In large environments, multiple WAPs are networked together to form a WLAN (Wireless Local Area Network). 

SSID (Service Set Identifier)
: the name of a wireless network

#### Campus Area Network (CAN)
: a network that spans a limited geographic area (e.g. College Campus)

#### Metropolitan Area network (MAN)
: a network that spans a region the size of a metropolitan area

#### Wide Area Network (WAN)
: a telecommunications network that extends over a large geographic area.

CAN < MAN < WAN

#### Software Defined Wide Area Network (SDWAN)

How the infrastructure should look is defined using computer software and this gets pushed out to a controller to be implemented. 

#### Multipoint Generic Routing Encapsulation (mGRE)

Multipoint Generic Routing Encapsulation (GRE) is a dynamic tunnel interface. It can dynamically accept incoming requests, verify the source, and erect tunnels

An initial headquarters site can be setup using mGRE. Then as other sites are brought on, they get pointed to the HG, and mGRE builds the tunnel dynamically. 

mGRE prevents having to manually reconfigure the HQ each time a new site is brought on. 

mGRE is cheaper than SDWAN

#### Multi Protocol Label Switches (MPLS)

![[MPLS.png]]

At the service provider level, MPLS is used to forward packets based on labels, instead of IP Addresses. 

Each packet receives a "Layer 2.5" label in addition to its normal Layer 3 IP header. 

Label Switching - routers forwarding traffic based on labels instead of IP Addresses. 

Label Swapping - the routers swap the labels/tags, after being received, for the next label in the path

### Virtualized Networks

hypervisor
: software that creates and runs Virtual Machines (VMs); also known as a Virtual Machine Monitor (VMM)

A Tier-1 Hypervisor, also known as a bare-metal hypervisor, runs directly on the network. 

A Tier-2 Hypervisor is an application (such as VMware) that runs the virtual machines. 

In a VMware environment hypervisors are named ESXi. 

#### Virtual Networking

![[virtualNetworking.png]]

Physical network connects the hypervisors. Virtual networking connects the VMs. 

Servers, Routers, and Firewalls can all be virtualized.  Physical equipment is still typically used, because ports are needed for physical computers and each device virtualized takes power/resources. 

### Networks for Storage

Local Storage - disk drives attached to physical hardware (direct attached)

Fibre Channel - dedicated network host that devices can access storage from

Fibre Channel over Ethernet (FCoE) - Fibre Channel running over an Ethernet network

Storage Area Network (SAN) - block-based storage that systems can share efficiently

block-based - individual blocks/chunks of data that can be read/written to

iSCSI - technology used to communicate with SANs

iSCSI uses the same commands as local storage, but can be used over an IP-based network

Network Attached Storage (NAS) - file-based (instead of block-based) storage. In file-based storage individual files are read from / written to, instead of blocks of data

---

## Network Cables and Connectors

### Intro to Cables and Connectors

Cables and Connectors are part of the physical layer of the OSI model. 

Copper Cabling sends data using electric signals. 

Fiber Cabling sends data using Light. 


### Copper Cables

Type 1 Token Ring cables were shielded. Shielded cables are wrapped in a tin foil like covering and plastic sheathing. 

Ethernet Cabling initially used Coax cables with RG-59 connectors. This cabling was used in 10base2 Bus Topologies. Any break in the cable took the entire network down. Cables were connected using t-connectors. 

When hubs came into production Unshielded Twisted Pair (UTP) cabling came into use. 

Layer 2 Switches also uses UTP cabling

Categories of UTP Cables

| Category | Speed Supported | Cable Type | 
| --- | --- |
| Cat5 | 100 Mbps | Unshielded Twisted Pair (UTP) |
| Cat5e | 1000 Mbps (1 Gbps) | Unshielded Twisted Pair (UTP) |
| Cat6 | 10 Gbps | Unshielded Twisted Pair (UTP) |
| Cat6a | 10Gbps | Unshielded Twisted Pair (UTP) | 
| Cat7 | 10 Gbps | Shielded |
| Cat8 | 40 Gbps | Shielded |

Maximum length for a cable run is 100 meters. 

In order to cover distances longer than 100 meters either: 1) Insert a Layer 2 Switch to break up the run or 2) Use Fiber cabling. 

### Fiber Cables

Fiber cables can be ran distances greater than 100 meters. 

Electro-Magnetic Interference (EMI)
: unwanted noise or interference in an electrical path or circuit caused by an outside source

Unlike Copper Cabling, which uses electric signals to send data, fiber uses light frequencies to send data. Light frequencies aren't electric, therefore electromagnetic frequencies don't effect fiber cabling. This makes fiber the better choice in environments with electromagnetic frequencies (e.g. areas near generators or fluorescent lights). 

### Connector Types

Unshielded Twisted Pair (UTP) cabling typically use RJ-45 connectors. 

This connectors has 8-pins (1 pin for each wire in UTP). 

The wires are twisted together in 4 pairs (orange/orange-white, blue/blue-white, green/green-white, and brown/brown-white). 

Each pair of wires has a specific number of twists per foot to prevent cross-talk from occurring and to prevent having to foil-wrap/shield the cables

Ethernet Cabling Pinouts: T568A and T568B

![[ethernetCablingPinouts.png]]

Straight-Through Cable - Pin-outs / wires are the same at both ends. Straight-Through Cables are used to connect different devices (e.g. A PC to a Switch)

Cross-Over Cable - The pins at one end are reversed. Cross-Over Cables are used to connect like devices (e.g. PC to PC, or Switch to Switch).

Most networking devices today use a technology called MDI-X that can automatically detect what cable type (Straight-Through or Cross-Over) is connected and pass traffic regardless of what's detected.   

Fiber Cabling Connectors
FC, LC, SC, and ST
mnemonics - FC | Fiber, LC | Little Connector, SC | Stick and Click, ST | Stick and Twist

### Transceivers and Media Converters

media converter
: a networking device that converts Ethernet or other communication protocols from one cable type to another

Gigabit Interface Converter (GBIC)
:a transceiver standard, hot swappable electrical interface that supports a wide range of physical media, from copper to single-mode fiber. 

Small Form-factor Pluggable (SFP)
: a compact, hot-swappable modular slot for a media-specific transceiver, such as copper or fiber-optic. Smaller version of a GBIC. Speed: 1 Gbps

SFP+
: an SFP specification that supports speeds up to 10 Gbps

Quad Small Form-factor Pluggable (QSFP)
: a four-lane SFP. The additional lanes allow for speeds 4 times their corresponding SFP (i.e. 4 Gbps)

QSFP+
: a QSFP specification that supports speeds up to 40 Gbps

### Cable Management

Intermediate Distribution Frame (IDF)
: a free-standing, or wall-mounted, rack for managing and interconnecting a telecommunications cable between end-user devices and the main distribution frame (MDF).

Main Distribution Frame (MDF / Main Frame)
: a signal distribution frame for connecting user equipment to the service provider's equipment

Plenum Space
: the space between the structural ceiling and the drop-ceiling, or the space under a raised floor. These spaces can facilitate air circulation for HVAC.  

Any cabling ran through a building's plenum space must be plenum-rated cable. 

Typical cabling route from a PC to the Service Providers equipment is: PC -> Wall Jack -> Patch Panel -> Switch -> Router

Telephone Connectors
66 Block (16 Mhz)
110 Block (100 Mhz)

Instead of blocks, Patch Panels are now used for terminating Ethernet Cables. 

Cables are punched down into the patch panel slots using a punch-down tool. 

Building Industry Cross Connect (BIX)
: part of a telephony cross-connect system that consists of various sizes of punch-down blocks, cable distribution accessories, and a punch-down tool to terminate wires at the punch-down block

### Ethernet Standards

Copper typically uses UTP cabling with the following connectors: 
RJ-45, RJ-11 (DSL / Phone Lines), RG6 (Coax Cable / DOCSIS | has 1 major conductor), TWINAX (has 2 major conductors, requires appropriate SFP)

Copper Connections

| Name | Cable Type | Speed | Colloquial Name |
| --- | --- | --- | --- |
| 10base2 | Coax | 10 Mbps | - |
| 10baseT | UTP | 10 Mbps | Ethernet |
| 100baseTX | UTP | 100 Mbps | Fast Ethernet |
| 1000baseTX | UTP | 1 Gbps | Gb Ethernet |
| 10GbaseT | UTP | 10 Gbps | - |
| 40GbaseT | Shielded | 40 Gbps | - |

Each connection has 100 meter max run. 

Fiber Connectors: FX, SX, LX, SR, LR

Fiber Connections
100Base<connector>, 1000Base<connector>, 10GBase<connector>, up to 50G, 100G, and 200G
Example: 100BaseFX

Bi-Direction Wavelength Division Multiplexing (BWDM)

Instead of having separate fiber cables for sending/receiving, fiber can transmit light at different wavelength. Therefore a separate wavelength can be used for sending and another for receiving, allowing both signals to transmit on a single cable. 

Coarse Wavelength Division Multiplexing (CWDM) is a way to accomplish this. 

Dense Wavelength Division Multiplexing (DWDM) uses different tech then CWDM to accomplish this at higher speeds. 

---

## IPv4 Fundamentals

### Introduction to IPv4 Fundamentals

### IPv4 Overview

Anything connected to a network is a host

Hosts connect to a network using its network interface card (NIC). 

All host addresses on the same network must be unique (hosts on different networks can have the same address). 

Analogy: hosts are similar to house addresses; networks are similar to street addresses

Routers pass traffic between networks. 

### Dotted Decimal IPv4

An IPv4 address is 4 numbers separated by 3 dots. 

Each number represents 8 bits of data. So, altogether an IPv4 address represents 32 bits. 

A bit is an on/off value, represented as a 1 or 0. 

IPv4 Example Address: 192.168.1.1

An IP Address represents both the network and the host address. 

A Subnet Mask denotes which part of the IP Address represents the network and which part represents the host. 

Example: 
IP Address: 192.168.1.151
Subnet Mask: 255.255.255.0
This Subnet Mask tells us the network address is 192.168.1 and the host address is 151. 

If a host needs to forward a message to a different network, it'll send the traffic to the specified Default Gateway. The Default Gateway is is typically the IP Address of the router connected to the service provider (ISP). 

IP Address Classes

| Address Class | Default Mask | First Octet of IP | CIDR Notation |
| --- | --- | --- | --- |
| A | 255.0.0.0 | 1-127 | /8 |
| B | 255.255.0.0 | 128-191 | /16 |
| C | 255.255.255.0 | 192-223 | /24 |

Classless Inter-Domain Routing (CIDR) Notation

Instead of writing/saying a Subnet Mask as 255.255.255.0, CIDR notation is a shorthand way of indicating the Subnet Mask. It adds the number of bits in use and is written in a slash notation. 

Example: 255.255.255.0 is using 24-bits, but the last 8 bits are off. In CIDR notation this is written as /24. 

### Assigning IP Addresses

Domain Name System (DNS): DNS gets the IP Address of a given URL / Domain Name

Each device on a network needs an IP Address, Subnet Mask, Default Gateway Address, and DNS information. 

Instead of manually entering this information, DHCP can be implemented to automatically assign this info. 

Dynamic Host Configuration Protocol (DHCP): protocol used to hand-out network information (including the IP Address, Subnet Mask, Default Gateway, and DNS information).

For devices where it's important for an IP address needs to stay the same the network information can manually be set on the device, this is called a Static IP. 

DHCP Reservation - For devices that needs to maintain the same IP Address; instead of manually setting a Static IP, a DHCP reservation can be set. A DHCP reservation will grant all network requests from the designation MAC address the same IP. 

Automatic Private IP Addressing (APIPA) - The Windows function that provides DHCP autoconfiguration addressing.

If a client makes a request to a DHCP Server, but there's not a DHCP Server setup on the network, then after the client request times out an APIPA Address would get assigned. 

If the IP of a device starts with 169, it's using an APIPA Address

A device with an APIPA address can only talk with other devices with assigned APIPA addresses. No traffic is able to be routed outside the network. 

### Unicast, Multicast, and More

Unicast: Sending an IP Packet sent to a single destination

Multicast: Sending  an IP Packet sent to a group of computers designated with a multicast group address. 

Multicast group addresses are Class D addresses that begin with an IP of 224. 

Broadcast: Sending an IP packet to every device on a network

Broadcast addresses end in .255 (e.g. 10.1.10.255) or are all 255s (255.255.255.255)

Routers won’t route/forward broadcast addresses. 

Anycast: Sending an IP packet to a single IP, but the IP being sent to is the IP of multiple hosts. 

Example: The IP of Google's DNS Servers is 8.8.8.8. When a device makes a request to Google's DNS it doesn't care which server responds. The first server, with that IP, to receive the request will send the response. 

Anycast is like Unicast, but more than 1 destination is using the destination IP. 

### Private IPv4 Addresses 

There are a limited number of publicly routable IP addresses. 

The RFC (Request for Comment) 1918 standard specifies a set of IP ranges set aside for internal network use. 

RFC 1918 Reserved Addresses

| Class | IP Range |
| --- | --- |
| A | 10.X.X.X |
| B | 172.16-31.X.X | 
| C | 192.168.X.X |

---

## NAT and PAT

### Address Translation Overview

Service providers won't forward traffic to RFC 1918 addresses. 

Any traffic sourced/destined from/to private address space is dropped by service providers. 

#### Network Address Translation (NAT)

Network Address Translation (NAT) swaps a client IP for a publicly routable address on the internet. 

Routers, Proxies, or Firewall can all be configured as the NAT device (device that performs the Network Address Translation). 

NAT can be used: 
- to route private addresses to the Internet
- to Hide (NAT obfuscates a source device's real IP)
- as a Fix (for internal networks sharing the same address space)

Example of NAT being used as a fix: 
![[Bi-directional NAT.png]]
- 2 Large companies merged. However, both companies were using the same internal network address space. 
- Traffic from 1 network meant for the other wouldn't forward, because it would treat the traffic as local traffic. 
- A temporary fix  was applied using NAT to make Client A appear as 10.6.4.0 to Client B and to make Client B appear as 10.7.4.0 to Client A. 
- This is an example of Bi-directional NAT

NAT is a 1-to-1 (1:1) mapping. A single IP is translated to a single IP. 

#### Port Address Translation (PAT)

Port Address Translation is a many-to-1 (many:1) mapping. 

These mappings can be set statically or dynamically. 

All blocks of IPv4 Address have already been allocated by service providers. Requests from/to multiple internal clients can still be processed using PAT. 

A service provider may grant a company a single publicly routable address. Each client that makes requests to the internet using the same public address, but the layer part of each session is changed. 

overloading: routing multiple clients through a single routable address

Some companies reference NAT, when they mean both NAT and PAT. 

#### Source versus Destination NAT/PAT

Source vs. Destination NAT/PAT is designated based on the initial flow of traffic that triggers NAT. i.e. What is being swapped when the initial packet is received?

Example: If a client (10.1.10.100) sends a request to Google DNS (8.8.8.8) NAT changes the client's IP (10.1.10.100) to a publicly routable address (23.1.2.0). This is an example of source NAT. When the response from Google DNS is receive and NAT performs the un-translation to get the response back to the client, this is still source NAT, because the initial request came from the client. 

Destination NAT only occurs when the original NAT request starts with an external address. 

### Source NAT

Good practice for security is to place servers that are reachable from the public internet into their own zone on the network. This is typically called the DMZ (demilitarized zone). 

Typically core devices (servers) should have statically assigned IP Addresses. 

NAT is a 1:1 mapping. Each Internal IP Address is mapped to a single External IP Address. 

NAT can be set statically or dynamically. 

If the initial translation swaps the source address, then that's source NAT. 

When the initial request is internal to external (outside the network), the un-translation of the reply is still source NAT, because the **initial flow** was internal to external translation. 

### Source PAT

TCP and UDP aren't the only protocols used by Ports. 

Ping commands are routed using the ICMP protocol. 

Most devices that implement PAT have the ability to track and uniquely identify sessions (and the session translations) even if they're using other protocols besides TCP/UDP. 

PAT applies to Layer 4 protocols other than just TCP/UDP. 

overloading: routing multiple clients through a single routable address. This is made possible using PAT. 

### Destination NAT

Destination NAT maps a publicly routable address to an internal address. 

The initial flow of traffic is external. 

If multiple servers need routed to a single public IP destination, then PAT can be used

### Destination PAT

If multiple servers are setup on a network with a single public IP, PAT can be used to route the traffic to the correct destination based on port. 

Example: 

| Server Type | Traffic Type |  DMS Address | Public Address | Port |
| --- | --- | --- | --- | --- |
| Web Server | HTTP | 172.16.1.100 | 23.1.2.125 | TCP 80 |
| Mail Server | SMTP | 172.16.1.101 | 23.1.2.125 | TCP 25 |

---

## IPv4 Subnetting

### IPv4 Subnetting Overview

Subnetting: taking a large network of IPs and segmenting them into smaller logical subnets. 

Summarize: refers to all subnetworks together (i.e. the major network). 

### IPv4 Address Anatomy

Dotted Decimal: the representation of an IPv4 address as four decimal number separated by three dots/periods. 

An IPv4 address is 32-bits long. 

Each decimal number in dotted decimal notation is 8-bits.

8 bits = 1 byte = 1 octet

4 bits = 1 nibble

A portion on the left of an IPv4 address represents the network and a portion on the right represents the host address. 

This divide is determined by the subnet mask. 

### Conversion Between Decimal and Binary

Binary is Base 2. | Decimal is Base 10

This means decimal can use the digits 0-9. Values greater than 9 carry the 1 (e.g. 10). 

Counting in Decimal: 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11

Each time the 1 is carried the place is 10 times the previous place (i.e. the ones place, tens place, hundreds place, thousands place)

Binary only uses the digits 0-1. Values great than 1 carry the 1 (e.g. 10). 

Counting in Binary: 0, 1, 10, 11, 100, 101, 110, 111, 1000

Each time the 1 is carried the place is double the previous (i.e. 1, 2, 4, 8, 16, 32, 128)

#### Binary to Decimal Conversion

Example: Convert 10110011 from Binary to Decimal 

| | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| 1 | 0 | 1 | 1 | 0 | 0 | 1 | 1 |

For each place where the bit is on (i.e. not 0), add the values. 

128 + 32 + 16 + 2 + 1 = 179

10110011 in Binary is 179 in Decimal. 

#### Decimal to Binary Conversion

Example: Convert 177 from Decimal to Binary

Find the largest Binary place the number is divisible by, then subtract that number. 

177 - 128 = 49, 49 - 32 = 17, 17-16 = 1, 1 - 1 = 0

| | | | | | | | |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| 1 | 0 | 1 | 1 | 0 | 0 | 0 | 1 |

177 in Decimal is 10110001 in Binary. 

### Longer Masks and New Subnets

The process of subnetting a network (custom subnetting) simply involves increasing the length of the subnet mask. 

Using a larger portion of the IPv4 address for the network address leaves less space for the host address portion. 

The same mask values (e.g. /8, /16, /24, etc.) don't have to be used everywhere on the network. Using different mask values is referred to as Variable Length Subnet Masks (VLSM). 

#### Example of Subnetting a Network

A client is using a RFC 1918 address space of 10.0.0.0/8

They subdivide the address space to create subnets for each site. 

| Site | Subnet |
|--- | --- |
| Headquarters (Site 1) | 10.1.0.0/16 |
| Site 2 | 10.2.0.0/16 |
| Site 3 | 10.3.0.0/16 |

Headquarters (Site 1) is then subdivided further into separate subnets for each department. 

| Department | Subnet |
|--- | --- |
| Department 1 | 10.1.10.0/24 |
| Department 2 | 10.1.20.0/24 |

### The Finger/Bit Quantity Game

To determine how many bits a specific value will require to be represented, we can use our fingers to help count. 

Pick a finger to start with. It's starting value is 2. Then count by doubling that value each time you hold up a new finger (2, 4, 8, 16, 32, …). When the number is >= the desired value, then count the number of fingers you have up and that's the number of bits needed to represent that value. 

Example: 

Desired Value: 70

| 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 |
|--- | --- | --- | --- | --- | --- | --- | --- |
|1 | 2 | 3 | 4 | 5 | 6 | 7 |

128 is the first number that's >= 70. By the time we hit 128 we have 7 fingers up. 

Therefore it'll take 7 bits to be able to get the value of 70

### New Subnet Addresses

To determine the network address space for new subnets: 
1. Determine the number of subnets needed. 
2. Calculate how many bits are needed to represent the number of subnets. 
3. Find the Least Significant Bit (LSB) of the Subnet Mask, the LSB is the block size of our new subnets. 
4. Write out subnets
5. Calculate Host address ranges of each subnet

Example: A company has a Major Network address space of 10.0.0.0/8 and a Headquarters address space of 10.1.0.0/16. How many bits would be needed to further subdivide the Headquarters network into 6 new subnets (separate subnet for 6 departments)? Answer: 3 bits

Each department subnet would have a new mask of 19 bits (The 16 bits of the Headquarters subnet + the 3 bits needed for each department). 

The first 16 bits are accounted for by the first 2 octets of the IP address. The third octet will be split into network and host address bits. We need 3 bits for our network address. Below is how the mask of the 3rd octet looks in binary. 

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 |

The Least Significant Bit (LSB) of the Subnet Mask is the smallest bit that is 1. In this case: 32. This will be referred to as the Block Size. 

Now the subnet can be written with each new subnet start at the location of the previous subnet + the block size. 

| Label | Subnet |
| --- | --- |
| A | 10.1.0.0/19 |
| B | 10.1.32.0/19 |
| C | 10.1.64.0/19 |

At least 1 bit of the host address has to be on, so the host address ranges will start at `<subnet>`.1

`<subnet>`.255 is reserved as the broadcast address for a subnet and therefore can't be used as a host address.  

| Label | Subnet | Host Address Range |
| --- | --- | --- | 
| A | 10.1.0.0/19 | 10.1.0.1 - 10.1.31.254 |
| B | 10.1.32.0/19 | 10.1.32.1 - 10.1.63.254 |
| C | 10.1.64.0/19 |10.1.64.1 - 10.1.95.254 |

### Calculating Hosts per Subnet

To calculate how many devices can be connected to a subnet, given it's number of host bits: 
Use the finger game to count out the powers of 2. Once the number of fingers held up matches the number of bits being counted, take that number and subtract 2 (to account for the network address and the broadcast address). 

Example: 

How many devices can connect to a /27 subnet?

If all bits in a subnet mask are on that's 32-bits. 32 - 27 = 5

| 1 | 2 | 3 | 4 | 5 |
| --- | --- | --- | --- | --- |
| 2 | 4 | 8 | 16 | 32 |

32 - 2 = 30

Answer: 30 hosts. 

---

## IPv6 Concepts

### IPv6 Overview

IPv4 addresses are 32 bits (4 octets) in length written as 4 decimal number separated by dots. 

IPv6 addresses are 128 bits in length written as 8 groups of hexadecimal numbers separated by colons. 

Example IPv6 address: 2045:0A59:0041:0000:0000:1045:7248

Each group represents 16 bits.

Hexadecimal numbers are base 16. After 16 digits, then carry the 1. To represent numbers over 0 letters of the alphabet are used. 

| Decimal | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 |
| Hexadecimal |  0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F | 10 |

The dividing line between the network and host portions of the IP address is still designated by a subnet mask. When using IPv6 the subnet mask is written exclusively using slash notation. 

### IPv6 Address Types

#### Global Unicast Addresses

Global address are IP addresses that can be routed on the public internet. 

Unicast means the packets are destined for a single destination host IP. 

Globally routable IPv6 addresses start with a 2 or 3. 

#### Link-Local Addresses

Link-Local addresses are used in IPv6 to connect with other IPv6 devices in the same subnet. 

Link-Local addresses start with FE80

An interface can have 2 IPv6 Addresses: 1 or more globally routable addresses and a link-local address. 

#### Multicast

When sending to a multicast IP, the traffic is routed to all IPs that are part of the multicast group. 

IPv6 multicast addresses start with FF

Packets sent to an IPv6 address starting with FF02::1 will go to every device on the network with an IPv6 address. 

IPv6 doesn't have a broadcast address, but this multicast address is close to performing the same function. 

Packets sent to an IPv6 address starting with FF02::2 will go to all routers on the network with an IPv6 address. 

#### Anycast

Anycast addresses are like global unicast addresses, but with two or more destinations that share the same network information. 

Example: Google DNS (8.8.8.8) is hosted on multiple severs. When a device makes a request to Google DNS, the closet server will respond. 

### Shorthand Notation

When an IPv6 address is written shorthand notation can be used by 
1. Leaving off any leading zeros
2. Omitting consecutive groupings of zeros and replacing them with a double colon (::)

Example: 
Long Form: 2003:0DB8:0002:0011:0000:0000:0000:BEEF/64
Shorthand: 2003:DB8:2:11::BEEF/64

###Neighbor Discovery Protocol

#### Router Solicitation | Router Advertising

A computer can search for all routers on an IPv6 network by sending a Router Solicitation (RS) request. The IP of a Router Solicitation will always start with FF02::2

If any routers are detected, they'll respond with their own address. This is call Router Advertising (RA). 

#### Neighbor Solicitation | Neighbor Advertising

A computer can find the network address of the network it's connected to by sending out a Neighbor Solicitation (NS) request to another client on the same network.

The client's response is called a Neighbor Advertisement (NA). 

IPv4 uses ARP to perform this functionality, but IPv6 doesn't use ARP nor broadcast addresses. 

#### Stateless Address Auto Configuration (SLAAC)

Instead of using DHCP to get an IP address, IPv6 workstations use Stateless Address Auto Configuration (SLAAC). 

In order for a workstation to talk on a network it needs to know it's IP address, the subnet mask, default gateway, and DNS server being used. 

When a device joins a network it'll perform a Router Solicitation to discover what network it's connected to. 

With the network portion known, the workstation will use EUI-64 (Extended Unique Identifier) to determine a unique value (uses the MAC address of the device to help create this unique value) to assign as the host portion of the IP address. 

### Transitioning to IPv6

#### Dual Stack

Dual Stack devices are devices that use the IPv4 and IPv6 protocols at the same time. 

#### Tunneling

If there's a part of the network that only support IPv4 traffic, but 2 IPv6 devices need to communicate over that network tunneling can be enable to allow this traffic. 

If 2 dual stack routers are setup at either end of the IPv4 section of the network they can embed the IPv6 traffic as a payload in an IPv4 GRE header, thereby create a tunnel for this traffic to passthrough. 

---

## Applications Layer Services

### Application Layer Overview

The Application Layer is the Functionality/Service the user is needing to access. 

Example: DNS, HHTP, SMTP

'nslookup' is a tool that can be used to verify DNS is working. It returns the IP address of a provided URL. 

[Application Research Center (paloaltonetworks.com)](https://applipedia.paloaltonetworks.com/) is a site that contains a database of applications and their common port numbers. 

### Core Web Services

| Protocol Name | Abbreviation | Port | Security Status |
| --- | --- | --- | --- |
| Hyper Text Transfer Protocol | HTTP |  TCP: 80 | insecure |
| Hyper Text Transfer Protocol Secure | HTTPS | TCP: 443 | secure |

Both HTTP and HTTPS are protocols used to browse the internet. 

HTTP is insecure, meaning the content payload is visible to anyone eavesdropping on the network. 

HTTPS uses a Secure Sockets Layer (SSL) or Transport Layer Security (TLS) to secure the connection by encrypting the traffic. 

Datagram Transport Layer Security (DLTS) uses TLS to establish a connection. However, once the connection is initially established it doesn't use the same overhead of a TCP port connection which grants it improved performance. 

Next Generation Firewalls (NGFW) add visibility for confirming what application services, and the well-known ports for those services, that are being used in the network.  

### Email Related Services

| Protocol Name | Abbreviation | Port | Security Status |
| --- | --- | --- | --- |
| Secure Mail Transfer Protocol | SMTP | TCP: 25 | insecure |
| SMTP over TLS | SMTP over TLS | TCP: 587 | secure |
| Post Office Protocol version 3 | POP3 | TCP: 110 | insecure |
| POP3 over SSL | POP3 over SSL | TCP: 995 | secure |
| Internet Message Access Protocol | IMAP | TCP: 143 | insecure |
| IMAP over SSL | IMAP over SSL | TCP: 993 | secure | 

[What are IMAP and POP? - Microsoft Support](https://support.microsoft.com/en-au/office/what-are-imap-and-pop-ca2c5799-49f9-4079-aefe-ddca85d5b1c9#:~:text=IMAP%20allows%20you%20to%20access,it%20from%20the%20email%20service.)

### Remote Access Services

| Protocol Name | Abbreviation | Port | Security Status |
| --- | --- | --- | --- | 
| Remote Desktop Protocol | RDP | TCP/UDP: 3389 | - |
| Virtual Network Computing | VNC | TCP/UDP: 5900-5903 | - |
| Telnet | Telnet | TCP: 23 | insecure | 
| Secure Shell | SSH | TCP: 22 | secure | 

Remote Access with a Graphical User Interface (GUI) is typically achieved using Microsoft Remote Desktop Services (RDS) or with Virtual Network Computing (VNC). 

If GUI access isn't needed, then Telnet or Secure Shell (SSH) grants Command Line Interface (CLI) access. 

Telnet sends data in plain text. This means anything sent during a Telnet session is sent in plain text (even logins/passwords). 

Secure Shell (SSH) encrypts the traffic. Only the 2 endpoints have the keys to decrypt the data. 

### DNS, DHCP, and NTP

| Protocol Name | Abbreviation | Port |
| --- | --- | --- |
| Domain Name System | DNS | UDP: 53 | 
| Dynamic Host Configuration Protocol | DHCP | Client - UDP: 68 / Server - UDP: 67 |
| Network Time Protocol | NTP | TCP/UDP: 123 |

Domain Name System (DNS) returns the IP address of a provided URL. 

Dynamic Host Configuration Protocol (DHCP): When a client powers on, if its been configured to use a DHCP server, it'll send a discover message on the network to look for the DHCP server. The DHCP server will recognize the request based on the request containing port number UDP: 68. 

Network Time Protocol (NTP) is used for devices connecting to a time server to synchronize their clocks. 

### File Services

| Protocol Name | Abbreviation | Port | Security Status |
| --- | --- | --- | --- | 
| Trivial File Transfer Protocol | TFTP | UDP: 69 | insecure |
| File Transfer Protocol | FTP | TCP: 21 | insecure | 
| Secure File Transfer Protocol | SFTP | TCP: 22 | secure |
| Sever Message Block | SMB | TCP: 445+ | - |

Trivial File Transfer Protocol (TFTP) has no overhead, no traffic gets encrypted, doesn't use authentication. NEVER use outside of a protected managed network. 

SMB (Server Message Block) is a Windows File Transfer Protocol. 

### Infrastructure Related Services

| Protocol Name | Abbreviation | Port | Security Status |
| --- | --- | --- | --- | 
| Simple Network Management Protocol | SNMP | TCP/UDP: 161 | v1/v2: insecure, v3: secure | 
| SNMP Trap | SNMP Trap | TCP/UDP: 162 | - |
| Lightweight Directory Access Protocol | LDAP | TCP/UDP: 389 | insecure | 
| LDAP over SSL | LDAPS | TCP/UDP: 636 | secure |
| SYSLOG | SYSLOG | TCP/UDP: 514+ | - | 


Simple Network Management Protocol (SNMP) uses agents on client devices and a management station that queries those devices for information like CPU Utilization, Fan Speed, etc. 

SNMP Trap generates a message that's sent to the management station when a device exceeds a specific threshold (ex. high CPU Utilization). 

Lightweight Directory Access Protocol (LDAP) is used for authentication against a Microsoft Active Directory (AD) environment. 

SYSLOG ("system logging") is used to send log messages to a centralized logging server to be sifted through when needed. 

### Database Services

| Protocol Name | Port |
| --- | --- |
| Microsoft SQL Server | TCP/UDP: 1433 |
| Oracle | TCP: 1521 | 
| MySQL | TCP: 3306 | 

Microsoft SQL Server, Oracle, and MySQL are all database management systems. 

### Multi-media and VoIP Services

| Protocol Name | Port |
| --- | --- |
| H.323 | TCP: 1720, 1731 |
| SIP | TCP/UDP: 5060, 5061 |
| Zoom | many |
| Google Hangouts | many |

Multi-Media Services and Voice over IP (VoIP) are services that run on a computer to call another computer and perform real-time communication.

SIP stands for Session Initialization Protocol. 

Zoom and Google Hangouts both rely on many other Application Layer Services in order to work. 

---

## Dynamic host Configuration Protocol (DHCP)

### DHCP Using Windows Server

If a client is configured to use DHCP and fails to contact a DHCP server, it'll received an Automatic Private IP Assignment (APIPA) address (starts with 169.). 

Proper planning must occur to ensure the DHCP server has enough addresses to hand out for the expected number of clients. Example: an IP range of .101-199 can support over a hundred clients. 

Some vendors require an entire subnet (Example: 10.1.0.0/24) be specified instead of a range (Example: 10.1.0.101-199).  In these cases exclusions need set to prevent handing out addresses of statically assigned devices. 

**probe**: In an attempt to prevent duplicate IPs on a subnet, the pings an address before assignment to ensure no response is received. 

**reservation**: instead of statically assigning an IP address to a device a DHCP reservation can be setup to always use the same IP Address when it receives traffic from the specific MAC Address

**lease**: the amount of time a DHCP Server has specified a client can use an address.

Clients will attempt to renew the lease, after a certain amount of time, prior to expiration. 

If a computer has been shutdown, when it powers back on it will attempt to renew the lease of its last known IP. 

All computers needs an IP Address, Subnet Mask, DNS, and Default Gateway to talk on a network. A DHCP server can be setup to provide all of these as DHCP Options and more (NTP, Domain Name, etc.). 

DORA
1. Discover - Client broadcasts a DHCP discover message
2. Offer - DHCP Server offers an address, that it hasn't handed out yet, back to the client
3. Request - Client sends a request to accept the IP Address offered
4. Acknowledgement - DHCP Server sends a final acknowledgement that the IP is being assigned to that client. 

### DHCP Server on a Windows Server

This video section was a demonstration of a Windows Server acting as an IPv4 DHCP Server and a Windows 10 device acting as a DHCP client. 

![[WindowsDHCPServer.png]]

`ncpa.cpl` in the run command to launch the Network Connections window on a Windows client. 

Use of Windows as a DHCP Server requires a Windows Server License. 

### DHCP Server on a Cisco Router

Rather than sending DHCP traffic across a Wide Area Network for a remote site, it might make sense for the router or firewall at the remote site to be setup as that site's DHCP server. 

Check to see if any DHCP services are already running on the device: `show running-config | include dhcp` - 
Create a DHCP pool with the specified name: `ip dhcp pool <name>`
Specify the network/subnet (use slash notation) DHCP is being configured for: `network <network>` 
Create DHCP exclusions for a range of addresses: `ip dhcp excluded-address <low-address> <high-address>` 
Set the default gateway: `default-router <router-ip>` 
Set DNS: `dns-server <dns-ip>` 
Review the DHCP settings and exclusions: `show run | section dhcp`
Monitor/Debug DHCP traffic: `debug ip dhcp server packet`
Show leased DHCP addresses: `show ip dhcp binding`

### DHCP Server on a Palo Alto Firewall

![[PaloAltoFWDHCPServer.png]]

Multiple devices (ex: Windows Server and Firewall) can be configured to act as DHCP servers and run at the same time to provide fault tolerance. 

Make sure each device acting as a DHCP server has a separate pool of addresses to hand out to prevent duplicate IPs. 

When a client makes a DHCP Discover request, and multiple DHCP Servers are configured, both servers will make an Offer. The client will typically accept the offer from whichever DHCP server responded first. 

To prevent a DHCP server from acting as the primary source, a DHCP delay (of a specified number of microseconds) can be set. 

### DHCP Relay

A DHCP Relay allows for connection to a DHCP Server that isn't directly connected to the same network as the client making the request. 

When DHCP configured client boots, then sends an initial DISCOVER request that request is a Broadcast message. Broadcast messages are only sent to devices in the local network. 

Helper/IP Helper/UDP Forwarding: a router feature that enables forwarding of DHCP requests to a DHCP server in a different network

---

## NTP and DNS

### NTP Overview

Network Time Protocol (NTP) is used to keep the time synced on network devices. 

NTP uses port UDP: 123

Issues with Incorrect Time
- If the time between devices is incorrect, then system logs will have different timestamps, thereby making issues harder to troubleshoot. 
- Windows Active Directory (AD) rotates a key for authentication that relies on accurate time. 
- If Digital Certificates are used for authentication, then systems with incorrect time may not be able to access resources (Ex: A system with time 2020 attempting to access a Certificate valid between 2021-2025, the system will receive a certificate invalid error).

A partial workaround would be to have the SYSLOG server change the timestamp of the log to the time the SYSLOG server received the log, but ideally all Infrastructure Systems and SYSLOG Systems have the same synced time for correlation. 

NTP is served in Universal Time Coordinated (UTC). 

The rest of the world not in the UTC time zone will have a hour offset. 
- Example: North American Central Standard Time (CST) is UTC-6:00
- Example (cont.): During Daylight Saving Time (DST) Central Daylight Time is used,  instead of CST, which is UTC-5:00

Some Companies, especially those with offices world-wide elect to setup their reporting using the same UTC time for all locations. 

NTP Stratums - The lower the stratum number, the closer to the atomic/reliable time source
1. Atomic Clock
2. Government/Publicly-Available Time Servers
3. Local Router
4. Local Devices

If using Active Directory, clients can get their time from the AD Server. 

### NTP Demonstration

[NTP Pool Project](https://www.ntppool.org/en/) is a publicly available site that a router can connect to for Time Syncing. 

When connecting a router to the public NTP server it can can several minutes to a few hours to finish syncing. 

### DNS Overview

Domain Name System (DNS) is used to return the IP Address of a domain name. 

DNS uses UDP Port 53. 

! Insert Image

Every specific domain will have an Authoritative DNS Server. 

Example of DNS Query for cisco.com
1.  A Client PC makes a request to a local DNS Server. 
2. The server queries the root for the name servers of .com. 
3. The server then queries the Top Level (.com) to get the the name server of the Domain (cisco.com)
4. The server then queries the Domain (cisco.com) to get the Authoritative DNS Server. 
5. The server then queries the Authoritative DNS Server to get the IP Address. 
6. The DNS Server then returns the IP Address of the site to the Client PC. 

DNS Cache - when a DNS Server makes each of these requests, it caches the responses in order to have that information for future requests. 

Poisoning - an attacker/hacker manipulating the DNS Cache to return the wrong IP Address for a Site. Typically done to perform a phishing scheme (see Credential Harvest below). 

Credential Harvest - redirecting a user to a site that looks like the official site the user wants to access, so they'll put in their credentials. 

### DNS Record Types

#### NSLOOKUP

`nslookup` is a command used to query DNS. 

`nslookup <url>`
Example: `nslookup cisco.com`

A specific Record Type can be request when using `nslookup`
`nslookup -type=<type> <url>`
Example: `nslookup -type=aaaa cisco.com`

`nslookup` uses the DNS Servers configured on the client. The configured DNS Server isn't always the authoritative server for the domain being looked up. This may cause `nslookup` to return results listed as "Non-Authoritative Answer"

An Authoritative Answer is a response from the name server who's in charge of the domain. 

Performing an `nslookup` specifying the `ns` type will return the authoritative name server(s) for the domain. 

Example: `nslookup -type=ns cisco.com`

Once the authoritative name server is known, we can use `nslookup` to query the authoritative name server. 
`nslookup <url> <nameServer>`

To view all records of a domain use `nslookup -query=any <url>`

#### Record Types

| Record Type | Description | 
| --- | --- |
| A | IPv4 Address | 
| AAAA | IPv6 Address | 
| NS | Name Server |
| CNAME | Alias | 
|SOA | Authoritative | 
| PTR | Reverse Lookup |
| MX | Email Server |

An **A** record returns the IPv4 record for a domain. 

An **AAAA** record returns the IPv6 record for a domain. 

An easy way to remember **AAAA** for IPv6 is to remember an IPv4 address is 32-bits, an IPv6 address is 128-bits, which is 4-times larger. 

A **NS** record returns the authoritative name server for a domain. 

A **CNAME** record returns any aliases that can be used to access the primary domain. 

**CNAME** stands for Canonical Name. 

Multiple names can be mapped to the same **A** record. 

A **SOA** record stands for "Start of Authority". This record contains administrative/authoritative information about the zone. 

A **PTR** record allows for Reverse Lookups. **PRT** stands for "Pointer". A reverse lookup returns the domain of a given IP. 
`nslookup <ipAddress>`

A **MX** record returns the email servers configured for the domain. **MX** stands for "Mail Exchange". 

### DNS Server Demonstration

One a Windows DNS Server there's a Forward Lookup Zone and a Reverse Lookup Zone. 

The Forward Lookup Zone is used for normal lookups (i.e. what's the IP of this domain).

A Reverse Lookup Zone contains the information for reverse lookups. 

Pointer Records (PTR) exist in the Reverse Lookup Zone. 

The name of the Reverse Lookup Zone for a domain must begin with the first octet of the domain's IP flipped. (e.g. A 10.1.0 network would have a Reverse Lookup Zone that begins with 0.1.10). 

---

## Network Architectures

### Network Architectures Overview

![[Network Architectures Overview.png]]

The 3-Tier Network Architecture is typically used in campus and enterprise networks. 

3-Tier Network Architecture has 3 Layers: 
1. Access Layer - devices connecting to the network through a layer 2 switch. 
2. Distribution Layer - uses multilayer switches to connect between layer 2 switches. 
3. Core Layer - connects blocks/groups on the network and to the outside internet. 

Multilayer Switch - device that can perform layer 2 forwarding (like a switch) and layer 3 routing (like a router). 

The 2-Tiered Networks Architecture is typically used in Data Centers. 

2-Tier Network Architecture has 2 Layers: 
1. Leaf Layer - hosts connecting to switches
2. Backbone/Spine Layer

Every Leaf Layer switch will have a connection to every Backbone device. 

In a 2-Tier Network there aren't any horizontal connections between devices on the same layer. 

Storage Networks are used to connect to storage devices. 

Wide Area Network (WAN) connects network devices across long distances (i.e. cross-country, worldwide). 

### Three-Tiered Architecture

![[threeTieredArchitecture.png]]

The 3-Tiered Architecture consists of 3 Layers: Access, Distribution, and Core

The Access Layer contains Layer 2 switches. 

The Distribution Layer uses Multilayer Switches to interconnect the switches. 

The Core Layer uses Multilayer Switches to connect groups on the network and connect to the outside internet. 

### Datacenter Architecture

A 2-Layer Architecture uses 2 Layers: Leaf Node Layer and the Backbone/Spine Layer. 

This architecture is typically used in Datacenter to support the high amounts of East-West (traffic between hosts) traffic. 

The Leaf Layer contains Layer 2 switches that clients connect to. This layer 2 switch is typically positioned at the Top of the Rack (ToR Switches). 

The Backbone/Spine Layer uses Multilayer switches that connect the Layer 2 Switches together and provides connectivity to the outside internet. 

Connections are present from every Leaf Layer Switch to every Backbone Layer Switch. 

There aren't any horizontal connections between devices on the same layer (i.e. there aren't any cross connects between Leaf devices, nor are there any cross connects between any Backbone devices). 

The 2-Tier architecture is designed to support the high levels are traffic between hosts. 

East-West Traffic is traffic going between one host and another in the data center. 

North-South Traffic is traffic leaving or coming into the data center. 

NetFlow is a network protocol developed by Cisco for collecting IP traffic information and monitoring network flow.

### Storage Area Networks

As technology has updated a lot of storage, especially in data centers, is no longer physically attached to the actual hosts. 

Network Storage access needs to be fast and not bottlenecked. 

If a physical host is about to fail or a move is planned to another hypervisor, the new hypervisor won't have access to the data. 

If storage is on the network, then all the hosts have access to that data. 

Options for Accessing Storage over a Network: 
- Fibre Channel: a dedicated network, using proprietary hardware, for storage. Fibre Channel is high-speed and reliable, but pricy. 
- Fibre Channel over Ethernet (FCoE): uses Fibre Channel technology, but over an Ethernet connection. Still high-speed, but less expensive due to not needing proprietary hardware. 
- iSCSI: Small Computer System Interface (SCSI) commands were used for computers to communicate with their hard disks. SCSI was originally used with locally attached storage. iSCI uses the same SCSI commands, but over an IP Network (hence the "i" in iSCSI). 

Both Fibre Channel and FCoE are setup on separate networks with dedicated bandwidth just for storage. Multiple network adapters are used to support higher throughput and provide fault tolerance. 

Accessing resources/drives using iSCSI is an example of a Storage Area Network (SAN). 

SANs used Block Based Storage to allow devices to access data blocks (i.e. chunks, groups) at a time.

In environments using iSCI / SAN, it's good practice to section off a separate area of the network for storage traffic. This can be achieved by setting up a VLAN. 

Network Attached Storage (NAS) is file-based (instead of block-based, like SAN) storage access. 

Network File System (NFS) is the protocol used to access NAS. 

### Wide Area Networks

Local Area Networks (LAN) use high-speed communications in a fairly small geographic area (within a building/couple buildings). 

Wide Area Networks (WA) are used to connect large areas (e.g. cross country sites). 

WANs require a service provider to provide the connectivity. 

In the early days WANs used leased lines on serial connections. In the 90s frame-relays were sused. Now the internet is used, provided by service providers. 

WAN overlay uses GRE logical tunnels to connect sites. 

GRE packets aren't encrypted. Anyone in the packet path can see the packet data. 

IPsec (IP Security) is a suite of protocols used to encrypt packets over the internet. 

### Software Defined Networking (SDN)

In Software Defined Networks (SDN) | Software Defined Wide Area Networks (SDWAN) an admin uses a controller to define the intent/layout of the network. The controller than handles the implementation. 

3 Planes: Management, Control, Data
1. Management Plane: the processes, communications, and methods administrators use to connect and configure (get/set/update) devices
2. Control Plane: Manages how devices forward traffic
3. Data/Infrastructure Plane: The packets being moved

The Management Plane tells devices what to do, the Control Plane determines how to do it, and the Data Plane is the occurrences of those actions. 

SDN is the first 2 Planes. An admin uses a management PC to give instructions/intent to the Control Center and the Control Center handles determining the how. 

Intent examples: 
- A computer that should only have access to a specific group of servers, regardless of where it's plugged into on the network. 
- Management of Wireless Access Points (WAPs).
- Tunnels between sites.

---

## Cloud Service Fundamentals

### Cloud Service Overview

Cloud Services are services someone else is providing. 

**Cloud Apps** includes Software as a Service (SaaS), where the service provider provides the application, a place for data, the OS, virtualization, CPU, Memory, Storage, and Networking. 

Cloud Apps are typically access via a web browser. 

A **Cloud VM** includes Infrastructure as a Service (IaaS), where the client rents a Virtual Machine (VM). 

Cloud VMs are typically access by clients connected using a Virtual Private Network (VPN). 

A VPN logically places a PC on the same network as the VM. 

Who's using these services?
- **Public Cloud** services are available to anyone. 
- **Private Cloud** services are only available to a specific group/company. 
- ** Community Cloud** services are shared by 2 or more organizations or subgroups with similar needs/interests (ex: Government projects). 
- **Hybrid Cloud** services are a mix of both public and private cloud services. 

With Automation clients can specify what they want setup and have it automatically created.  

Infrastructure as Code (IaC): the script and applications used to provide consistent results when rolling out new devices and systems

Software Defined Network (SDN): an approach to networking that uses software-based controllers or application programming interfaces (APIs) to communicate with underlying hardware infrastructure and direct traffic on a network.

Multi-Tenancy: multiple customers using cloud services hosted on the same piece of hardware. 

scalability is the ability to grow as needed (increase resources or add hosts to support the load). 
elasticity is the ability to shrink as needed, so client only pays for what their using / what their needs are. 

### Service Models

![[Cloud Service Models.png]]

On-Prem: On-Prem servers are servers hosted on premises, meaning on site at the clients location. The clients is responsible for all parts of hosting. 

**Infrastructure as a Service (IaaS)**: the customer pays the service provider for the physical hardware, but manages their own VMs (i.e. customer is renting Virtual Machines from the Service Provider) 

**Platform as a Service (PaaS)**: the customer pays the service providers to host and manage the virtual machines. PaaS is typically used by developers as an environment to develop their applications. 

**Software as a Service (SaaS)**: the customer pays for use of an application (e.g. Google Docs, Microsoft Teams, Zoom)

[Website & Web App Deployment - AWS Elastic Beanstalk - AWS (amazon.com)](https://aws.amazon.com/elasticbeanstalk/) AWS Elastic Beanstalk - quickly deploy and manage applications in the AWS Cloud without having to learn about the infrastructure that runs those applications. 

**Function as a Service (FaaS)**: instead of having an application run on a specific server, the customer supplies an executable to the service provider and is paying the service provider to execute and run it. 

**Desktop as a Service (DaaS)**: VMs used as Desktops that clients can remotely connect to. 

**XaaS** stands for "Anything as a Service"

### Infrastructure as Code

Infrastructure as Code (IaC) includes scripts and commands used to implement network configurations. Automation is setup to check for and alert of changes to the network. 

3 Main Concepts: 
- Software Defined: scripts/commands are used to deploy and configured the network, then verify it's online.
- Automation: automation checks for changes and provides alerts
- Orchestration: orchestration coordinates and rolls out details, configuration, and deployments without having to manually implement those changes

These concepts are to ensure consistency and checks for environment changes. 

The network can be configured to point connecting clients to a Load Balancer IP. The Load Balancer can then connect the client to an appropriate/available server based on usage and other factors. 

Application Programming Interface (API): a way to interact with networking devices. 

### Demand Based Resources

Scalability and Elasticity

**scalability**: as system resources get overloaded, scalability is the ability to add more resources as needed

Adding additional servers/VMs and using a load balancer are ways of providing scalability. 

When users connect to the virtual IP of the load balacer it keeps track of the VMs and determines which to connect client to. 

**elasticity**: automates the process of adding/removing servers as needed. 

When using SaaS or IaaS the service provider can implement elasticity to charge the client only for the services they're using. 

### Cloud Security Concerns

[World’s Biggest Data Breaches & Hacks — Information is Beautiful](https://informationisbeautiful.net/visualizations/worlds-biggest-data-breaches-hacks/)

#### Data Breaches

The service provider holds the clients data. The client should ensure the data is: 
- stored appropriately (within the geographical boundaries for the country)
- meets encryption requirements
- secure (that the service provider won't have the data leaked or stolen)
- accessed only using HTTPS or VPN
- only authenticated users should have access to the data

#### Hacked Accounts

Hackers can using phishing or other methods to gain access to a user's username/password. 

Implement Multi-Factor Authentication to prevent access even is a user's credentials are known. 

#### Insider Threat

An insider threat is an internal user (e.g. disgruntled employee) leaking data. 

#### Malware

A user may not be malicious, but may have malicious software (malware) installed. 

To prevent malware issues: 
- A Host-Based Intrusion Prevention System (HIPS) should be setup; or at least anti-virus/anti-malware software should be install on every client PC. 
- Used a next-gen firewall with SSL/TLS decryption to analysis traffic to look for malicious files. 

#### Weak APIs

API stands for Application Programming Interface. APIs are a way to interact with network devices to direct network traffic. 

It's now common practice for IT to talk (input commands) on a controller. The controller then uses an API to push out the desired changes to the network. 

Authentication needs to be setup between the controller and API to ensure insecure/weak APIs aren't being used. 

#### Distributed Denial of Service (DDos) Attack

Hackers can use a controller to instruct a botnet (army of computer) of infected machines to perform an activity. 

The botnet can be used to access a site and thereby use up the site's bandwidth and resources, which prevents real customers from access the site. This is called a Denial of Service (DoS) Attack. 

A Distributed Denial of Service (DDoS) attack is the term for when the attacking machine's origins are spread across the planet.

#### Multi-Tenancy

Since multiple customers share the same hardware, make sure the service provider is providing the correct isolation and segmentation between customers to ensure customer actions don't affect/impact one another. 

#### Data Loss

Make sure to take proper backups. 

The person who cares most about your data is you. 

Restore Point Objective (RPO): defines the point of return for backups (i.e. what should the backups be able to return to (e.g. previous week, day, hour, etc.))

---

## Network Infrastructure Devices

### Layer 1 Devices

Physical Layer (Layer 1) Forwarding Devices

#### Hub (Layer 1 Hub)

Features: 
- Layer 1 Device
- Multi-Port Repeater
- 1 Collision Domain ("1 lane road")
- 1/2 Duplex
- 1 Broadcast Domain

A Hub has has no idea of addressing, forwarding, nor packets. 

Hubs take signals (1s and 0s) from one port and repeats the signal on all other ports. 

Topologies: Logical Bus | Physical Star

1 Collision Domain: Only 1 device can talk at a time. A collision occurs if two or more devices attempt to talk at the same time. 

Operates at half duplex, meaning a device connected to the hub can send or receive, but can't send/receive at the same time.

1 Broadcast Domain: IPv4 broadcast traffic is sent to all other devices on the network. 

#### CSMA/CD

Carrier Sensing Multiple Access with Collision Detection
- Carrier Sensing: before a PC attempts to talk on a network it'll first listen to hear if anyone else is sending data at that same time
- Multiple Access: multiple devices are (or could be) connected to the single collision domain
- Collision Detection: if multiple PCs attempt to send a signal at the exact same time they'll be able to detect if the signal crashed

**repeater**: takes signals from one end and passes it out the other (i.e. essentially a 2-port hub)

**media converter**: performs conversion of media types (e.g. converting electrical signals over copper to light signals over fiber)

### Layer 2 Devices

Layer 2 Forwarding and Switching is the activity that happens between routers. 

#### Layer 2 Ethernet Switch

Layer 2 (Data Link) Ethernet Switch

Features: 
- Layer 2 Device
- 1 Collision Domain per Port
- Full Duplex
- 1 Broadcast Domain

Layer 2 Ethernet Switches are aware of, and make forwarding decisions based on, Layer 2 (MAC) Addresses

A MAC address is 48-bits long, typically represented as 12 hexadecimal characters.

Layer 2 Addresses are also referenced as:
- Layer 2 Address
- MAC (Media Access Control) Address
- Physical Address
- BIA (Burned In Address)
- Ethernet Address

To learn the Layer 2 Address of a Windows PC: run `ipconfig /all`, then look for the `Physical Address` field. 

A Layer 2 Switch knows the MAC Addresses of each device connected to it. This allows the switch to pass a frame along directly to the Port the frame is destined for. 

Each port on a switch is its own collision domain. 

Switches have 1 Broadcast Domain, meaning broadcast traffic is sent to all devices connected to the switch. 
Broadcast  - when a computer configured for DHCP boots, it sends out an ARP broadcast request. Broadcast is sent to all devices on the network. 

#### Layer 2 Bridge

Layer 2 Bridges were present in the early days of networking. 

A Bridge is essentially a Switch with only two ports. 

### Devices at Layer 3 and 4

A Layer 1 Hub (Physical Hub) takes bits coming in on a port and blindly repeats them on all other ports. Layer 1 Hubs have 1 Collison Domain and 1 Broadcast Domain. 

A Layer 2 Switch memorizes the Layer 2 Addresses of each device connected to it and can make forwarding decisions based on the addresses its learned. Layer 2 Switches have 1 Collision Domain per Port and 1 Broadcast Domain. 

Layer 3 (Networking) Layer Devices (typically routers) make forwarding decisions based on Layer 3 IP Addresses. 

If a PC wants to forward traffic to a device on a different network, the PC is aware the device isn't on the same network, so it'll forward the traffic to the Default Gateway. A Switch grabs the frame and passes it directly to the router (Default Gateway). The router gets the frame, then de-encapsulates it. It looks at the destination IP address and, if it knows how to forward it, it'll send it to the next router. 

Devices that can do Layer 3 Routing: routers, firewalls, multi-layer switches (can do Layer 2 switching and Layer 3 routing). 

Most of these devices can also make decisions based on Layer 4 Protocols (ACL, PAT, etc.). 

Access Control List (ACL): deny/allow traffic based on ports and protocols. 

### Application Layer Devices

proxy: a device that does something on behalf of another device

#### Proxy Server

A network can be configured to redirect PC internet request through a Proxy Server first. 

A Proxy Server can be configured to analyze and work with the entire protocol stack in order to filter traffic and implement rules. 

Policy at the application layer can be enforced using a Proxy Server

#### Next Generation Firewall (NGFW)

A Next Generation Firewall (NGFW) acts as a middleman between a PC and a server  that has the ability to look at the application layer and setup rules/policies. 

Next Generation Firewalls (NGFW) are aware of the apps being used/requested.
Example: Granting users access to Facebook, but denying access to Facebook File Transfer and Facebook Chat. 

#### Unified Threat Management System (UTM)

A Unified Threat Management System (UTM) is typically a Next Generation Firewall (NGFW) with Application Layer visibility and the ability to manage proxy services, decryption services, intrusion prevention services, and perform Application Layer filtering

#### Proxy Cache

When a client requests a site, the proxy can cache the site data. This way, if multiple clients request the same site, the content can be delivered directly from the Proxy Server (if the cache is current).

Caching helps with performance issues

#### VoIP Gateway
A VoIP Gateway is a device that runs at the Application Layer to convert VoIP digital phone signals to physical/non-IP phones connected to a PBX

---

## IP Routing

### IP Routing Overview

**routed protocol**: a Layer 3 protocol with information in IP Packets that can be used to make forwarding decisions (example: IPv4, IPv6)

When routers forward a packet they work through 2 planes: 
- Control Plane: (the how) learn routes to a network 
- Data Plane: (the doing) forward the packet

#### Control Plane
The 3 Ways Routers Learn About (How to Get To) Networks 
1. Directly Connected - routers know the networks they're directly connected to
2. Static Route - a manually configured route
3. Dynamic Routing Protocol -  an application (or app-like service) that allows routers to share the routes they know with routers on different networks. 

When a route is learned, the router places it in its routing table.

To view the routing table of a Windows PC run `netstat -r`

### Directly Connected Networks

A router directly connected with a Network Interface Card (NIC) knows exactly how to reach the networks its connected to.

One way of training a router how to reach a network is to directly connect the router to that network.

### Static Routes

Static Routes are manually configured routes set on the router to inform it of the destination, or next hop traffic should be forwarded to to reach that destination. 

**default route**: if there's a better or longer match in the routing table for a destination address, then use the instructions in the default route (typically the default gateway) to forward the packet.

Static Routes can be configured based on a:
- network address (e.g. 10.1.0.0/24)
- host address (10.1.0.2/32) | a host route is an exact 32-bit match for a specific IP address
- default route

A default router is represented with a network and subnet mask of all zeros (0.0.0.0 0.0.0.0).

To view routes on a Windows PC run `route PRINT`

### Dynamic Routing Protocols Overview

Dynamic Routing Protocols: a way for routers to share what networks they're connected to (i.e routers talking to other routers)

**routing domain**: the routing devices (routers, firewalls, multi-layer switches) under our control 

#### Interior Gateway Protocols (IGP)

| Protocol | Method |
| --- | --- |
| RIP | Distance Vector | 
| OSPF | LInk State |
| IS-IS | Link State |
| EIGRP | Hybrid |

Interior Gateway Protocols (IGP) are the dynamic routing protocols used at a company level. 

The Interior Gateway Protocol (IGP) to use depends on what the devices on the network support.  

##### Distance Vector

Distance Vector is a method of implementing an Interior Gateway Protocol. 

Using the Distance Vector method, routers that are directly connect to a network advertise their connection to the other routers its connected to. Each router also shares the knowledge they learned from the routers sharing knowledge with it.  "Routing by Rumor"

Example: Routers A, B, and C have networks connected to them. Router A is directly connected to Router B and Router B is directly connected to Router C, but Routers A and C aren't connected. C shares the networks its connected to with Router B. Router B shares the networks its connected to and the networks it learned Router C is connected to with Router A. 

Metric Cost: Distance Vector measures paths to an IP using *hops*. Each router in the path to an IP counts as a hop. 

If multiple routers advertise a path to an IP, the router sending the traffic will choose to send the traffic to the path with the shortest number of hops. 

The **Routing Information Protocol (RIP)** is the oldest and most popular protocol using the Distance Vector method. 

##### Link State

Link State is another method of implementing an Interior Gateway Protocol. 

Using the Link State method, routers advertise the networks it's connected to, and the state of those networks (i.e. link state, e.g. up/down), to all other routers on the network. 

Every router using a protocol that uses the Link State method can build a logical map of where all the networks are and the best paths to reach them. They put that in their routing table. 

Metric Cost: Link State measures paths to an IP as *cost*. 

Example: OSPF assigns a cost value for each route to a network. If there are multiple paths to the same network, the path with the lowest cost will be used.

##### Hybrid

EIGRP is a proprietary protocol developed by CISCO systems. EIGRP primarily uses the Distance Vector method with some characteristics of Link State. 

##### Variable Length Subnet Masks (VLSM)

RIP version 1 only supported fixed length subnet masks. 

RIP version 2 and OSPF support variable length subnet masks (VLSM)

##### Route Redistribution

If two companies merge that were using two different routing protocols (e.g. RIPv2, OSPF, etc) a router can be installed between the networks that's aware of both protocols and can share routes. 

This is not best practice and should only be implemented as a temporary solution. 

#### Exterior Gateway Protocol (EGP)

Exterior Gateway Protocol (EGP) is used for large networks (hundreds of thousands of devices), typically by service providers to share routes with each other.

Uses the Border Gateway Protocol (BGP).

### RIP

Routing Information Protocol (RIP) is a dynamic, Distance Vector routing protocol. 

Version 1 only supports fixed length subnet masks | Version 2 supports Variable Length Subnet Masks (VLSM)

Layer 3: Advertisements are sent using Multicast address of 224.0.0.9
Layer 4: RIP uses UDP port 520

Administrative Distance: the believability or preference for a certain source regarding a route. 

If a router learned about a route from 2 different sources (static route and RIP), the router will use the route with the lowest administrative distance. 

Administrative Distance in CISCO Systems:
| Route | AD | 
| --- | --- | 
| Static Route | 1 |
| RIP | 120 |

If there are 2 routes to the same address that were both learned using RIPS, then the router will use the route with the lowest cost. 

RIPS uses **hop count** as it's cost. 

### OSPF

Open Shortest Path First (OSPF) is a Link State routing protocol.

Link State: every device running OSPF (OSPF speakers) sends advertisements with all their links and the state of those links

Links are forwarded from each router to every other router, so the all share knowledge of the available routes. Each router uses that data to build a map and adds the shortest path for each destination to its routing table.

OSPF has its own layer 4 protocol. 

Layer 3: Multicast 224.0.0.5/6

Layer 4: OSPF port 89

Administrative Distance for OSPF (In CISCO systems): 110

### EIGRP

Enhanced Interior Gateway Routing Protocol (EIGRP) is a Hybrid routing protocol, though it behaves mostly like a Distance Vector protocol. EIGRP does "routing by rumor" (i.e. Distance Vector - the router only knows the paths its direct neighboring routers are telling it), but also establishes formal adjacencies with those neighbors and keeps track of them. This way if a router goes away, or a route becomes missing, the router can search for that route. 

Layer 3: Multicast 224.0.0.10

Layer 4: EIGRP port 88

Administrative Distance for OSPF (In CISCO systems): 90

Cost: Composite Metric

### BGP

Border Gateway Protocol (BGP) is a protocol used between Service Providers to handle the tens to  hundreds of thousands of routes that make up the internet. 

In BGP, each Service Provider is assigned an Autonomous System number.

Internal BGP (iBGP): All routes have the same Autonomous System number. 

External BGP (eBGP): Two devices in different Autonomous Systems peering with each other. 

Layer 3: BGP uses the Unicast address of its peer (the router it's talking to). 

Layer 4: TCP port 179

Administrative Distance for eBGP (In CISCO systems): 20

Administrative Distance for iBGP (In CISCO systems): 200

---

## Ethernet Switching

### Layer 2 Switching Review

PCs connected to Layer 2 switches using a wired connection, typically Ethernet.

Connecting devices to a command segment doesn't equate to having an IP Addressing scheme in place. Layer 3 networks need to be planned. 
- Determine network addressing (ex: 10.1.10.0/24)
- Configure router. Setup router as the Default Gateway (ex: 10.1.10.1)
- Configure the router to act as a DHCP Server (hands out IP Addresses, Subnet Mask, Default Gateway, and DNS Server)

Layer 2 Switches dynamically lean the Layer 2 (MAC) addresses of the devices that are connected to its ports. A single frame from a connected device is all it takes for the switch to learn the device's MAC Address. 

Layer 2 Switches forward traffic based on Layer 2 Addresses.

Example: 
If PC1 wants to forward traffic to the Default Gateway, the PC1 Layer 2 Address (MAC) is the Source MAC Address. PC1 makes an ARP request to learn the Layer 2 MAC Address of the Default Gateway. When the switch receives a broadcast request (ex. ARP) it forwards the broadcast traffic to all other ports in the broadcast domain. 

Unicast vs. Broadcast vs unknown broadcast
- Unicast traffic is traffic from 1 device to another device. 
- Broadcast Traffic is traffic from 1 device to all other devices in the same broadcast domain. 
- Unknown Unicast Traffic (traffic to a destination MAC that the switch doesn't know at the time of request) is forwarded to all other ports on the switch (i.e. handled the same as broadcast traffic). 

Every port on a switch is its own collision domain (i.e. acts as its own road). 

Switches can perform Full Duplex communication, meaning data can be sent and received simultaneously between a switch and connected devices.

Because each port on a switch is its own collision domain and supports Full Duplex communication, switches can disable CSMA/CD. 

Switches have 1 broadcast domain. 

Virtual Local Area Networks (VLANs) are carved chunks of address space on a switch that act as their own broadcast domain. 

### VLANs and Routing

Virtual Local Area Networks (VLANs): the process of carving a broadcast domain into smaller broadcast domains

Broadcasts are forwarded to all ports of a Broadcast domain, even if the connected devices of that broadcast domain use separate logical network addresses/subnets. 

Each VLAN is its own broadcast domain. The default broadcast domain is VLAN 1, which is all ports. 

VLAN numbering doesn't have to match the IP Network numbering, but there is a 1-to-1 correlation between IP Networks and VLANs. Typically, there's a separate VLAN for each IP network. 

A VLAN represents a Layer 2 enforced Broadcast Domain. Each device in a given VLAN cooperates using the same IP Addressing scheme.

Broadcasts stay in the broadcast domain. 

For communication to occur between two networks/VLANs, there must be a Layer 3 device between the networks to acts a door/path for traffic.

VLANs can share a router to act as the Default Gateway for both networks. 

Switches make Layer 2 forwarding decisions based on Layer 2 addresses. 

Routers make routing decisions based on Layer 3 information (i.e. IP Addressing information, specifically the destination IP Address in an IP Header). 

### The Multi-Layer Switch

Multi-Layer Switch (MLS): a device that can perform Layer 2 forwarding (exactly like a Layer 2 switch) and has the ability to have Layer 3 interfaces acting exactly like a Layer 3 router (making routing decisions based on IP Addresses). 

Logical Layer 3 interfaces can be created on switches that support Multi-Layer Switching (MLS); on Cisco devices these interfaces are call Switched Virtual Interfaces (SVI). 

IP Addresses are assigned to the Switched Virtual Interfaces (SVI) and associated with a specific VLAN. 

A Multi-Layer Switch (MLS) , with its multi-layer routing capabilities and Switched Virtual Interfaces (SVI), can perform the logical Layer 3 routing between subnets on separate VLANs. 

### Multi-layer Switch Demonstration

Disabling unused ports on a switch and assigning them to an unused VLAN is good practice for security. 

Multi-Layer Switches, like routers, also participate with dynamic routing protocols. 

---

## Enterprise Ethernet

### Enterprise ethernet Networking Overview

#### Connectivity

For a VLAN to be present on multiple switches, the switches must be connected (e.g. ethernet, fiber, copper, wireless). 

Connection using an Ethernet cable between switches (or any like devices) requires a cross-over cable. 

MDI-X | Auto MDIX: a feature of networking devices that allows for connection of like devices regardless of whether a cross-over or straight-through cable is used. 

Even if MDI-X is present, using the correct cable type (cross-over) is still the preferred method of connection. 

#### Trunking (802.1Q)

When a Layer 2 frame is sent between switches, then sending switch needs to add a tag to the frame to indicate which VLAN the frame is associated with. 

Trunking is used to include the tag numbers when frames are forwarded. 

#### Loops

Time to Live (TTL): a value for the period of time that a packet should exist

Whenever a router forwards a packet it lowers the TTL. If there's a loop in the network the routers will stop forwarding the packet when the TTL reaches zero. 

TTL is a concept of Layer 3 devices. This concept doesn't exist at Layer 2. Therefore, a packet could loop endlessly between switches. 

Spanning Tree Protocol (STP): a protocol, that runs in the background, that identifies parallel paths. If a loop is detected STP drops one of the links causing the loop. 

#### Link Aggregation (LAG)

Link Aggregation (LAG) takes 2 or more physical connectors and logically bundles them together, so Spanning Tree Protocol (STP) only see 1 large connection. This allows for the bandwidth/connectivity of parallel paths, without having links dropped by Spanning Tree Protocol (STP). 

Loops can't occur over a Link Aggregation (LAG) connections. 

Link Aggregation Control Protocol (LACP): the protocol used to with Link Aggregation (LAG)

#### Quality of Service (QoS)

The needs of apps differ. For example: latency of a few ms isn't an issue when sending email, but a few ms delay when using VoIP is unacceptable in terms of call quality. 

VLANs can be created for specific services so traffic for those services can be treated special (e.g. logically placing Voice and VoIP devices in their own VLAN in order to grave an unfair traffic priority for throughput). 

Internet of Things (IoT): the interconnection of computing devices embedded in everyday objects (via the internet) enabling them to send and receive data.

Power over Ethernet (PoE): power and data signals sent through the same Ethernet cable

Storage Area Networks (SANs) have a Maximum Transmission Unit (MTU) of 1500 bytes per Ethernet frame. 

Large amounts of data have to be split up into multiple MTU chunks in order to be sent across the network. 

Jumbo frames are frames with a larger MTU size of 9k. They allow for less frames to be used in order to send the same amount of data. For Jumbo frames to be used/implemented all devices sending/receiving the data have to support it. 

### 802.1Q Trunking

VLAN Trunking (802.1Q) allows physical network interfaces in a computing environment to be shared. 

Example: When a DHCP configured PC boots for the first time it goes through the DORA process to get a DHCP address. The initial DHCP Discover is sent as a broadcast to a port associated with VLAN 10. The switch forwards the traffic to all other ports associated with VLAN 10, which includes the trunk. When traffic is forwarded on the trunk the frame is tagged with the VLAN id, so the receiving switch will know the VLAN the traffic is associated with. 

End devices must be connected to ports that are associated with the correct VLAN. 

Ensure any Switched Virtual Interfaces (SVI) on our Multi-Layer Switch (MLS) are up and available. 

### Spanning Tree Protocol (STP)

When there are multiple connections between switches, then there's a possibility for a Layer 2 loop to occur. 

A Broadcast Storm is an example of a Layer 2 loop: 
- a PC sends a broadcast to Switch 1
- Switch 1 has 2 connections to Switch 2. 
- Switch 1 sends the broadcast to all of its ports, so the traffic is sent to Switch 2.
- Switch 2 sends the broadcast to all of its ports, so the traffic is sent to Switch 1. 
- This traffic gets repeatedly sent from Switch 1 to Switch 2, then back again (i.e. it loops). 

Spanning Tree Protocol (STP) is a behind-the-scenes protocol that looks for parallel connections. If a parallel connection is found, Spanning Tree Protocol (STP) will drop one of the links to prevent Layer 2 loops from occurring. 

Most modern switches use Spanning Tree Protocol (STP). Most commercial switches run Spanning Tree Protocol (STP) by default. 

#### Root Bridge

The Root Bridge is the switch with the lowest value Bridge ID. 

The Root Bridge gets to forward on all ports. 

Spanning Tree devices send Bridge Protocol Data Units (RPDU) to find the switch with the lowest Bridge ID. 

A Switch's priority and Base MAC Address make up the Bridge ID. 

If switches have the same priority value, then the switch with the lower Base MAC Address wins. 

The Losing Switch's job is to identify the best port it should use for forwarding towards the Root.

When a Switch is trying to identify the best possible interface used to go to the root it'll use:
1. the Lowest Cost to the Toot Bridge
2. the Upstream Switch's Bridge ID
3. the Port ID

designated port: a forwarding port that's forwarding away from the root

#### Security

Bridge Protocol Data Unit (BPDU): a Spanning Tree Protocol (STP) data message that describes attributes of a switch port (e.g. MAC address, priority, and cost to reach). 

Hackers can send crafted BPDUs on a Switch port to claim they have a lower Bridge ID than the Root, thereby disrupting the Spanning Tree Protocol (STP). 

Root Guard, BPDU Guard, and BPDU Filter can be implemented as security measures. 

Root Guard: trains the Switch to not change the Root Port. 

BPDU Guard: if a port is sending BDDU traffic that shouldn't be, this will automatically shutdown that port

BPDU Filter: similar to guard, but just doesn't process the requests. 

### Link Aggregation with LACP

When there are multiple connections between two switches, Link Aggregation (LAG) is a way to leverage all the bandwidth without STP blocking links. 

Link Aggregation Group (LAG): grouping multiple links between switches to behave as a single link. On Cisco devices this is called an Ethernet Channel Group. 

Link Aggregation Control Protocol (LACP): the protocol used to implement Link Aggregation Grouping (LAG). 

### Improving Performance

What happens when there isn't enough Bandwidth to support the number of frames/packets being sent in an exact moment?
- By Default the switch will handle frames/packets in a First Come, First Server manner. 
- Quality of Service (QoS) can be setup to give preferential treatment to time-sensitive applications (e.g. VoIP)

The main purpose of Quality of Service (QoS) is to prioritize the traffic that needs the most prioritization in our networks. 

If a PC has an IP phone connected, the PC traffic and IP phone traffic are tagged differently by the switch. 

priority: specialized treatment of traffic
policing: reducing/restricting/stopping traffic
traffic shaping: slowing down traffic

An example of when we'd want to use Traffic Shaping: If Headquarters (HQ) has a 10 Mbps connection, but the site only has a 1 Mbps connection, then we'd want to pace the traffic. 

For Quality of Service (QoS) to work it has to be implemented on ALL devices in the traffic's path. 

Differentiated Services Codepoint (DSCP): a section of the IP Header routers can use to determine priority. 

Power over Ethernet (PoE): the sending of power and data through the same Ethernet cable

PoE Versions
- PoE 802.af
- PoE+ 802.at (can provide more power)
- other proprietary versions

Storage Area Networks (SANs) have a Maximum Transmission Unit (MTU) of 1500 bytes per Ethernet frame. 

Large amounts of data has to be split up into multiple MTU chunks in order to be sent across the network. 

Jumbo frames are frames with a larger MTU size of 9000 bytes (9k). They allow for less frames to be used in order to send the same amount of data. For Jumbo frames to be used/implemented all devices sending/receiving the data have to support it. 

If the Storage Area Provider, Host, and Switch all support Jumbo frames all support Jumbo frames, the it's wise to use them in order to increase throughput. 

---

## WiFi and Wireless

### Wi-Fi Standards

The Institute of Electrical and Electronics Engineers (IEEE) creates the Wi-Fi standards. 

| Shorthand | Wi-Fi Standard | Supported Frequencies | Maximum Theoretical Speeds |
| --- | --- | --- | --- |
| - | 802.11b | 2.4 GHz | 1-11 Mbps |
| - | 802.11a | 5 GHz | 6-54 Mbps |
| - | 802.11g | 2.4 GHz | 6-54 Mbps |
| Wi-Fi 4 | 802.11n | 2.4/5 GHz | 72-600 Mbps |
| Wi-Fi 5 | 802.11ac | 2.4/5 GHz | 3-7 Gbps |
| Wi-Fi 6 | 802.11ax | 2.4/5/6 GHz | 10 Gbps |

Things to take into consideration: 
- support: client devices have to support the technology
- coverage: availability in all spots of the building
- capacity: number of devices connecting

Multi-User (MU) | Multi-In, Multi-Out (MIMO): the technology that allows multiple conversations at the same time from an access point

**channel bonding**: the range of frequencies being used (ex. 20 MHz, 80MHz)

802.11n is the most flexible and compatible Wi-Fi standard for most users and guests who are bringing their own devices onto a corporate network while also delivering good performance

### Wi-Fi Frequencies

Most Common Wi-Fi Frequencies: 2.4 GHz and 5 GHz

**2.4 GHz Center Channels**
*each channel is space 5 MHz apart*

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2.412 | 2.417 | 2.422 | 2.427 | 4.432 | 2.437 | 2.442 | 2.447 | 2.452 | 2.457 | 2.462 | 

If multiple businesses close to each other all use the same channel there will be a degradation of service, because the signals/radio frequencies would collide with each other. 

Businesses can choose which channel and width of frequencies they use.

The standard width is 20 MHz. Therefore, using a center channel of anything other than 1, 6, or 11 is almost guaranteed to bump into someone else's signals. 

The higher a frequency the more the signal will degrade as it passes through physical objects. 

2.4 GHz has better wall penetration than 5 GHz

When setting up a wireless access point (WAP), perform a site survey using a tool like [NetSpot](https://www.netspotapp.com/) to discover what wireless access points and signals are being used around the area. This will provide the information needed to plan which channel and width should be used to avoid a conflict with competing frequencies. 

With 2.4 GHz the 3 non-overlapping channels are intended to be channels 1, 6, and 11 with a 20MHz wide swath. 

### Wi-Fi Topologies

Ad-Hoc: Uses the Wireless Network Adapter of device close to each other to perform communications directly without needing a centralized device to coordinate the sending of signals. 

Examples: Personal Area Networks (PAN), BlueTooth

Wireless Access Points (WAPs) send and receive radio frequencies to support Wi-Fi. 

WAPs are still wired into the network. PCs connect to the WAPs wirelessly. 

Ideally, WAPs are connected to a switch that support PoE. That way only a single cable would need ran to each Access Point. 

Access Point Management

Ensure there are enough access points to provide adequate coverage in the building or campus. 

When using multiple Access Points, ensure they're coordinated to work together. WAPs should coordinate central frequency channels to provide overlapping coverage, but without competition for the exact same frequencies between Access Points. 

5GHz has more central frequencies than 2.4 GHz. 

Access Point Modes

Autonomous: manual configuration of all AP settings: SSID Name, the Wi-Fi standard (e.g. 802.11n), Wireless Frequency (e.g. 2.4 GHz), Channel (e.g. 11), Width (e.g. 20 MHz), Speed/Duplex, and IP Info.

When using Autonomous Mode with multiple access points these settings would have to be manually configured across all APs. 

Lightweight: uses a controller to push out configuration settings to the Access Points. 

Software Defined Networking (SDN): technician configures settings on a controller, then the controller communicates with all of the Access Points, through a logical tunnel between itself and each Access Point, to push those settings out. 

When a user connects to the Access Point their traffic goes through the Access Point and gets forwarded over the tunnel to the controller. The controller makes the traffic decisions. 

Cisco systems refer to this tunnel as a CAPWAP tunnel. 

The controller ensures frequencies in use are compatible and that they don't conflict with each other.

Rogue Access Points are Access Points that aren't being managed by you.

Service Providers typically provide an internet connection using DSL (i.e. over phone lines) or Coax Cable. These signals go to a DSL/Cable Modem which converts the signals to Ethernet. A router performs NAT/PAT translations of IP Addresses. The router connects to a Switch and the Switch connects to the Wireless Access Points (WAP) which provides the signals for the network. 

A Cable Modem, Router, Switch Ports, and a Wireless Access Point can all be integrated into a single box/package. 


Mesh: multiple access points forming a network. The main Access Point repeats the wireless signals to the other Wireless Access Points which act as repeaters. 

Wireless Access Points build this full mesh network between each other using a frequency that's not being used by the data network. 

Every device is logically connected to every other device. 

Since the Access Points are acting as repeaters to pass the signal along instead of having a direct connection to the switch there can be degradation of service. 

### Antenna Types

All Wireless Access Points have at least 1 antenna. 

The antenna used impacts coverage. 

There are 2 Main Types of Antenna: Omnidirectional and Unidirectional. 

Omnidirectional: the signals go in every direction sends signals equally in all distances

Unidirectional: signals are focused in single direction 

ex: HQ wants to extend Wi-Fi to a branch office 100 feet away
Unidirectional signals are able to reach farther than omnidirectional signals. If HQ wanted to extend Wi-Fi to a branch office 100 feet away, then a unidirectional signal, over omnidirectional, would be a good use case. 

Security

Security risks are posed if Wi-Fi signals extend past the building (e.g. to a parking structure where a malicious entity could easily connect). 

To limit security risks: 
- Do a Site Survey to check the range of the Wi-Fi signals
- Make sure omnidirectional antennas aren't to close to the edge of the building. 
- Put antennas as close to the center of the building as possible while still maintaining coverage throughout the building. 

### Authentication and Encryption

Open Authentication: Users are able to see the Wi-Fi network show up when scanning. The user can then select the SSID with no password needed to connect. 

Pre-Shared Key (PSK): Users can still see the SSID in a scan, and select it, but are required to enter a password to connect. 

Neither Open Authentication nor Pre-Shared Key (PSK) are recommended in a corporate network due to security reasons. Even though PSK requires a password, that password could be easily shared. 

802.1x: a standard for network access that passes authentication through a RADIUS server to verify a user's credentials and grant varying levels of network access.

Extensible Authentication Protocol (EAC): Protocol for authenticating a user before allowing them access to a Wi-Fi network. 

Centralizes AAA:
- authentication: who are you?
- authorization: what are you allowed to do?
- accounting: what did you do?

Examples of AAA servers: RADIUS, TACACS

A Microsoft Active Directory Server uses LDAP to authenticate users. 

Evolution of Network Encryption: Wired Equivalent Privacy (WEP), Wi-Fi Protected Access (WPA), WPA2 - Personal / WPA2 - Enterprise, WPA3

In an enterprise network every user needs to be authenticated using the highest Wi-Fi Protected Access encryption method available. 

Summary: 
- use the Wi-Fi standards that meet our needs
- do a site survey to plan and implement proper coverage
- use the best possible encryptions
- use best possible authentication method

### Cellular Technologies

Code-Division Multiple Access (CDMA): a method for taking multiple sessions and encoding them in a specific set of frequencies

The intention of CDMI is to allow multiple people to have have calls happening at the same time. 

Global System for Mobile Communication (GSM): a type of cellular technology that's likely to be most compatible and available when traveling internationally to multiple countries

Cellular Technologies Generations (G stand for generation): 3G, 4G, 5G, 6G, Long Term Evolution (LTE)

Questions to Ask a Vendor: 
- coverage
- traveling
- throughput
- cost

---

## Network Operations

### Operations Overview

Establish the network's baseline (i.e. what "normal" looks like)
- Utilization Factors: CPU, Memory, Network 
- Environmental Factors: Air, Humidity, Power
- Traffic Types (e.g. is it normal for data to be sent to/from other countries)
- Feedback
- Latency

latency: the delay before a transfer of data begins following an instruction for its transfer.

jitter: frequently changing latency, or latency that's too high

Stimulus, Pause, Response (SPR): the more prepared we are, then the shorter the pause for response to a stimulus will be

Set processes and procedures in place to be prepared for stimulus changes. 

### SNMP

Simple Network Management Protocol (SNMP): the protocol used to gather information from networking devices and alert if there's a problem

Agents are installed on our networking devices. The agents wait for an SNMP manager to make a request. 

The SNMP Manager sends a GET request when it wants to get information. 

The SNMP Manager sends a SET request when it wants to modify information. 

The SNMP Manager can request an agent to provide an alert at a specified threshold (e.g. CPU Utilization). 

Agents send TRAP/INFORM notifications to the SNMP manager.

SNMP SETS/GETS use UDP Port 161  

SNMP TRAPS uses UDP Port 162

There are multiple versions of SNMP (ver1, ver2.x, ver3). 

Only version 3 is recommended, because it's the only version that supports username/group authentication and encryption.

Version 2 uses community strings, which are like passwords. However, when using version 2, all information between agents and the manager is transferred over the network in clear text (i.e. doesn't use encryption). This means the community string is also presented in clear text when inspecting packets. 

Management Information Base (MIB): contains the details of the SNMP device with each details assigned an Object ID (OID)

Each vendor uses slightly different MIBs. Make sure MIBs are downloaded directly from the appropriate vendor and ensure the SNMP manager uses the appropriate MID with each device. 

PRTG: a tool used to monitor SNMP traffic

community string: SNMP v2 Security

priv: SNMP v3 Encryption

auth: SNMP v3 Authentication

### Performance Metrics

SNMP periodically polls the network devices for information. 

TRAPS are also sent to alert the SNMP manager when a device metric (e.g. Temperature, CPU Usage, Memory Usage, etc.) exceeds a set appropriate value. 

Jitter: fluctuations in the Round Trip Time (RTT)

Jitter is the enemy of time sensitive applications.

VoIP applications should normally have latency be under 150ms and be a steady connection (i.e. no jitter). 

Measuring

SLA: a built-in Cisco tool used to measure jitter and delay

SLA results can be sent to an SNMP Manager via SNMP.

### Network Device Logs

Security Information and Event Management (SIEM)

Log files are generated to show what a device is doing and can help technicians troubleshoot if there's an issue. 

Most devices generate local log files. 

For networking devices, log files can provide visibility into what traffic is being allowed or denied. 

Devices can also be trained to send their logs to a centralized logging server. 

syslog is an example of a logging server. 

Rather than connecting to multiple individual devices to review logs it's beneficial to aggregate the logging from multiple devices into a centralized location so the log files can be reviewed quicker/easier.

There are multiple levels of logging details, from 0-7, a technician can set. Level 0 only details Emergency/Critical information. Level 7 is the full verbose details. 

The default protocol port used by a syslog server is UDP Port 514. 

### Interface Status

The status, statistics, and errors of an interface can all be reported. 

3 Things for an Interface to be Happy (up, speed, duplex): 
1. An in-use interface should be up. Interfaces are typically down by default. 
2. The interface's speed settings should match the device connected to it. 
	- Speed Examples:  Gigabit (G) 1000 Mbps | Fast Ethernet (F) 100 Mbps | Ethernet (E) 10 Mbps
	- auto-negotiation: a feature on some devices that should automatically set the speed. However, note that auto-negotiation doesn't always do so correctly. In these cases the speed can still be set manually. 
3. The duplex settings should be set correctly. If connecting to a switch, use Full Duplex. 

Errors to Watch Out For: 
- Zero Traffic
	- If there haven't been any packets or frames sent into or out of an interface for over a minutes, that's typically indicative of a problem. 
	- Technicians can create an SNMP Trap to alert them if no packets come through an interface for over 60 seconds. 
	- If zero traffic is detected this is typically a down port or a physical problem / hardware error. 
- Cyclical Redundancy Check (CRC) Errors
	- If CRC errors are detected this typically means there's likely a cable issue between the router and switch that's harming the signal, or the switch could be mangling the frames. 
- Frame Size Errors
	- Giant Frames: frames that are larger than the default of 1500 bytes
	- Runt Frames: frames that are smaller then the possible size (Ethernet frames must be at least a certain size). 
	- Jumbo Frames: 9k size frames. Jumbo frames are allowed as long as every device in their path can accept them. 

### NetFlow

NetFlow is a tool, originally developed by Cisco systems, used to determine a network's baseline, monitor traffic flow, and look for anomalies. 

NetFlow uses a collector on the network with an open port configured to accept NetFlow reports from networking devices. 

The interfaces to collect data from the the direction of traffic to monitor (i.e. inbound or outbound) can be specified. 

This packet data is periodically shipped to the collector. 

NetFlow provides a high-level overview of the packet's contents, without keeping a full copy of the packet. 

Technicians then interface with the collector to review, sort, and graph the data. 

There are multiple versions of NetFlow. The current version is version 9 (v9). 

IPFix is the IETF standardized 'flavor' of Version 9 from Cisco systems.

Using Version 9 of NetFlow allows technicians to be granular about the what content to monitor and the sampling period (e.g. "sample every 1-in-10 packets").

Summary: NetFlow is a tool that can be used to figure out what's running on the network and help identify network traffic flows. NetFlow captures data, but isn't a direct copy of the packets. This high level overview of data is then shipped to a NetFlow collector. The collector collates and graphs the data for technician review. 

### Environmental Controls and Sensors

"An ounce of prevention is worth a pound of cure"

Controls: provide control over a device or environment. 

Sensors: Senses/Detects a property and indicates, records, and/or alerts on that data

Power 
- In most data centers there are two separate power sources routed to a device. 
- An Uninterruptable Power Supply (UPS) should be installed between the power sources and the device to continue providing power in the case of a power disruption or outage. 
- A UPS provides short term power. A generator should also be installed to provide longer term power until the power source is restored. 
- Use a SNMP alert to send a notification if power source fails. 

Temperature
- The Intermediate Distribution Frame (IDF) (i.e. the "wiring closet" where the gear (patch panels/switches) are kept) needs appropriate ventilation and temperature control to prevent overheating. 

Humidity 
- Too much humidity can lead to condensation and moisture on the networking equipment. 
- To little humidity can lead to static electricity 

Flooding
- Water and electronics don't mix.

---

## High Availability

### High Availability and Fault Tolerance Overview

Fault Tolerance: a technique used to implement high availability that's essentially having 2 of something (i.e. if one device fails, then use the other) (e.g. 2 switches, routers, and/or firewalls, etc.)

Load Balancer: a load balancer is connected to multiple servers (that host the same content) and assigned a virtual IP, so when a user requests a site the load balancer connects the user to the appropriate server based on availability or to a server optimized to handle that user's particular browser

NIC Teaming: multiple NIC cards on a device connected to different switches. If a NIC, or switch, fails the device can still connect to the internet

The "Concept of 2" can be applied to default gateways, firewalls, and other networking devices. 

"Concept of 2" applied to Default Gateways: routers using the First Hop Redundancy Protocol (FHRP) to support Default Gateway functionality for the client

"Concept of 2" applied to Firewalls:
- Active/Passive: 1 Firewall handles all the traffic (active), while another Firewall (passive) monitors the first to ensure its still there, and takes over if it doesn't detect it.
- Active/Active: Both firewalls (active/active) handle a portion of the traffic. Both monitor each other and take over full responsibility if one fails. 

A backup site can be setup to go to in the event of a natural disaster.

Types of backup sites: 
- cold site: a facility/building only (i.e. no network equipment setup)
- hot site: a facility setup with all the networking gear and equipment. Minimal amount of downtime to transfer between sites. 
- warm site: a facility/building with some network items configured
- cloud site

### Redundant Default Gateway (FHRP)

First Hop Redundancy Protocol (FHRP): provides a redundant (fault-tolerant) Virtual IP (VIP) as the Default Gateway to the end users. 

Having 2 Routers can provide Fault Tolerance, however both routers can't have the same IP address. 

DHCP hands out a Virtual IP (VIP) as the Default Gateway to connecting devices. 

The VIP will direct to one of the routers as the active device, the other router will be used as a backup. 

A First Hop Redundancy Protocol (FHRP) will use Virtual IPs (VIPs) for the Default Gateway and also typically assign a Virtualized Layer 2 (MAC) Address. 

Examples of First Hop Redundancy Protocols (FHRPs): 
- VRRP - Virtual Router Redundancy Protocol (open standard)
- HSRP - Hot Standby Router Protocol (proprietary to Cisco systems)
- GLBP - Gateway Load Balancing Protocol (developed by Cisco also)

All of these protocols support 2 or more routers than can work together to create a virtualized Default Gateway. 

### FHRP Demonstration

First Hop Redundancy Protocols (FHRPs), like VRRP, are implemented at the Layer 3 Interfaces of networking devices.  

### HA Facilities and Gear

Uninterruptable Power Supply (UPS): a big battery that can kick in if power is lost. Protects against brown-outs. 

Having Multiple Paths (Multi-Path) through the network, and towards the internet, is recommended for High Availability and Fault Tolerance. 

Multiple Paths in a Storage Area Network (SAN):
- Have two network adapters installed on the storage devices to support multi-path
- Implement NIC Teaming: two network adapters installed on hosted SAN appliances.
- RAID: the ability to stripe data over multiple disks, including some parity information.

HVAC

Fire Suppression System: uses a chemical cloud, instead of water sprinklers, to stop the fire (i.e. the chemical reaction causing the fire) without harming the networking equipment/gear

Have a plan if a natural disaster occurs: 
- Disaster Recovery Plan (DRP)
- Business Continuity (BC) 

Sites: 
- hot site: another location that all the networking, infrastructure, and data simultaneously running. 
- cold site: just a physical location with no networking equipment setup. 
- warm site: a location with some, but not all, networking equipment and infrastructure setup
cloud

Recovery Time Objective (RTO): the planned length of time to get back up and running after data or site loss occurs (e.g. 2 days, 2 months, etc..).

Recovery Point Objective (RPO): the objective point to be able to recover to (i.e. "What point do we want to get back to?"). 

### Network Device Backups

Server Backups

Full Backup: backs up everything on a server each time the backup is ran.

Full Backups take a long time to run. 

Incremental Backup: backs up only the data the changed since the previous backup. 

Differential Backup: backs up everything that changed since the last full backup

If Full Backups are taken daily, then the full backup from any day can be restored to. 

If Full Backups are taken once a week, then Incremental Backups are taken the rest of the week,  the Full Backup would need restored, then each incremental backup would need restored in order until the desired recovery day is reached. 

If Full Backups are taken once a week, then Differential Backups are taken the rest of the week, the Full Backup would need restored, then the differential backup of the desired recovery day would need restored. 

Examples: 
- If Full Backups are taken Daily and Thursday's backup needs restored, then restore the Full Backup from Thursday. 
- If Full Backups are taken on Sunday, then Incremental Backups are taken the rest of the week, then restore the Full Backup from Sunday, then the Incremental from Monday, then the Incremental from Tuesday, then the Incremental from Wednesday, then the Incremental from Thursday.
- If Full Backups are taken on Sunday, then Differential backups are taken the rest of the week, then restore the Full Backup from Sunday, then the Differential Backup from Thursday

Snapshots can be taken on Virtual Machine to take an instantaneous "picture" of the entire server's file system at the time the snapshot was taken. When a server is restored to a snapshot it will revert to exactly how it was at the time the snapshot was taken.

The backup process varies based on equipment vendor and the equipment being backed up.

Test backup solutions to verify functionality/reliability.

3-2-1 Rule
- Have 3 copies of the data: 1 on the server (primary) and 2 backups)
- Backups should be on 2 different media types (e.g. NAS, TAPE, etc.)
- Have at least 1 copy of the backup offsite

Buy It Right | Buy It Nice or Buy It Twice | Buy Once, Cry Once - (i.e. get the right gear or you may have to purchase it again later)

When buying network equipment consider the Brand, MTBF, and MTTR

Mean Time Between Failures (MTBF): the estimated time (rated in hours) equipment will work before a failure occurs.

Higher MTBF is more reliable than a lower MTBF.

Mean Time To Repair (MTTR): the approximate time it takes to repair a component.

Lower MTTR is more desirable than a higher MTTR. 

Network Device Configuration Backup
- Most devices on a network (e.g. Firewalls, Routers, Switches, etc.) have some capacity for exporting their configs. 
- If a network devices fails, a new device can be restored from the configuration backup to provide minimal downtown. 
- A Management Station should be configured to extract exported configs from networking devices in an automated manner. The Management Station then builds a report that compares the downloaded configs to a baseline in order to check for drift. 
- drift: a change that wasn't approved or didn't go through change control. 

---

## Security Fundamentals

### Security Vocabulary

C.I.A. - confidentiality, integrity, availability
- confidentiality: only the people who should be able to see or work with the data can see or work with the data
- integrity: ensure the data hasn't been modified, tainted, or mangled by any unauthorized system or entity
- availability: ensure the data is available, that an attacker isn't preventing access

Data needs to be protected in each of it's states (at rest/in storage, in transit, and while it's being processed)

Secure Protocols: SSH/HTTPS/SFTP/SCP/IPSec(on VPN Tunnel)

Integrity is typically implemented using a hashing mechanism. 

When downloading a file from a vendor, run the hash against the locally downloaded file and compare it with the hash value listed on the vendor's site to confirm  the values match. 

High availability and fault tolerance can be achieved using NIC Teaming, Multiple-Paths, Multiple Devices (firewalls, routers, switches), a Load Balancer, RAID, and using FHRP to provide the Default Gateway. 

Vulnerabilities (i.e. Weaknesses)
- User:  a compromised (e.g. Social Engineering, blackmail, trickery) user revealing info or clicking something they shouldn't which leads to a compromise. 
- OS/Application
- Password: Most companies use their emails as login names, so a secure password is essential. Not having a password policy, or having a weak one, can lead to a compromise
- Protocol: a person eavesdropping on data being transferred using an unencrypted protocol (e.g. Telnet, older version of SNMP, etc.) can discover credentials and other comprmizing data. 

Exploit: the method by which a vulnerability is taken advantage of (e.g. phishing email (user exploit), unlimited password attempts (password exploit))

Threat Actor: the person, individual entity, or group of people implementing an exploit

Risk: the chance of an exploit being successful against a vulnerability, the resultant loss, and the amount the loss would be (e.g. cost ($), reputation, fines, etc.) 

Minimize risk by focusing on the critical assets first. If risk is too high, then the company should spend time/effort implementing controls. 

Controls are designed to prevent exploits from being successful.
- Administrative
- Technical/Logical
- Physical  

AAA
- Authentication: who is accessing the system
- Authorization: what an authro8ized use is able to do or access
- Accounting/Auditing

### Zero Trust

Zero Trust: don't trust anything

Specifying Zone (inside, outside, DMZ) allows for policies to be setup specifying what is and isn't allowed between zones (e.g. a device outside the network should never be able to directly access a device from inside the network). 

No level of access should be allowed by default inside a zone. 

To safely facilitate communication inside a network or between zones: 
- Require Secure User Identification
	- Implement MFA and SSO
- Monitor the Devices Being Connected
	- Know what devices are being connected. 
	- Users should not be able to access network items using a personal/home device. 
	- Require 802.1x authentication when plugging a device into a network.
		- supplicant: software behind the scenes that informs the network of the device being connected. This information is then sent to the authenticator. 
		- authenticator: verifies the information from the supplicator by contacting the authentication (AAA) server.
	- Requirements can be site that a device has to meet before being allowed on the network (e.g. latest updates, anti-malware software)
- Monitor and Filter Network Traffic
	- Don't send any traffic that's not encrypted.
	- If unsecure data needs sent, then it should first be placed inside an encrypted VPN tunnel.
	- Use a secure flavor of DNS
- Monitor Allowed Applications
	- Verify installed software is signed, so it can be verified as legitimate. 
	- Host-Based IPS (HIPS) is an extreme software for PCs that takes full control of reads/writes. HIPS is used to create application permit lists and  prevent unapproved software from executing. 
- Categorize and Monitor Data
	- Data needs to be categorized (e.g. sensitive, intellectual property, personal, etc.). 
	- Data needs to be stored within the allowed geographical boundaries defined by your country.
	- Backups needs to be protected and encrypted.

Insider Threat: an authenticated user scanning the network for vulnerabilites

### Control Types

There are 3 Primary Categories of Control Types: Administrative, Physical, and Technical/Logical. 

Administrative
	- Require an employee background check as part of New Hire policy and procedures.
	- Role Separation: separation of duties (e.g. the person who creates a Purchase Order (PO) shouldn't be the same person who makes the payment). 
	- Users should have admin rights. Let users be users and admins be admins. 
	- The "Rule of Least Privilege": only grant enough access for a user to be able to do their job
	- Require mandatory vacations which will require other employees to perform that user's duties, which can shed light on potential fraud. 

Physical 
	- Person Trap: a bottleneck to only admit people into the building one at a time. Person Traps prevent multiple people entering the building using a single badge swipe.
	- Guards
	- Locks
	- Cameras and Motion Sensors

Technical/Logical
	- Create an Access Control List (ACL) (i.e. a list of what each user should have access to). 
	- Filtering - content filtering, website block list, packet filtering, content policies
	- Decryption -  Next-Gen Firewalls should be able to decrypt packets in order to view their payload to ensure the content policy is being upheld, before the packet is sent out to the internet.
	- If guest devices need internet access, then implement a Guest network. 
	- Segment the network into Zones. 
	- Enforce 802.1X authentication. 
	- Use a central AAA server for User Authentication.

### Segmentation

Two devices that have direct access to each other could compromise one another (e.g. if one device is infected with Malware, it could infect the other).

Segmentation separates devices by inserting a technical control between then. 

Network Segmentation: dividing a computer network into smaller parts, with a control mechanism (e.g. router, firewall, switch, etc.) between segments, for the purpose of network performance and security. 

Firewall Zones and VLANs on a Switch are both examples of segmentation. 

Micro-Segmentation: a network security technique used to logically divide the data center into distinct security segments and device controls to deliver services for each segment. 

To control what a device can do as it moves between network segments we need to implement Software Defined Networking (SDN) using a vendor solution that support Micro-Segmentation. 

Example of an Access List for Micro-Segmentation

| Department | Printers | Data Server | Internet Access |
| --- | --- | --- | --- |
| Sales | x |  | x |
| HR | x | x | x |
| Guest |  |  | x |

### Authentication Methods

Authentication (i.e. "Who are you?")

802.1X Authentication should be implemented on switch ports to verify connecting users. Verified users should then be placed in the appropriate VLAN before network access is granted. 

802.1X is an example of Port-Based Authentication. 

802.1X uses three components: a supplicant, authenticator, and authentication server

When a user logs in, software on the PC (e.g.  AnyConnect) should act as a supplicant. The supplicant passes the credentials to authenticator running on the switch. The switch passes the credentials to the Authentication (AAA) Server using a protocol (e.g. RADIUS, TACACS+). If the user is authorized, then the AAA Server authorizes the switch port to allow traffic. 

Active Directory Single-Sign-On (SSO): authenticates the user to the domain when they sign into a computer to reduce the amount of time for a user to access multiple systems. Active Directory (AD) then protects the user's session by encrypting traffic as the user accesses other devices they're authorized to use. 

TACACS+: the protocol commonly used to authenticate administrators in a CISCO environment

If a device doesn't support a supplicant (e.g. printers, etc.), then the Layer 2 (MAC) Address can be specified on the Authentication (AAA) Server and the Switch can use MAC Authentication Bypass (MAB) to pass the the devices Layer 2 (MAC) Address to the Authentication (AAA) Server for verification. 

Extensible Authentication Protocol (EAP) is used as part of the 802.1X authentication process. 

There are multiple flavors of EAP: 
- EAP - Extensible Authentication Protocol
- EAP-FAST - EAP-Flexible Authentication via Secure Tunnel
- PEAP - Protected EAP
- EAP-TLS - EAP-Transport Layer Security (used when connecting with certificates)

3 Categories of Authentication:
- Category 1 - Something the user knows
	- password, SSN/ID, birthday, picture
- Category 2 - Something the user has
	- smart card, digital certificates, one-time passcode/password (OTC/OTP)
- Category 3 - Something the user is
	- biometric scanner (e.g. fingerprint, eye-scanner, etc.)

Single Factor Authentication: authentication using elements from a single Authentication category.

2-Factor Authentication: authentication using element from two different Authentication categories. 

Multifactor Authentication: authentication using elements from 2 or more Authentication categories. 

Follow the "Rule of Least Privilege": only give users the access they need to do their job

The "Rule of Least Privilege" is usually implemented using Role-Based Access Controls (RBAC). 

permission creep: the accumulation of permissions that occurs when a user moves between roles in an organization without unnecessary permissions getting removed.

Audit a user's permissions each time their position changes to prevent permission creep. 

Disable accounts that aren't actively being used. 

### Risk Management

Risk Management
- What vulnerabilities are present?
- What Exploits and Threat Actors could compromise the network?
- What's the like of an attack or exploit being implemented?
- What would be the cost of repair if the system was compromised?

Defense in Depth (i.e. multiple layers of defense/security across the entire network)
	- Implement multiple zones for the network (e.g. inside, outside, DMZ). 
	- Create multiple VLANs to segment the network. 
	- Use Micro-segmentation to control access between PC and resources regardless of where the PC gets plugged in. 

The Authentication (AAA) Server should be running RADIUS, TACACS+, or LDAP. 

Kerberos is used as a security measure in an AD environment to protect the interaction between computers and ensures they're authorized for the resources being accessed. 

Vulnerability, Threat, and Exploit Assessment
	- Have management devices on the network to scan for open ports representing services running on a system that shouldn't be.
	- Keep an inventory of all network devices.
	- A Vulnerability Scanner can query a system regarding it's OS and the applications it's running to determine and list known vulnerabilities. 
	- [Common Vulnerabilities and Exposures (CVE)](https://cve.mitre.org/)): a database of security vulnerabilities

Penetration Testing: authorized hacking with a defined scope for the purpose of located network vulnerabilities and verify the effectiveness of security controls. 

Penetration Testing to best performed by an ethical outside group to prevent bias. 

Honey Pot: network-attached systems intended to mimic likely targets of cyber attacks used to attract, detect, and thereby deflect cybercriminals from hacking into legitimate targets.

Honey Net: a network of honey pot devices designed for the same purpose

Posture Assessment: the assessment of an organizations security status regarding their networks, information, and systems based on information security resources (e.g., people, hardware, software, policies); and the capabilities in place to manage the defense of the organization and respond to threats and vulnerabilities.

Business Risk Assessment: the assessment of an organization's processes, procedures, and vendors

Supply Chain Attack: when one organization relies on a vendor's services/functions and the vendor is compromised providing an attack vector into the organization. 

Security Information and Events Management System (SIEM): takes all the data from security logs and compiles them to provide a single view of current attacks on the network, current events, and a ranking of them in priority from 10 to 1. 

---

## Common Attack Types

### Attack Type Overview

Denial of Service (DoS) Attack: preventing access to a system or causing it to stop operating

Flooding: sending tons of traffic to consume all bandwidth between the server and the internet

Distributed Denial of Service Attack (DDos): using a botnet to perform and DoS attack

zombie: a computer with malware installed to act as part of a botnet. 

Command and Control (C2) Network: the network from which an attacker tells botnet devices what to do 

SYN-FLOOD
- When a user connects to a server a 3-Way TCP Handshake is performed
	- Client sends a SYN request to the server (sync)
	- The Server sends a SYN, ACK response (sync acknowledgement)
	- The Client sends a final ACK response (acknowledgement)
- A SYN-FLOOD attack uses a botnet to flood  SYN requests to the server causing the server to respond with SYN, ACK responses. However, the botnet clients never send the final ACK response back. 
- Ghost: a device that sends a request to a sever without sending an acknowledgement
- Spoofing: lying
- The botnet devices can spoof their source Layer 3 Addresses to prevent the server from knowing where the requests are coming from. 

Man in the Middle (MITM) / On-Path Attack
- A Man in the Middle attack is where an attacker inserts themselves between a client and a server. 
- Example of a Layer 2 MITM Attack: An attacker can intercept an Address Resolution Protocol (ARP) request from a client PC and respond back with a Default Gateway that's different than what's configured on the network. The attacker could set their own PC as the Default Gateway, so that outgoing traffic from the client's PC would be forwarded to the attacker's PC instead. To cover there tracks, they could proceed to forward the traffic to the real Default Gateway. This way they'd have a copy of the traffic, without the client ever knowing there's an issue.  

MAC/ARP Poisoning/Spoofing: manipulation of an ARP cache on a PC

Layer 3 DNS Poisoning
- An attacker returning the wrong IP when a client makes a DNS request.
- They attacker could return an IP of a site that's designed to look like the site the user was intending to access (e.g. Facebook). Then when a user inputs their credentials, they attacker has a copy (i.e. phishing). The site could also be designed to forward the user to the actual website afterwards, so they wouldn't know there was an issue. 

HOSTS File Manipulation
- When a computer performs Domain Name Resolution it doesn't always check the DNS Server, computers will typically check their local cache first. This local cache is the HOSTS file. 
- An attacker can manipulate the HOSTS file to redirect a user to an unintended IP when trying to reach a site (i.e. typically for phishing purposes). 

Rogue DHCP server
- A Rogue DHCP server is a DHCP Server on the network that isn't under the control of administrative/network staff.
- An attacker can perform a DoS attack against a DHCP server to exhaust all the available DHCP Addresses. The could then setup their own DHCP server on the network to hand out IP Addresses, a Default Gateway address, and DNS Server IP. 

Rogue Access Point (AP):  an Access Point that isn't authorized for the network

Evil Twin
- a rogue SSID crafted to look like the corporate SSID.
- If an attacker his a device on-premises and created an Evil Twin, they may also perform a DoS attack to prevent internet access by jamming wireless signals and/or sending a deauthentication message to all wireless clients to force them to re-authenticate/connect to the network. This would lead to a higher chance of user connecting to the wrong/Evil Twin network. Then when they enter their credentials to connect the attacker would have them. 


VLAN Hopping
- An attacker connected to a network VLAN can trick the switch into thinking the port they're connected to is a Trunk port, instead of just an access port. 
- Trunk ports have access to all VLANs the switches Trunk interface has access to. 
- The attacker can then modify an 802.1q header with the appropriate IP Address space for the VLAN they want access to.

Malware: any type of software that's malicious (i.e. not intended for you system and/or exfiltrating information that it shouldn't)

ransomware: malware that encrypts a user's or company's data and holds it for ransom

Password Attack
- Online Password Attacks aren't common, because most systems lock an account after a certain number of failed login attempts.
- It's more common for an attacker to get a hashed database of passwords, dump them to a file, then attack the passwords offline without risk of account lock-out/alert. 
- Offline Attacks: 
	- Brute Force Attack: attempt every combination of characters the password would be starting with 1 character, then 2, etc... 
	- Brute Force Attacks take a long time to complete and are ineffective against long passwords. 
	- Dictionary Attack: compares the passwords with a long list of possible passwords that are commonly used (dictionary). 
	- Rainbow Table: precompiles all the hash values of a dictionary. The dictionary hashes are compared to the hashed database. This method is significantly faster, because the hash values are precompiled.

Social Engineering: tricking users into doing something that's not in their best interest (e.g. revealing info/passwords)

piggybacking: entering a building behind another user

### Botnets

C2: a command and control network  an attacker uses to control bots

zombie: a PC infected with malware to act as part of a botnet

The only way to protect against an infected machine performing as part of a botnet is to have something between the machine and the internet to block its traffic. 

Zero Day Attack: a type of attack that hasn't been seen before

Prevention of our computers from becoming part of a botnet
- Have Limited Rights at the computer level (i.e. Follow the Rule of Least Privilege at the computer level).
- Don't allow users to have root/admin access. Typically, this means a user can't install software. 
- Install Anti-Virus/Anti-Malware software on all computers and keep it up-to-date. 
- Use a Next-Gen Firewall that can decrypt encrypted traffic for inspection to ensure its not malicious or compromising. 
- The firewall should also have help from cloud services to be able to send file to for analysis in a sandbox environment (i.e. safe testing environment), so the software can be inspected to see have it behaves.
- Configure the Next-Gen Firewall to decline/drop traffic from a PC making to an IP known to be part of a C2 or malicious network. 

### DoS and DDoS

Denial of Service (DoS) / Distributed Denial of Service (DDoS): a network attack as an individual (e.g. DoS) or botnet (e.g. DDoS) with the intention of preventing access to a network. 

Flooding is another name for Denial of Service (DoS) Attacks. There are many types of flooding:
- UDP
- TCP
- ICMP
- TCP-SYN-FLOOD

If bandwidth is being flooded, then work with the service provider to limit certain incoming traffic types. Don't arbitrarily configure these limits. Measure first (using a tool like NetFlow), then implement as needed. 

SYN-Cookies
- SYN-Cookies is a technique used to reduce overhead while waiting for the completion of a 3-way TCP handshake.
- When a client sends a TCP-SYN request a network device with SYN-Cookies can be configured to intercept the request. This device sends back the SYN, ACK response with a crafted Layer 4 header that has identifying information. If the device receives a final ACK packet back with the identifying information, it'll pass the traffic through to the network. 
- This prevents flooding attacks from devices sending TCP-SYN requests without responding causing a service issues, because the SYN-Cookie device doesn't have to remember all the devices making requests (i.e. it acts as a proxy). It only has to look for the correct Layer 4 Header in ACK responses. 

It's possible for Flooding/DoS Attacks to come from internally connected devices on the network. This is why implementing a Zero Trust security model is important. 

Link Layer Discovery Protocol (LLDP): advertises which devices are connected at Layer 2, which devices they're connected do, and can be reviewed without having to be physically on-site. 

Cisco Discovery Protocol (CDP): Cisco's version of LLDP. 

CDP Attack:  flooding a device's CDP table

### Malware

Ransomware: malware that encrypts files and requires payment of a ransom amount for the files to be unlocked

Ransomware encrypts a drive and prevents access by authorized users. 

Reconnaissance: malware that causes a device to scan the entire network; sending ping/ARP requests to scan for open ports.

Prevention Methods
1. Software at the Host
	- Anti-Virus/Anti-Malware
	- Host Based Intrusion Prevention Software (HIPS)
2. Decryption
	- Implement a Next-Gen Firewall with decryption features, so it's able to scan encrypted traffic and drop malicious packets. 
3. Anti-X
	- Software on the firewall that looks for malicious files; if a file can't be determined as malicious or not, it can reach out to cloud services to test the file in a sandbox environment. 
4. Procedure
	- Have policies and procedures in place, so users know what to do if a security incident (e.g. clicking on a phishing email) occurs. 

### Wireless Attacks

Service Set Identifier (SSID): wireless network name

Extended Service Set Identifier (ESSID):  an SSID implemented across multiple Access Points

Rogue Access Point (AP): a non-authorized/home device with DHCP Services built-in acting as an Access Point. 

Evil Twin Attack: when an Attacker spoofs a Wireless Access Point, matching an existing ESSID on the network being attacked. The attacker can then hand out a Default Gateway and DNS they control to any connecting clients. 

De-Authentication: Encouraging or forcing clients to disconnect from and existing Access Point (AP). 

### DHCP Attacks

Clients use the DORA Process (Discover, Offer, Request, Acknowledge) to request DHCP information. 

An attacker may exhaust all the available IP Addresses from the DHCP Server by sending a flood of Discover requests. 

The attacker could then configure their own (i.e. rogue) DHCP Server to hand out a Default Gateway and DNS Server that they control. 

DHCP Attack Goals: 
- Exhaust scope/pool of the authorized DHCP server
- Implement a non-authorized DHCP server

### L2 Switching Attacks

ARP Poisoning/Spoofing

Spanning Tree Protocol (STP) Attack
	- Spanning Tree forwards on some ports and blocks on others. 
	- The Spanning Tree Process is to identify the Root Bridge, then identify everything that's not the Root Bridge as Root Ports (Root Ports forward to the Root Bridge). 
	- In a Spanning Tree Protocol (STP) Attack the attacker attempts to identify their device as the Root Bridge. 
	- Prevention: Root Guard is a feature of some networking switches that prevents requests from other devices trying to take over as Root

VLAN Hopping
	- A VLAN Hopping Attack is when an attacker tricks a Switch by converting an Access Port they're connected to into a Trunk Port, thereby allowing the attack access to any of the VLANs on the network.
	- Prevention: Train the switch about ports that should never be 802.1Q Trunks. 

---

## Network Hardening Techniques

### Hardening Overview

Objective: to have every device resistant to attacks and limit vulnerabilities

Setup the Baseline

- Know the components and configuration the networking devices are using (e.g. L2 Switches, L3 Forwarding, Endpoints, Firewall Applications, etc.). 
- A good baseline has all the security features of each networking device enabled, configured, and saved to a configuration. This way the configuration can be easily applied to any newly purchased components. 

Use Secure Protocols and Services
- Only secure versions of network protocols and services should be used (e.g. SFTP instead of FTP, etc.). 

Ensure Backup Gear is Kept Up-To-Date
- All Firmware and Operating Systems (OS) should be kept up-to-date.

Check Data Integrity
- Data Integrity: file hasn't been modified or tainted by an attacker injecting malware
- Check for legitimacy of Vendor Software when downloading. This can be done by checking the hash value of the software and comparing with the expected hash value the Vendor lists.
		- A Vendor will publish their expected hash value for a file. 
		- After downloading software from a Vendor, run the hashing algorithm they used (e.g. MD-5, SHA-256, SHA-1) against the downloaded file. 
		- Ensure the output hash value matches what the hash value the vendor has published. 

Change Equipment Passwords
- The default password for any piece of equipment can be easily looked-up online. Ensure to change the default password for every piece of networking equipment used. 

Follow Vendor Hardening Guides
- Every equipment vendor publishes recommendations for network hardening using their piece of gear. Implement the vendor's recommendations. 

### Hardening Layer 2 Switches

Port Security
- Disable unused ports. 
- Place unused ports into a bogus VLAN (e.g. 999).  Ensure there aren't any services (e.g. DHCP) or routing functions running on the bogus VLAN. 
- Access Port: a switch port the only supports 1 VLAN and won't become a trunk. 
- Configure all end-device (e.g. computers, printers, etc.) ports as Access Ports. 

Spanning Tree Protocol
- Root Guard: specifies which port(s) is the Root Bridge, then prevents any other ports from becoming the Root Bridge. 
- Bridge Protocol Data Unit (BPDU): the language used by devices, using Spanning Tree, to communicate to each other
- BPDU Guard: disables a network port if it detects end devices sending BPDUs over that port.

Disable any service or function not in use.

### Security Rules

Control what traffic is or isn't allowed through a network by: 
- Configuring Access Control Lists to drop traffic using insecure protocols. 
- Configuring Firewall Zones. 
- Start with a Zero Trust security model, then only add rules to allow necessary traffic. 

Access Control Lists (ACL) are processed from top-to-bottom. 

Know the Layer 4 Protocols and Ports for the type of traffic we want to allow (e.g. HTTPS TCP:443) or block (e.g. Telnet TCP:23): 

| Application Layer Service | Layer 4 Protocol & Port |
| --- | --- |
| Telnet | TCP: 23 |
| FTP | TCP: 21 |
| HTTP | TCP: 80 |
| HTTPS | TCP: 443 |

### Port Security

MAC Flooding / CAM Table Overflow Attack
- Switches memorize the MAC Addresses of the devices plugged into each port.
- These MAC Addresses are placed into a MAC Address Table on the Switch. 
- When Switches are making Layer 2 Forwarding decisions for incoming frames, it'll first compare them to the MAC Address Table. 
- Switches have a limited amount of memory to store this information. 
- A malicious device can constantly send frames with a spoofed source MAC Address in order to consume all of the allocated memory on the Switch. 
- If all of the memory of the MAC Address Table is consume with bogus information, then when a real frame comes in the Switch won't know where to forward the frame to. 
- When a Switch doesn't know where to send a frame, it forwards it to all the other ports on the switch. 
- The attacker can then intercept that data by eavesdropping on any of the Switch ports. 

Port Security is a feature on most Layer 2 Switches that can: 
- limit the number of MAC Addresses learned on each port
- give exclusive use of a port to a specific MAC Address
- shutdown (i.e. disable) the network port or restrict (i.e. drop) traffic from a port where a violation is detected (e.g. traffic from multiple MAC addresses on a port)

### DHCP Snooping

Rogue DHCP Server: a DHCP Server on the network that isn't under the control of administrative/network staff.

Rogue DHCP Servers aren't always malicious. Users may be bringing home equipment w/o realizing DHCP Services are enabled.

DHCP Snooping is a Switch feature that: 
- Protects against Rogue DHCP Servers by blocking DHCP Server Responses an all but specified DHCP trusted ports (i.e. the ports where the trusted DHCP Servers configured for the network are located). 
- Builds a table of Layer 3 - to - Layer 2 mappings regarding DHCP Clients

### Dynamic ARP Inspection

Hackers can use ARP Spoofing to convince a client that their Default Gateway is different than what's configured on the network. 

Dynamic ARP Inspection prevents ARP spoofing by training the switch to drop ARP traffic coming from any ports other than the configured trusted ARP ports. 

Dynamic ARP Inspection (DAI) prevents poisoning of VLAN devices with bogus Layer 2 information, by utilizing a DHCP Snooping table to know which IP addresses are associated with Layer 2 MAC Addresses. 

If the Switch hasn't learned the Layer 3 - to - Layer 2 mappings for a device, then that devices traffic would also be blocked, even if its a legitimate device.

### Wireless and IoT

Wireless LAN Controller (WLC): manages multiple Access Points to implement a wireless network with overlapping coverage, but without interfering frequencies by automatically configuring the center channels and frequencies for each Access Point to use. 

Extensible Authentication Protocol (EAP): a protocol used to validate a connection to ensure a device doesn't connect to a rogue network. 

WPA-3 Enterprise or WPA-2 Enterprise security protocols should be implemented for network security because these protocols: 
- require use of a centralized AAA (Authentication) Server
- doesn't allow a Pre-Shared Key (PSK) of the only mechanism for connection

If hosting a "Guest" network, ensure it's separated from the rest of the network (i.e. on a separate VLAN and subnet) and leverage a captive portal. 

Captive Portal: a webpage that users of a Guest (i.e. public) network are required to interact with (i.e. enter contact information, accept Terms of Use agreement) before they can access the network.

MAC Filtering: a network feature that only allows traffic from specific specified MAC Addresses 

Strategically place Wireless Access Points (WAPs) to provide the necessary coverage for the building while also limiting access outside the building (e.g. parking lot). 

Signal strength can be reduced on an Access Point to limit the area of coverage. 

Faraday Cage: stops any emanating signals from passing through.

Geo-Fencing: only allows the device to work within a certain geographical area

Internet of Things (IoT) Devices
- Implement a separate subnet and VLAN for IoT devices. 
- Place IoT devices behind a Next-Generation Firewall that can perform decryption to inspect and filter traffic. 

---

## Remote Access

### Remote Access Overview

Options for Remote Access: 
- Command Line Interface (CLI)
- Browser-Based Services/Management-Console
- Remote Desktop

Who Uses Remote Access:
- End-Users (i.e. the "customers of the network")
	- Data Plane Traffic: user-based network traffic	
	 - Users should only have access related to business functions (i.e. the use of a computer, company software, and printers). 
	 - Users shouldn't have access to infrastructure devices (e.g. switches, firewalls)
 - Administrators
	 - Management Plane Traffic: all traffic used to manage the network
	 - Examples: SNMP, SSH, Browser, Remote Desktop

Security
- Require authentication. 
- Use secure protocols for remote connections (e.g. SSH for CLI Access, HTTPS for Browser-Based Access, Secure Flavor/Implementation of the Remote Desktop Protocol for Remote Desktop Access). 
- Direct connection between remote client and  workstation shouldn't be allowed. Route the traffic to a Firewall or Remote Detection Gateway (RDG) first.   
- Leverage VPNs
	- Virtual Private Network (VPN): a secure connection using encryption over a public network. 
	- site-to-site: traffic between sites
	- client-to-site/remote-access: traffic between a remote user and a site

Rather than connecting to each network device individually, setup a terminal server to connect to that has all the connections to each of the managed devices. 

Some routers have special ports that can be used to gain access when all effective connectivity has been lost: 
- Console Port: a port that can be directly connected to, using a serial cable, to get CLI access.
- Auxiliary Port: the aux port can be connected to a modem. The modem connects to a Public Switched Telephone Network Cloud (PSTN), which grants it a telephone number. Therefore, if all Ethernet connectivity has been lost, then the phone number of the modem can be dialed via the PSTN to gain access to the device. 

In-Band Management: the use of the same subnet and VLANs for both Data Plane and Management Plane traffic. 

Don't use In-Band Management as it's susceptible to Man in the Middle (MITM) attacks. 

Out-of-Band (OOB) Management: the use of a separate subnet and VLAN for Data Plane and Management Plane traffic. 

Examples of Out-of-Band (OOB) Management: 
- Modem connected to the PSTN and the aux port on a router
- Management network in a dedicated VLAN and subnet

### Remote Access VPNs

Virtual Private Network (VPN): a secure connection using encryption over a public network. 

VPNs are a way for users to access work resources from outside the network. 

Client-to-Site (i.e. Remote Access): traffic between a remote user and a site

Recipe for Client-to-Site VPN Access: 
- Head End Device: a firewall or dedicated VPN device
- VPN software on the client's PC
- Implement IPsec, or some flavor of SSL (TLS), to secure and encrypt the VPN Tunnel
- Require Multi-Factor Authentication (MFA)

Full Tunnel: encrypts all packets that leave a client PC, passes them through the VPN tunnel to the Firewall for decryption

"All" is the keyword. Regardless of whether the traffic is meant for Work Resources, or the public internet it's all passed through the VPN tunnel. If a request is for a public website, the traffic is passed through the VPN tunnel to the Firewall, which makes the web requests, then sends the results back through the tunnel to the PC. 

Split Tunneling: allows a client to have simultaneous direct access to the corporate network using the VPN and access to the public internet. 

Split Tunneling uses a list of traffic that defines what should be filtered through the VPN or sent to the public internet. 

There are similar concepts of tunneling regarding DNS resolution. 

For a remote user to access work resources: 
- Go to the IP Address of the Company Portal in their browser. 
- Authenticate, then download the VPN software. 
- The software builds the VPN tunnel to a configured Firewall that acts as a Head-End Server.
- Once the connection is established, the details of Split Tunneling, DNS, and IP Addresses for the Virtual Connection are negotiated, established, and pushed out to the remote user's PC. 

### Site to Site VPN

Site-to-Site: traffic between sites

A Site-to-Site VPN builds a tunnel between a remote site and headquarters. 

Recipe for Site-to-Site (S2S) VPN Access
- Requires a VPN Device at each end of the tunnel that has a reachable IP address and IP connectivity.  
- S2S VPNs almost always use IPsec (a suite of protocols used to protect packets between sites); SSL/TLS encryption in S2S tunnels is rare
- IKE (Internet Key Exchange) v1/v2: a way of dynamically negotiating and setting up a tunnel and keys

IKE (Internet Key Exchange) is the Tunnel built using the Diffie-Hellman Key Exchange. 

Diffie-Hellman: a way for routers to establish a shared secret key that encrypts/decrypts communication between the routers. 

Diffie and Hellman are the last names of the two developers who created the Diffie-Hellman Key Exchange.

IKE (Internet Key Exchange) v1/v2 has 2 major parts: 
1. Initialize secure communication between the routers at each site. 
	- this initial step establishes an IKE-SA (Internet Key Exchange, Security Association) for Control Plane traffic between the two routers. 
2. Build an IPsec Security Association (SA) (i.e. a tunnel) between the sites.
	- The IPsec Security Association (SA) (i.e. a tunnel) allows for Data-Plane (i.e. User) traffic. 

HAGLE is an acronym that details the negation steps the site routers do to setup communication

H: Hashing - What type of hashing algorithm should be used for data integrity?
A: Authentication - What authentication method (e.g. Pre-Shared Key (PSK), digital certificate, etc.) should be used? 
G: Diffie-Hellman Group - What flavor of Diffie-Hellman should be used?
L: Lifetime - How long should the tunnel exist?
E: Encryption - What type of Encryption should be used? 

Firewalls using pre-shared keys (PSKs) for Site-to-Site VPN tunnels should schedule a periodic change of the PSKs at both ends of the tunnel.  

### Site to Site Interesting Traffic

When a packet comes into a router, that's one end of a site-to-site VPN tunnel, the router has to decide whether to encrypt the packet or to forward it without encryption.

Interesting Traffic: traffic that should be encrypted and sent through the tunnel (i.e. is interesting enough for the router to decide to encrypt it).

Options for Implementation:
1. Create a traditional IPsec tunnel that defines traffic between two specified IPs as Interesting Traffic. 
2. Create a GRE Tunnel that an IP Address can be logically associated with. 

There isn't a logical connection between routers when using a list. They have an internet connection, but because they aren't logically connected, they can't use an Interior Gateway Routing Protocol (e.g. OSPF, EIGRP, RIP), or any other routing protocol that requires them to be logically next to each other

IPsec, with a list, isn't enough to perform Dynamic Routing. 

Having a GRE Tunnel logically associates both routers on the same network. This allows for the use of routing protocols (e.g. OSPF, EIGRP, RIP). 

### Remote Desktop

A Remote Desktop session allows a remote user to connect to a device (physical or virtual) as if they were sitting at that device (i.e. display, mouse, and keyboard control). 

Virtualized Desktop Infrastructure (VDI): a common app for Remote Desktop usage that creates multiple VMs for a remote user to connect to. 

VDI allows for centralized management of VMs instead of manually installing/updating software on individual user PCs. 

VDI is supported by multiple vendors (e.g. VMware, Citrix). 

Windows Remote Desktop
- a Remote Desktop Application/Platform developed by Microsoft and used on Windows computers. 
- Remote Desktop Protocol (RDP)
- Remote Desktop Connection (RDC)
- The default server port for Microsoft RDP is TCP: 3389

Remote Desktop Gateway (RDG): a device in-between a client and a remote system

Virtual Network Computer (VNC): another option for Remote Access

Security
- Train users. Attackers use Social Engineering to attempt to convince users to enable Remote Access. Once an attacker is granted access they have full control over the workstation. 
- Remote Desktop session should require Authentication to connect and Encryption during the connection. 

### CLI Access via SSH

Command Line Interface (CLI) Access Options: 
- Use a Console Cable (i.e. a serial or USB cable) to plug directly into the Console Port of the device. 
- Configure the network device to accept in-bound SSH connections. 

Avoid using Telnet! Telnet doesn't have encryption. 

Secure Shell (SSH) Access protects traffic by using a key-pair to lock and unlock data sent between clients and devices.

Key-Pair: keys that are mathematically linked together so when we encrypt with one we can decrypt with the other

Public Key: key that's shared with the world (i.e. public)

Private Key: key that's not shared with anyone (i.e. private)

RSA is a cryptosystem used to generate key pairs. It's name comes from the first initial of each developer of this asymmetrical algorithm. 

Secure Shell (SSH) traffic uses TCP port 22. 

Software used for Terminal Emulation Services (i.e. SSH Connections): Putty, SecureCRT, MobaXterm

Access to an SSH server can be further secured by restricting access using passwords, known/trusted hosts, or through Access Control Lists (ACLs). 

---

## Physical Security Controls

### Controls Overview

Controls are placed to detect and protect against bad things from happening to the network. 

Purpose of Controls:
- Preventative - prevent something from happening (e.g. door lock)
- Compensating - compensate for a known, but yet-to-be-patched vulnerability
- Detective - detect if something bad or suspicious is happening (e.g. vehicles in parking lot after hours, door alarms)

Control Types
- Administrative
	- Examples: mandatory vacations, separation of duties, background checks
- Technical/Logical
	- Examples: Access Control Lists (ACL), Security Policies, 802.1X Authentication, DHCP Snooping, ARP Inspection
- Physical
	- Example: Locks, Fences, Motion Sensors, Security Guards, Mantraps

Tailgating: sneaking into a restricted area without the knowledge of the person providing access

Piggybacking: when an authorized user lets another person into a restricted area assuming they have a legitimate reason for being there. 

Mantrap / Access-Control-Vestibule: a room connecting two parts of a building that locks after entry and requires authentication to passthrough. 

Mantraps are designed to eliminate piggybacking and tailgating. 

Some mantraps also have weight sensors that can detect the presence of multiple people, or can alert if a user is leaving with more weight than they came in with. 

Install locks on Computers to prevent tampering and component theft. 

### Detective Physical Controls

Detective Controls: controls that alert when something has, or is happening, regarding a change in the environment. 

Security Cameras needs to be monitored, either by a security team or automated alerting system, in order to be effective. 

Motion Sensors alert when motion is detected in an area. 

Environment Sensors alert if there's been a change in the environment (e.g. temperature, humidity). 

Asset Tag: a device label

Digital Asset Tags also exist that have location tracking. Digital Asset Tags can be set to alert if a device leaves a Geo-Fencing Area. 

Tamper Detection:  seals that irreversibly change when removed (e.g. when a computer case is opened).

### Preventive Controls

*"an ounce of prevention is worth a pound of cure"*

Technical/Logical
- Install Anti-Virus/Anti-Malware software on Computers and Host Based Intrusion Prevention Software (HIPS) on Hosts. 
- Keep software (e.g. Firmware, Operating System) up to date. 
- Implement Change Control before installing updates (i.e. identify what an update fixes, how quick it needs deployed, and get approval before install). 
- Disable all unused services (i.e. System Hardening). 
- Implement Access Control Lists (ACLs) (i.e. who can do what with what). 
- Implement the Concept of Least Privilege. 
- Utilize Encryption
- Configure Intrusion Prevention Systems (IPS) and Intrusion Detection Systems (IDS). 
- Implement Email Security (i.e. use spam blockers, use secure protocols, and scan messages for phishing links). 
- Require Multi-Factor Authentication (MFA). 

Physical
- Examples: Locks, Badge Readers, Biometric Scanners (e.g. fingerprint scanners, retina scanners), Lockers / Smart-Lockers, USB Locks. 

A USB Lock is a Physical Control, that prevents users from attaching a flash drive to their computer. 

End-User Training
- Users are the weakest link of any security plan, therefore End-User Training is the most important aspect regarding security. 
- Users should be required to sign an Acceptable Use Policy (AUP) Agreement that details what is and isn't acceptable when they use their computers. 
- Users should be trained on what to look out for regarding security threats (i.e. Security Awareness) and what to do in case they've been compromised or have fallen victim to a security threat (e.g. Phishing email). 
- Test users on what they've been trained to do. 

### Asset Disposal

Data should be permanently deleted from our systems based on the company's **Retention Policy**.

Assets should be properly disposed of by following the company's **Disposal Policy**. 

| Media | Disposal Method |
| --- | --- |
| Paper (e.g. company secrets, tax returns, customer data) | Mulch, Shred, Burn |
| Drives (Flash, HDD, SSD) | Physical Destruction, Wipe |
| CD/DVD | Physical Destruction, Microwave |
| Cloud Data | Service Provider Involvement |

Most disposal options are physical in nature. 

Wiping a drive rewrites every bit of storage multiple times. 

Backups should follow the 3-2-1 Police: Have *three* copies of the data (1 in production and 2 backups) storage on *two* different media types and have at least *one* backup offsite. 

Digitally remove any backups that are past the company's Retention Policy. 

Regarding Cloud Backups, ensure the cloud provider used for cloud backups has the ability to permanently dispose of the data that should no longer be kept. 

Keywords for getting rid of data: sanitize, wipe, remote wipe for lost/stolen devices, encryption

### Organizational Documents and Policies

Plans & Procedures
- Change Control - Have a Procedure in place to ensure any changes won't cause harm to the network and to document any changes made. Change Control should include a section for reviewing and updating documentation. 
- Incident Response Plan
- Disaster Recovery Plan (BCP) - Identify processes critical for running the business, with details for how to keep the business running in the event of a disaster. 
- Standard Operating Procedures (SOP) - Procedures to follow that will help with compliance

Policies
- Data Loss Prevention (DLP) Policy - Detail what types of control methods are implemented on the network to prevent the loss and exfiltration of data. Its purpose is the prevention of sensitive data from being leaked out. 
- Password Policy - Detail password requirements (e.g. must be at least 8 characters, with upper and lowercase letters) and password manager (e.g. LastPass) policies. 
- Bring Your Own Device (BYOD) Policy - Details the rules for connecting user owned equipment. 
- Remote Access Policy
- Data Retention Policy
- Asset Disposal Policy
- On-Boarding and Off-Boarding Policies for Users and Devices. 

Common Documents
- Diagrams of Physical Locations (i.e. server racks, Intermediate Distribution Frames (IDF) (i.e. wiring closets), Main Distribution Frames (MDF)), Demarcation Point (Demarc)). 
- Logical Diagrams (i.e. representations of the network layout). 
- Wiring and Device Labels
- Wireless Site Surveys
- Baseline Configurations

Agreements
- Acceptable Use Policy (AUP) - A User Agreement that indicates what is and isn't allowed on the network (i.e. what is expected of users). 
- Non-Disclosure Agreement (NDA) - An Agreement regarding sensitive data. 
- Service Level Agreement (SLA) - An Agreement with a service provider regarding expectations. 
- Memorandum of Understanding (MOU)

---

## Troubleshooting Methodology

### Troubleshooting Overview

1. Identify the Problem
2. Establish a Theory of Probable Cause
3. Test the Theory
4. Solve the Problem
5. Document What Was Done

### Identify the Problem

4-Step Strategy for Problem Solving: 
1. What is the problem?
2. Why did the problem happen?
3. What are the Possible Solutions?
4. Pick a Solution to test. 
- Repeat as needed. 

Gather Information (e.g. Who are the affected users?, What computers are affected?, When did the issue start occurring?)

Be Kind when questioning and working with users. 

Use terms the users can understand. 

Determine if there have been any recent changes. 

Identify the Symptoms of the Issue. 

Symptoms must be measurable and/or observable. 

Replicate the Problem. 

Replicating the problem is a step in identifying the problem that can assist in confirming what the problem is. 

If there are multiple parts to an issue, then troubleshoot each part individually. 

### Establish a Theory

Approaches
- Bottom-to-Top Approach
	- Regarding networking issues, work from the bottom of the protocol stack (i.e. the Physical Layer), then up. Example: Is the Ethernet cable plugged in?, Is Wi-Fi Connected?
- Top-to-Bottom Approach
	- Regarding networking issues, work from the top of the protocol stack (i.e. the Application Layer), then down. Testing DNS first is an example of a top-to-bottom approach. Example: Does a website load?
- Divide-and-Conquer Approach
	- Regarding networking issues, work from the middle of the protocol stack, then out from there (i.e. either down or up as needed). Example: Can an IP Address be pinged (e.g. `ping 8.8.8.8`)?

Question the Obvious (e.g. Is the device powered on?)

### Test and Determine Cause

Test the Theory in order to Validate that what is thought to be the issue is the actual issue. 

If the initial Theory is confirmed, then proceed with Solving the Problem. 

If the initial Theory is not confirmed, then establish a new theory of what may be wrong (or escalate if you are stuck).

### Solve the Problem

Create a Plan for Resolution. 

Pass the Plan through Change Control. 
- Any Configuration Changes should go through the Change Control process.
- Change Control puts additional eyes on the recommended resolution to help prevent against unintentional issues from occurring by implementing a change. 
- As part of Change Control get authorization to make the change and have an way to rollback any changes if additional issues occur. 

Implement the Solution

Verify the Solution Resolves the Issue. 

When verifying the solution, repeat the original tests first before performing additional tests to reduce variables. For example: If the original test was to attempt to load google.com, makes sure google.com loads to verify the solution rather than another site (e.g. yahoo.com). 

Document the Solution. 

### Troubleshooting Review

Identify the Problem

Establish a Theory of Probable Cause

Test the Theory

Create a Plan of Resolution

Verify the Implemented Plan Resolved the Issue

Document What Was Done

---

## Working with Network Media

### Network Media Overview

#### Copper Cables

Ethernet Cables are mostly Unshielded Twisted Pair (UTP) Copper Cables with RJ-45 Terminations (i.e. Jacks). 

Patch Cables (i.e. Straight-Through Cables) have all pins lined up at both ends. 

Cross-Over Cables have pin 1 swapped with 3 and pin 2 swapped with 6. 

Straight-Through Cables are used to connect different devices (e.g. PC to Switch). 

Cross-Over Cables are used to connect like devices (e.g. Switch to Switch). 

Cross-Over Adapter: an adapter used to convert a Straight-Through Cable into a Cross-Over Cable. 

Auto-MDIX: a feature of some networking devices to detect Send/Receive signals and allow traffic to still be sent correctly even if the wrong cable is connected (e.g. a Straight-Through Cable connecting like devices). 

Even if a networking device support Auto-MDIX, it's still best practice to use the correct cable type. 

Console Cable have all pin completely flipped (i.e. pin 1 connects to pin 8). 

Console Cables are used to connect a PC to a network devices' Console Port. 

The maximum length of an Ethernet Cable run is 100 meters. 

#### Fiber Optics

Fiber Optic Cables use light to transmit data. 

Fiber Optic Cables are able to span longer runs than Ethernet Cables. 

Multi-Mode Fiber Optic Cable is intended for shorter distances. 

Single-Mode Fiber Optic Cable covers longer distances. 

Fiber Optic Cables come as a pair of two cables connected together. One Cable receives at one end and transmits at the other. The other cable does the opposite. 

There are multiple terminators (i.e. connectors) for Fiber Optic cable. Use the adapter (i.e. transceiver) (e.g. SFP) appropriate based on the media type and gear being used. 

#### Wireless

Wi-Fi uses the 2.4 GHz and 5 GHz frequency ranges. 

A Network Analyzer is used to check the ranges of in-use frequencies. 

Services Set Identifier (SSID): the name or a Wi-Fi network

A controller is used to configure multiple access points with an Extended Services Set Identifier (ESSID). "Extended" denotes the Wi-Fi network name is configured on multiple access points. 

When configuring Wi-Fi networks across multiple access points aim for overlapping coverage without fighting over in-use frequencies. 

### Choosing Copper Cables

Straight-Through Cable: an Ethernet cable used to connect different devices (e.g. PC to Switch).

Cross-Over Cable: an Ethernet cable used to connect like devices (e.g. Switch to Switch). 

Plenum-Rated Cables should be used when running cables in a plenum space (i.e. the space between a drop ceiling and the physical ceiling). Plenum space can also be used for air flow. Plenum-Rated Cabling is an important safety measure in these areas, because it's less toxic (i.e. releases less harmful vapors) when burning. 

There are two standards for terminating RJ-45 Cables: 568A and 568B

A Straight-Through Cable uses the same termination at both ends. 

A Cross-Over Cable uses a different termination at each end. 

Power over Ethernet (PoE) Cables deliver power in addition to data signals. 

When wiring Access Points, PoE cables can be useful so only a single cable has to be ran to each Access Point. 

There are different versions of PoE Cables. Ensure the correct cable version is used based on what the Switches support and the power consumption needs of the networking device (e.g. Access Point). 

Keep Ethernet Cable runs less than the maximum run of 100 meters. 

Even if the networking gear being used can compensate for the wrong cable type being attached (i.e. the device has the Auto-MDIX feature), follow best practice and use the correct cable type (e.g. Straight-Through, Cross-Over). 

| Cable Type | Appropriate Use |
| --- | --- |
| Power Cable | from AC outlet to computer |
| Straight through cable | Between a PC and a switch |
| Rollover cable | between a PC and console port |
| Plenum rated cable | For a cable that will be in an airway |
| Cross over cable | Between like devices |

### Tools for Copper Cables

multimeter: a tool used to measure two or more electrical values (i.e. voltage (volts), current (amps), resistance (ohms)).

A multimeter can be used to measure Direct Current (DC), continuity (i.e. flow between one end of a wire and the other), and resistance. 

cable tester: a tool used to verify cable runs

One end of a cable tester is plugged into an RJ-45 slot, the other end is plugged into a meter. The cable tester can then verify if the cable run is good, test if there's an open (e.g. pin 1 not connecting to pin 1), test for miss-wirings (e.g. ping 1 connecting to pin 4), and measure the cable length. 

If a cable run isn't verified, then snip off the cable end and re-terminate with another RJ-45 connectors. 

snips, cutters, and cable strippers are all tools used to cut and strip cables. 

crimper: a tool used to crimp an RJ-45 jack to an Ethernet Cable to secure the connection

punch-down tool: a tool used to punch-down cables into a patch panel or jack

A punch down tool is used to connect the individual wires in a UTP cable to an RJ-45 jack in a patch panel. 

tone generator: a tool consisting of a device that plugs into a network jack and a probe that will generate a tone when held up to the wire that connected to the jack. 

### Copper Cable Concerns

When implementing Cable plans its worth it to hire a company to perform the installation, that has the tools to complete the installation, documents the installation with a cable map, and can certify their work. 

Interference
- Generators or Fluorescent Lighting can introduce interference. 
- Since UTP Cabling is unshielded, any electromagnetic interference nearby would influence the cable's signals, thereby degrading or interrupting service for any connected devices. 
- A gas powered electric generator is most likely to cause interference with UTP if it is too close. 
- There are four pairs in a UTP cable. Each pair has a specific number of twists per foot. The twists help to reduce cross talk between the cable pairs. 
- A flat cable would be more susceptible to interference and cross talk. 
- Always use the correct category, or better, standard of cable in a production environment to help protect against interference. 

Physical Damage (e.g. cable rolled over with chair, tripping hazard)

Attenuation: the reduction of the amplitude of a signal, electric current, or other oscillation.
	- When a signal is sent across a distance (via airwaves or wire) the signal will degrade, because it loses energy as it travels.
	- This is why an Ethernet cable run shouldn't exceed 100 meters. 

Opens/Shorts

Incorrect Pin-Outs
	- The pins of a Straight-Through Cable should line up at each end (i.e. 1-1, 2-2, ... 8-8). 
	- The pins of a Cross-Over Cable should line up, except pin 1 -> 3 and pin 2 -> 6. 

Cyclical Redundancy Check (CRC) errors on router could indicate a cabling issue. 

### Fiber Optic Cabling

Fiber Optic cabling can be ran longer distances than Ethernet, because it isn't affected by Electromagnetic Interference (EMI).

Checklist for a Successful Fiber Optic Cabling Installation: 
- Ensure the networking gear in use support Fiber Optic. 
- Ensure the appropriate Small Form Pluggable (SFP) / Transceiver is used based  on the networking gear and Fiber Optic cabling in use. The SFP must accept the termination type of the Fiber Cabling. 
- Ensure the Terminators (i.e. the ends of the Fiber Optic Cable) are clean. The connectors should be kept covered when not in use. 
- Ensure the pairs of the Fiber Optic cables are lines up correctly. Transmit (TX) on one side should line up with receive (RX) on the other side and vice-versa. 
- When purchasing Fiber Optic cables, factor in the bend radius (i.e. the amount a Fiber Optic cable can be bent before becoming damaged). 

Fiber Optic Tools
- fiber optic meter: a tool used to measure light being sent through a Fiber Optic Cable
- fusion splicer: a tool used to fuse Fiber Optic Cable together; can be used to repair cuts. 
- Optical Time Domain Reflectometer (OTDR):  a tool that can help identify a problem with a fiber cable, including where a problem is located on that cable

### Wireless Media

802.11 Wireless Standards

| IEEE Standard | Frequency | Maximum Data Rate |
| --- | --- | --- | 
| 802.11 | 2.4GHz RF | 2 Mbps |
| 802.11a | 5GHz | 54 Mbps |
| 802.11b | 2.4GHz | 11 Mbps |
| 802.11g | 2.4GHz | 54 Mbps |
| 802.11n | 2.4GHz/5GHz | 600 Mbps |
| 802.11ac | 5GHz | 6.9 Gbps |
| 802.11ax | 2.4GHz/5GHz | 9.6 Gbps |

Layer 2 Switching uses a pair of wires for sending and a pair for receiving. Having both pairs allows Layer 2 Switching to operate in Full Duplex. 

Wi-Fi operates in Half Duplex (i.e. only 1 device can send on a given set of frequencies at a time). 

Multi-User Multi-In Multi-Out (MU-MIMO): uses more frequencies with the goal of more throughput for more users operating simultaneously. 

A Wireless Controller is used to manage multiple access points. The details of the wireless network are input into the controller. The controller then implements these details across the network. 

attenuation: the reduction of the force, effect, or value of something. 

Attenuation occurs with Wireless Signals (i.e. the signals get weaker the longer they travel). 

Attenuation, in regards to Wireless Signals, is measured as Decibel Loss (dB). 

Note: a signal with a dB loss of -44 is stronger than a signal with a dB loss of -85. 

The Power to an Access Point (AP) can be adjusted to affect the range of the Wi-Fi signal. 

To prevent a Wi-Fi signal from extending past the building, the power to the Access Point(s) can be reduced. 

A Site Survey can be performed by a  3rd Party Company to identify the best location(s) for Wireless Access Points to be placed.

Tools like [NetSpot](https://www.netspotapp.com/) can show competing wireless frequencies. 

A Spectrum Analyzer identifies all competing frequencies in the 2.4 GHz and 5 GHz ranges, not just other Wi-Fi signals.

### Network Cards and Interfaces

What could go wrong?
- Wireless Network uses a standard not supported by the computer. 
- AP isn't close enough for usable signals. 
- NIC could be disabled in the computer settings. 
- Static IP doesn't match what's configured on the network. 
- Access Port of the Switch isn't configured as Full Duplex. 
- Port Security is enabled, but the Layer 2 Address isn't allowed. 
- Bad NIC
- Misconfiguration of networking devices. 

To test a computer's NIC, you can disabled the Built-In NIC, then use a USB-Ethernet adapter and test for a signal. 

Switches have LEDs to indicate the status of: Duplex, Forward/Blocking, System States, Link. 

LED indicators could be used to verify duplex or speed on a switch port, without having to log on to that switch. 

Loopback Adapter: a devices that physical plugs into an interface/port to test the interfaces status by taking traffic being send and sending it back. 

Loopback Contexts: 
- *Physical Loopback*: plugging into ports for local testing
- *Loopback Address Space*: IPv4 and IPv6 logical loop back address. 
	- Note: IPv4 Loopback addresses start with 127.____
- *Loopback Interface*: a logical (not physical) component that an IP Address can be assigned to. 

Example of how a Logical Loopback Interface with an associated IP can be used in a network environment for additional fault tolerance:
- A router has 2 interfaces. One is connected to Switch 1 and the other is connected to Switch 2. 
- SNMP is used to poll the device every 60 seconds.
- If each interface was different IP, then which interfaced should be polled?
- If the IP of a single interface was polled/pinged and the ping didn't respond, then the whole router appears as being down. 
- Solution: Create a Logical Loopback Interface and assign it an IP Address to be tracked with SNMP. Since it's a logical interface that's being monitored, a ping would still respond if either Switch interface is up. The router would only appear down, if both Switch interfaces were down. 

If a network devices is having a problem, but the cabling looks good (i.e. there are signals in/out), then perform Protocol Analysis on the packets going through. 

A Wire Tap can be put in to test the cable. A Tap streams off copies of the data (i.e. mirroring) being transmitted over the wire to a Protocol Analyzer. 

---

## Software Tools and Commands

### Tools and Commands Overview

Wi-Fi Scanner: scans for access points and displays their center channels.  

Protocol Analyzer: tool used to inspect frames, packets, and 3-way handshakes. 
- [Wireshark](https://www.wireshark.org/)

IP Scanner: scans for IP Addresses. 

Port Scanner: scans for open ports. 

Performance Analyzer: tool used to measure the speed of the network. 

NetFlow: tool used to identify traffic types flowing through the network. A high-level overview of the discovered traffic is sent to a NetFlow Collector.
- [Cisco IOS NetFlow](https://www.cisco.com/c/en/us/products/ios-nx-os-software/ios-netflow/index.html)

NetFlow is used to see what protocols are being used on the network.

Trivial File Transfer Protocol (TFTP): a protocol used to copy software to networking devices, popular  for firmware updates. TFTP doesn't use authentication or encryption. 

Secure Copy Protocol (SCP): works like TFTP, but is secure. 

Terminal Emulator: software used to connect to run commands on a network device while using SSH, or connected to a console port. 

A terminal emulator is used for CLI access to a device.

Command Line Interface (CLI): a means of interacting with a computer program by inputting lines of text called "command-lines".

`ipconfig` (Windows) / `ifconfig` (Linux) / `ip address`:  returns the IP address information of a device

`ipconfig` is used to see an IP address on Windows.

`ifconfig` is used to see an IP address on Linux. 

`ping`: stands for Packet Internet Groper; tests for connectivity between a computer and a destination IP address.

Address Resolution Protocol (ARP):  tests Layer 3 and down in the TCP/IP stack. Multiple commands exist, based on platform, to extract address translation information and test if ARP has the Layer 2 information for the next loop in its cache. 

A `ping` can also be sent to a URL to test name resolution. 

`dig` (Linux) | `nslookup`: tests name resolution by querying name servers.

`dig` or `nslookup` tests DNS name resolution.

`traceroute` | `tracert` (Windows): helps identify how far, in a path, a packet traveled (i.e. shows each Layer 3 hop in the path). 

`traceroute` verifies the path taken through a network.

`route` (linux) | `netstat -r`: shows the routing table on an end device. 

`netstat` can also be used to show open connections.

`ssh`: a secure terminal emulator application. 

`telnet`: an insecure terminal emulator application. 

`tcpdump`: a packet analyzer ran on end devices.

`nmap` | `zenmap` (gui): a scanner that can look for open ports, finds what devices are on the network, and interrogate those devices (e.g. what OS is the device running?). 

Summary

| Command/Tool | Purpose/Function |
| --- | --- |
| NetFlow | see what protocols are being used on the network |
| terminal emulator | used for CLI access to a device | 
| `ipconfig` | see an IP address on Windows |
| `ifconfig` | see an IP address on Linux |
| `dig` or `nslookup` | test DNS name resolution |
| `traceroute` | verify the path take through a network |

### Software Tools

WiFi Analyzer: a software tool that scans for Wireless Access Points (WAPs), then reports on the Wi-Fi networks, center channels, bandwidth swath, and ranges (e.g. 2.4 GHz and 5 GHz) in use. 

Spectrum Analyzer: scans for any additional radio frequencies in use, not just wireless signals
- [NetSpot]](https://www.netspotapp.com/)

Protocol Analyzer: analyzes packets, then reports on the protocols and ports in use
- [Wireshark](https://www.wireshark.org/)

Port Scanner: scans for open ports
- Tricks the Operating System (OS) into thinking someone wants to connect. If a response is received, then we know that's an open port.
- [Nmap](https://nmap.org/)

Trivial File Transfer Protocol (TFTP): used to move large numbers of files to networking devices, especially if they're not yet in production. 

Performance Analyzer: tool used to identify/verify connectivity, measure latency and measure jitter. 
- Some software vendors have this tool built-in.
- Cisco has their own version called [Cisco IP SLA](https://learningnetwork.cisco.com/s/blogs/a0D3i000002SKN0EAO/ip-sla-fundamentals).

[iPerf](https://iperf.fr/): a tool used to take active measurements of the maximum achievable bandwidth on IP networks.
- iPerf can measure the maximum transmission unit (MTU) and function of TCP regarding window size, packet loss, delay. 
- iPerf can also setup periodic logging
- These measurements are achieved by setting up an iPerf server and client, then measuring the connection between the two. 

Summary 
| Tool | Purpose/Function |
| --- | --- |
| Packet/Protocol Analyzer | views the details of a 3-way TCP handshake |
| Network Scanner | discovers systems and open ports |
| TFTP | a fast, but not secure, file transfer protocol |
| iPerf | measures traffic going over a network |

### Virtual Machines

hypervisor: a program used to run and manage one or more virtual machines on a computer.

A type-1 hypervisor runs directly on hardware (bare-metal). 

[VMware](https://www.vmware.com/) ESXi is an example of a type-1 hypervisor. 

A type-2 hypervisor runs as an application (i.e. a virtualized environment on an OS). 

VMware Workstation (Windows) and VMWare Fusion (MAC) are examples of type-2 hypervisors. 
- [VMware Workstation Player](https://www.vmware.com/content/vmware/vmware-published-sites/us/products/workstation-player.html.html) |  [VMware Workstation Pro](https://www.vmware.com/products/workstation-pro/workstation-pro-evaluation.html)
- [VMware Fusion](https://www.vmware.com/products/fusion/fusion-evaluation.html)

[Oracle VM VirtualBox](https://www.virtualbox.org/) is another example of a type-2 hypervisor. 

Oracle VM VirtualBox uses the ova (open virtualization format) file type. 

Virtualized Networking
- The NIC of the PC running the VM can act as a router performing NAT/PAT.
- Bridge Adapter: mode used to connect the virtual Network Adapter of a VM to a Physical Network Adapter.

### Desktop CLI Tools

`ipconfig`: returns the IP address of a Windows device.

`ipconfig /all` | `ipconfig -all`: returns additional networking info (e.g. Layer 2 Address, DHCP Server Address, DNS Server, etc) of a Windows device. 

`ifconfig`: returns the network information for all networking interfaces on a Linux device. 

`ifconfig <interface>`: returns the IP address of a Linux device (example: `ifconfig eth0`).

`ip address`: returns the IP Address of a Linux device.

`ipconfig /displaydns`: displays DNS information. 

`ipconfig /flushdns`: flushes the DNS cache. Used if DNS information is wrong/poisoned. 

`ping`: verifies Layer 3 connectivity from device being ping'd from to the device being ping'd. 

Pings can be sent to an IP address (e.g. `ping 8.8.8.8`). 

Pings can also be sent to a URL to verify name resolution/DNS (e.g. `ping www.comptia.org`)

`arp`: returns Address Resolution Protocol (ARP) table. 

`dig` or `nslookup`: used to verify name resolution. 

`tracert` (Windows) | `traceroute` (all other platforms): used to discover how far in a path traffic is sent. 
- helps identify where in a path something is going wrong. 
- used the Time-to-Live (TTL) in the IP Header at Layer 3. 
- Trace Route works by sending  3 packets to a destination IP with a Time-to-Live (TTL) of 1. When a router sees a TTL of 1 it kills the packet and returns an ICMP message back. The computer measures how long it took to get the response. Then it sends 3 packets with TTL of 2. The computer measures the response when the TTL is decreased to 1 and the packet is killed (i.e. the next hop in the path). This process is repeated by increases the initial packets TTL by 1 each time to measure each hop. 
- Note: The Layer 4 Protocol used by Trace Route can be different based on the platform it's used on. Windows uses ICMP. Linux, Routers, and Firewalls are likely to use UDP. 

`pathping`: used to verify a path to a network (i.e. combination of ping and traceroute).

`netstat`: used to show open connections/sessions, listening ports on a device, the routing table on an end device, and IP addresses in a TCP connection. 

[`nmap`](https://nmap.org/): a utility for network discovery and security auditing. 

`tcpdump`: used to show traffic going into and out of an interface in text format. Provides a detailed look at packets without having to use a packet analyzer. 

Summary

| Command | Function |
| --- | --- |
| `netstat` | used to see connection information |
| `dig` or `nslookup` | used to test DNS name resolution |
| `traceroute` | used to see the path taken over a network |
| `arp` | can be used to see or set a layer 3 to layer 2 mapping |
| `ipconfig` | can be used to flush the DNS cache on Windows |
| `tcpdump` | used to see packet information on the local computer |

### Network Device CLI Tools

`ssh` or `telnet` commands can be used to access the Command Line Interface (CLI) of a networking device. 

Unlike `telnet`, `ssh` provides a secure and is therefore the preferred method of connecting. 

The commands used to see and configure the details on a network device (such as a switch, router, or firewall) will vary slightly (and sometimes quite a bit), based on the vendor. 

---

## Implementing Wi-Fi

### Wi-Fi Case Study

Picture of Doneness (POD): the goal (i.e. what the customer expects when the project is complete). 

The Picture of Doneness should include: 
- Network Details
	- the number of WLANs
	- the number of subnets
	- the number of hosts needed per subnet
	- the Speed and Duplex for the APs
	- the VLANs being used
- Coverage details
	- the number of Access Points (APs)
	- the center-channels and range swaths to provide overlapping coverage with non-competing frequencies
- Security Details
	- Authorization to Use (e.g. 802.11n WPA2, Auth PSK, UserAuth, Captive Portal)
- Controller Details
	- is a Wireless Controller being used?

Autonomous Mode: Access Points (APs) are configured without the use of a controller (i.e. manually). 

Lightweight Mode: Access Points (APs) are configured using a Controller. 

Important considerations regarding the customer's Wi-Fi network: 
- Overlapping Coverage
- Authentication Method
- Speed and Duplex for the APs
- Non-Overlapping Frequencies

### AP Firmware and OS

Access Points can be connected to over the networking using the IP Address of the Access Point, then logging in with a username/password. 

Reviewed the vendor website of the Access Point for updates and release notes. 

When downloading software, compare the hash value of the software downloaded with the value provided by the vendor to verify the software hasn't been tampered with (e.g. malware). 

TFTP, or a direct connection with a console cable, can be used to transfer the software/update to the Access Point. 

### AP to Switch Port

Wireless networks are extensions of a wired network. 

Access Points have to be wired/connected to a Switch Port, or to a Patch Panel connected to a Switch Port. 

Document which device is connected to each Switch and Patch Panel Port. 

If attempting to locate the Switch Port an Access Point is connected to in an undocumented environment, a dongle can be placed on the Access Point Cable, then a Tone Generator can be used to locate the Access Port. 

Questions regarding Connection Between a Wireless Access Point (WAP) and Switch Port: 
- Is the speed correct (e.g. should be max: 1 GB)?
- Is duplex correct (e.g. Full Duplex)?
- What VLAN should the Access Point be in?

If using a Controller, then a logical tunnel should exist between the Access Point and the Controller. Users can be connected to different VLANs based on which Wireless Network they connect to. 

If the Access Points are running in Autonomous Mode (i.e. there's no Controller), then the Access Point would need to be placed in the same VLAN the users should be in. 

Power over Ethernet (PoE): power and data is provided through the same Ethernet cable. 

PoE prevents having to run multiple cables to each Access Point. 

The proper Switch Port configuration of a Port with a 1G Access Point attached is: 1,000 Mbps, Full Duplex. 

### Trunking to Controller

What VLAN should a device go to?

If there are multiple Wireless Networks, and multiple Subnets, that need routed between, then: 
- This implies that the network is bigger than a single VLAN. 
- A Wireless LAN Controller should be used to coordinate traffic, based on which VLAN a customer is coming in on and which IP Subnet, and VLAN, they belong to. 

If there are multiple VLANs, on multiple Subnets, and traffic in coming in from the Access Points to the Controller, then the Controller needs the ability to access all of the VLANs in order to forward traffic appropriately. This is accomplished via Trunking between the Controller and the Physical Network. 

802.1Q Trunking tags each packet between the Controller and the Switch Port. 

An On-Prem (i.e. Local) Controller that needs to support multiple subnets, should connect to the Physical Networking using an 802.1Q Trunk. 

### IP Addressing Options

Best practice is to have a separate network specific for Network Management. 

Wireless devices (e.g. APs, Controllers) may be placed on their own separate network. 

Each VLAN should also have its own separate Subnet also. 

The IP of each Access Point could be set statically, delivered using DHCP, or reserved using a DHCP reservation. 

If a DHCP Server isn't directly connected on a VLAN, then a DHCP-Relay/IP-Helper is needed to listen for discover messages and forward them to the DHCP Server. 

There are varying ways for an Access Point to discover a Controller, that vary based on the equipment manufacturer/vendor: 
- Sending a Discover message. 
- A DHCP option that indicates the Controller's location. 
- Sending a Broadcast message to locate the Controller. 

To configure a Switch Port for a Controller supporting multiple subnets, designate the Port as a Trunk Port. A Trunk is able to support multiple VLANs and uses 802.1Q tagging to identify them. 

A specific IPv4 Address can be assigned to a network device by setting it statically, or using a DHCP reservation. 

### IP Subnetting Plan

This section walks through an example request from a customer network change request. 

The customer wants 5 new Subnets associated with 5 new Wireless Local Area Networks. Each Subnet must be able to support at least 12 hosts (i.e. 5 Subnets on 5 WLANs supporting 12 Hosts each). 

10.1.9.0/24 is the Address Space given that the Subnets much be carved from. 

Use the Finger game to determine how many bits are needed to support the number of Subnets requested: 

| finger | bits |
| --- | --- |
| 1 | 2 |
| 2 | 4 | 
| 3 | 8 | 

8 is greater than 5. 

3 bits are needed to support the number of Subnets requested. 

The original Subnet Mask was 10.1.9.0/24 to compensate for the 3 additional bits needed, then Mask then becomes: 10.1.9.0/27

Determine the Block Size. 
- A network address is 4 octets (8 bits each) for a total of 32 bits. 
- Our mask of 27 completely fills the first 3 octets. Fill bits of the last octet until all bits of the mask are listed. 
- All of the filled bits represent the Network Address Space, the unfilled bits are the Host Address Space. 

<- Network Address Space | Host Address Space ->

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 

- The first bit of the Host Address space represents the Block Size. 
- In our example The Block Size is 32. 
- To determine the number of hosts a subnet can support subtract 2 from the Block Size to account for a Subnets network address and broadcast address. 
- In our example: Block Size - 2 = 32 - 2 = 30 | Therefore, the number of supported hosts for each Subnet is 30. 
- The request was that each Subnet to support at least 12 Hosts. We're able to fulfill the request, because 30 > 12. 

To get the start address of each new subnet, add the Block Size. 

**Valid Host Addresses for Each New Subnet**

| Start Address |
| --- |
| 10.1.9.0/27 |
| 10.1.9.32/27 |
| 10.1.9.64/27 |
| 10.1.9.96/27 |
| 10.1.9.128/27 |

To get the first host in each range, add 1 to the Block Size. 

To get the last host in each range, subtract 2 from the start of the next range. 

**Ranges of Host IPs for Each Subnet**

| Subnet | Ranges |
| --- | --- |
| A | .1-30 | 
| B | .33-62 |
| C | .65-94 |
| D | .97-126 |
| E | .129-148 |

Question: How many new subnets could we create by using 3 additional bits for the mask? 

Answer: 8. We can calculate this easily using the finger game as shown at the start of this example/section. 

### Location, Signal, and Channel

Location
- Perform a Wireless Site Survey to determine the location Access Points should be placed. 
- After the initial survey, temporarily place the Access Points, then cart a Wireless device around the whole building to measure signal strength and ensure proper coverage. 

Signals
- Are signals going to be ran in the 2.4 GHz and/or 5 GHz range(s)?
- What standard regarding 802.11_ (e.g. n, ac) are being used?

Channels
- What Center Channels are going to be used?
- What other Wireless Signals, outside of the network, are generating signals (i.e. are beyond our control)? Avoid using the same Center Frequencies and Swath as those signals. 
- A Controller takes all the signals the connected APs see and implements the best non-conflicting frequencies to use. 

In the 2.4 GHz range, the 1, 6, and 11 Center Channels are non-overlapping. 

### Creating Wireless Networks

How WLANs are created depends on the vendor of the network equipment being used. 

Make sure to test the WLAN after it's creation.

Potential Issues
- If a user is getting a DHCP address in the wrong subnet for that WLAN:
	- DHCP Services may be setup incorrectly. 
	- The user is connected to the wrong SSID. 
- If a computer is hardwired into the network and connected to a Wireless network at the same time, then the computer may try to use both networks at the same time, causing conflicts. 
	- Unplug or disable the Ethernet connection, or disable the Wireless connection. 
- If a user is unable to connect to Wi-Fi: 
	- Ensure the computer's NIC isn't disabled. 

Once the Wireless Network has been created and verified as working, then Document: 
- What Wireless Network Standards are in use. 
- Which Frequencies are in use. 
- A copy of the Site Survey that shows the coverage of the Access Points.
- The IP Addressed on the Controller. 
- The Login Credentials for the Networking Devices that were configured. 

The following could cause problems for a Wi-Fi customer: 
- The Wi-Fi and LAN NIC being enabled at the same time. 
- A Wi-Fi adapter being turned off. 
- A user attempting to connect to wrong SSID. 

---

## General Network Troubleshooting

### Overview of Network Troubleshooting

When starting to troubleshoot an issue, it's important to gather a **baseline** for what the expected behavior is, in order to have something to compare the troubleshooting against. 

Application Specific Integrated Circuits (ASIC): an Integrated Circuit (IC) custom-designed for a particular task or application.

Emulation of network device features won't run as fast as dedicated hardware. 

NetFlow: a network protocol developed by Cisco that provides a high-level overview of the types of traffic patterns and the top applications being used over the network. 

A benefit of Out of Band (OOB) management is that even if all of a device's Ethernet connections fail, the device can still be accessed through a terminal connection (e.g. using a console cable). 

### What Could go Wrong?

Anything part/component of the TCP/IP Protocol Stack (Physical, Data Link, Network, Transport, Application) could potentially have an issue. 

Speed/Duplex
- A Switch Port and the device connected to it both have to agree on the speed/duplex to use. 
- A Layer 2 Switched environment uses Full Duplex (i.e. sends and receives at the same time). 

Duplicates
- If multiple devices have the same IP Address, an IP Conflict occurs. 
- Documentation reduces duplication. 
- IP Address Management (IPAM): a tool suite used to track and manage IPs. Includes a database of the static IPs being used and DHCP Servers. 

Loops
- Layer 2 Loop
	- A Layer 2 Loop occurs when two devices are connected with more than a single path. 
	- Spanning Tree Protocol (STP) identifies parallel paths and prevents Layer 2 Loops. 
	- STP is on by default on most commercial switches. 
- Layer 3 Loop
	- Misconfiguration of Switches/Routers can lead to Layer 3 Loops. 
	- Example: Two Multi-Layer Switches (MLS) are connected to each other and a router for redundancy. A device pings and IP Address. The ping is forwarded to a MLS. The MLS forwards the ping to the router. The router forwards the ping to the other MLS, which then forwards back to the original MLS. 
	- Ensure Dynamic Routing Protocols are operating correctly. 
	- Packets should include a Time to Live (TTL). Each time a packet is forwarded the TTL decreases. If the TTL reaches zero, then the packet is killed. 

DHCP Server on a Different VLAN
	- DHCP requests follow the DORA (Discover, Offer, Request, Acknowledgement) process. 
	- When a client sends an initial Discover request to DHCP, if there isn't a DHCP server setup on the local subnet, then there won't be a response. 
	- DHCP Relay Function/DHCP Helper/IP Helper: a device setup on a VLAN, without a DHCP server, that's used forward DHCP requests to where the DHCP server is located. 

Incorrect Default Gateway
	- If a client to talk to other devices on the network, but not externally, then ensure the Default Gateway is correct. 

Ensure all Layer 3 routers know how to forward correctly. 

Incorrect Subnet Mask
- If a PC believes it's in the rogue subnet of /16, then it would think 10.1.20.# is in the same network as 10.1.10.# network. 
- Verify the subnet mask is correct. 

Certificate Authorities 
- When a client accesses a secure site, the server presents a certificate that the client validates. 
- If a device or piece of software can't, or won't, trust a certificate, then that can cause problems. 
- [badssl.com](https://badssl.com/) is a site use to test SSL Certificates. 

Filtering
- Access Control List (ACL): a set of rules that determines the types of traffic and software that users and computers are able to access. 
- If filtering is been implemented incorrectly, then business traffic could be prevented from passing through the network. 

Port/VLAN Assignment Issues

Clocks/Incorrect Time
- Incorrect Time can affect certificates. 
	- If the time is set in the past, then expired certificates may be allowed. 
	- If the time is set in the future, then a certified that isn't expired could appear as though it was and thereby access to resource relying on the certificate would be blocked. 
- Network Time Protocol (NTP) is used to sync clocks. 

Name Resolution
- If a computer can't resolve DNS, then it won't be able to access a site by name. 
- Trying pinging the site by it's IP Address. If the ping responds to the IP (8.8.8.8), but not the domain name (e.g. google.com), then DNS is likely the issue. 
- Ensure the client is set to use the correct DNS Server. 

Licenses
- Firewalls perform URL filtering based on categories. If the firewall being used is subscription based and the subscription expires, then issue can occur. Typically, the firewall would either start blocking all or allowing all traffic. 
- Ensure licenses aren't expired.  

Misconfiguration of Allow/Deny Traffic on the Firewall

Rogue Devices on the Network
- DHCP Snooping: used to block rogue DHCP servers

Bring Your Own Device (BYOD)
- Have policies and guidelines regarding acceptable use for personal devices being brought onto the network. 

**Summary of Some Common Issues**

| Network Problem | Likely Cause |
| --- | --- |
| Name Resolution Failure | Wrong DNS Server |
| Slow Router | Device is Virtualized |
| Certificate Error | Untrusted CA (Certificate Authority) |
| No IP Address | DHCP Relay is Not Configured |

### Tshoot Scenario 1

A DHCP Relay is required when the DHCP Server isn't directly connected to the subnet where the DHCP Client is. 

### Tshoot Scenario 2

The Default Gateway Address provided by a First Hop Redundancy Protocol (FHRP), such as Virtual Router Redundancy Protocol (VRRP) or Hot Standby Router Protocol (HSRP), is a Virtual IP (VIP). 

### Tshoot Scenario 3

Incorrect static configuration on a computer or an incorrect DHCP configuration on a DHCP Server would both cause a computer to use an incorrect Default Gateway. 

### Tshoot Scenario 4

`ping` uses the Internet Control Message Protocol (ICMP). 