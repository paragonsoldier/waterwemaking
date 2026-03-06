This page lists several sections covered on the exam that require rote memorization.  

### Copper Cable Categories

| Ethernet Standard | Cable Category | Maximum Supported Distance |
| --- | --- | --- |
| 1000BASE-T | Cat 5 | 100 meters |
| 1000BASE-T | Cat 5e (enhanced) | 100 meters |
| 10GBASE-T | Cat 6 | Unshielded: 55 meters; Shielded: 100 meters |
| 10GBASE-T | Cat 6A (augmented) | 100 meters |
| 10GBASE-T | Cat 7 (Shielded only) | 100 meters |
| 40GBASE-T | Cat 8 (Shielded only) | 30 meters |

### T568A and T568B Termination

![[TIA_EIA-pin-outs.png]]

| TIA/EIA 568A | TIA/EIA 568B |
| --- | --- |
| Green/White | Orange/White |
| Green | Orange |
| Orange/White | Green/White |
| Blue | Blue |
| Blue/White | Blue/White |
| Orange | Green |
| Brown/White | Brown/White |
| Brown | Brown |

### Ethernet over Fiber

- 100BASE-FX
	- 100 Mb Ethernet over Fiber using Laser components
	- Multi-mode Fiber Pair
	- Max Distance: 400 meters (half-duplex), 2 kilometers (full-duplex)
- 100BASE-SX
	- 100 Mb Ethernet over Fiber using LED optics (less expensive)
	- Max Distance: 300 meters
- 1000BASE-SX
	- Gb Ethernet over Fiber using NIR (near infrared) light
	- Multi-mode Fiber (usually)
	- Max Distance: 220-500 meters (depending on fiber type)
- 1000BASE-LX
	- Gb Ethernet over Fiber using Long Wavelength Laser
	- Max Distance: 550 meters (using multi-mode fiber), 5 kilometers (using single-mode fiber)
- 10GBASE-SR (Short Range)
	- 10 Gb Ethernet over Fiber
	- Multi-mode Fiber
	- Max Distance: 26-400 meters (depending on fiber type)
- 10GBASE-LR (Long Range)
	- 10 Gb Ethernet over Fiber
	- Single-mode Fiber
	- Max Distance: 10 kilometers

To remember fiber type for the exam, remember the pneumonic: "S is not single" (i.e Base-S uses multimode). 


### Common Ports 1.5

| Protocol | Port |
| -------- | -------------- |
| Telnet | tcp/23 |
| SSH | tcp/22 |
| DNS | udp/53, tcp/53 |
| SMTP | tcp/25 |
| POP3 | tcp/110 |
| POP3S | tcp/995 |
| IMAP | tcp/143 |
| IMAPS | tcp/993 |
| SFTP | tcp/22 |
| FTP | tcp/20, tcp/21 |
| TFTP | udp/69 |
| DHCP | udp/67, udp/68 |
| HTTP | tcp/80 |
| HTTPS | tcp/443 |
| SNMP | udp/161 |
| Syslog | udp/514 |
| RDP | tcp/3389 |
| NTP | udp/123 |
| SIP | tcp/5060-5061 |
| SMB | tcp/445 |
| LDAP | tcp/389 |
| LDAPS | tcp/636 |
| MS-SQL | tcp/1433 |
| `SQL*Net` | tcp/1521 |
| MySQL | tcp/3306 |


### Wireless Standards 2.4

| Frequencies | Maximum MIMO Streams | Maximum Theoretical Throughput (per stream) | Maximum Theoretical Throughput (total) |
| --- | --- | --- | --- | --- |
| 802.11a | 5 GHz | N/A | 54 Mbps | 54 Mbps |
| 802.11b | 2.4 GHz | N/A | 11 Mbps | 11 Mbps |
| 802.11g | 2.4 GHz | N/A | 54 Mbps | 54 Mbps |
| 802.11n | 5 GHz / 2.4 GHz | 4x MIMO | 150 Mbps | 600 Mbps |
| 802.11ac | 5 GHz | 8x DL MU-MIMO | 867 Mbps | 6.9 Gbps |
| 802.11ax | 5 GHz / 2.4 GHz | 8x DL and UL MU-MIMO | 1,201 Mbps | 9.6 Gbps |


### Cellular Standards 2.4 2

| Cellular Technology | Band Type / Technology Type | Average Speed | Theoretical Speed |
| --- | --- | --- | --- |
| 4G | LTE | 20 Mbps | 150 Mbps |
| 4G | LTE-A | 40 Mbps | 300 Mbps |
| 5G | Low-Band | 55 Mbps | 150 Mbps |
| 5G | Mid-Band | 150 Mbps | 1.5 Gbps |
| 5G | High-Band | 3 Gbps | 70 Gbps |


### Error Condition Severity Levels 3.1

*0 (most severe) to 7 (least severe)*

| Level | Severity |
| Level 0 | Emergency
| Level 1 | Alert
| Level 2 | Critical
| Level 3 | Error
| Level 4 | Warning
| Level 5 | Notice
| Level 6 | Information
| Level 7 | Debugging

802.1d - Spanning Tree Protocol (STP)
802.1q - Trunking
802.1x - Network Access Control (NAC)
802.3ad - Link Aggregation Control Protocol (LACP)
802.3af - PoE
802.3at - PoE+

### Policies and Agreement Types 3.2
AUP (Acceptable Use Policy)
MOU (Memorandum of Understanding)
NDA (Non-Disclosure Agreement)
SLA (Service Level Agreement)