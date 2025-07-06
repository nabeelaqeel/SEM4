> [!NOTE]- TIPS FROM LECTURER
> ```
> 10 question - 8 July : 3 - 5 pm BK 1
> 
> 1Q : 5m
> 
> explain ;
> define ;
> compare ; 
> differentiate ; 
> give your opinion ;
> technique ;
> why ;
> how ;
> 
> Job of network security profession 
> CIA
> malware worm ,virus , recoinassance attack 
> SDN , Divition of network function
> InBand and outband management
> NTP 
> IDS and IPS
> ```

# Job of Network Security profession
- File : `Network Security v1.0 - Module 3.pptx`
- responsible for maintaining data assurance for an organization and ensuring the integrity and confidentiality of information.
- Job roles 
	- Chief Information Officer (CIO)
	- Information Security Officer(CISO)
	- Security Operations(SecOps) Manager
	- Chief Security Officer(CSO)
	- Security Manger 
	- Network Security Engineer
- 
# CIA
- `Confidentiality` 
	- Only authorized individuals, entities, or processes can access sensitive information.
- `Integrity` 
	- This refers to the protection of data from unauthorized alteration.
- `Availability` 
	- Authorized users must have uninterrupted access to the network resources and data that they require

# Malware , worm , virus
- File :  `Network Security v1.0 - Module 2.pptx`
- Malware : 
	- short for malicious software or malicious code. It is code or software that is specifically designed to damage, disrupt, steal, or generally inflict some other “bad” or illegitimate action on data, hosts, or networks.
	- Common types of malware are:
		- virus
		- worm
		- Trojan horse
 - Virus : 
	 - type of malware that spreads by inserting a copy of itself into another program. After the program is run, viruses then spread from one computer to another, infecting the computers. Most viruses require human help to spread.
- Trojan Horses :
	- software that appears to be legitimate, but it contains malicious code which exploits the privileges of the user who runs it.
- Worms : 
	-  Computer worms are like viruses because they replicate and can cause the same type of damage. Specifically, worms replicate themselves by independently exploiting vulnerabilities in networks. Worms can slow down networks as they spread from system to system.
	- Most worm attacks consist of three components:
		- `Enabling vulnerability` - A worm installs itself using an exploit mechanism, such as an email attachment, an executable file, or a Trojan horse, on a vulnerable system.
		- `Propagation mechanism` - After gaining access to a device, the worm replicates itself and locates new targets.
		- `Payload` - Any malicious code that results in some action is a payload. Most often this is used to create a backdoor that allows a threat actor access to the infected host or to create a DoS attack.
		- Propagation technique used by the Code Red worm
		- ![](../images/Screenshot%20from%202025-07-01%2001-17-13.png)
- Ransomware
	- malware that denies access to the infected computer system or its data. The cybercriminals then demand payment to release the computer system
- Others : 
	- Spyware
	- Adware
	- Scareware
	- Phishing
	- Rootkits
- File : `Network Security v1.0 - Module 3.pptx`
- Mitigating :
	- Worms
		- four phases: containment, inoculation, quarantine, and treatment
		- ![](../images/Screenshot%20from%202025-07-02%2001-07-12.png)
	- Reconnaissance Attack
		- Implementing authentication to ensure proper access.
	    - Using encryption to render packet sniffer attacks useless.
	    - Using anti-sniffer tools to detect packet sniffer attacks.
	    - Implementing a switched infrastructure.
	    - Using a firewall and IPS.
	- Access Attack : 
		- `Use strong passwords` - Strong passwords are at least eight characters and contain uppercase letters, lowercase letters, numbers, and special characters.
		- `Disable accounts` after a specified number of unsuccessful logins has occurred - This practice helps to prevent continuous password attempts.
	- Dos Attack :
		- sign : 
			- network utilization graph showing unusual activity
			- unusually slow network performance
			- large number of user complaints about unavailable resources
		- DHCP snooping,
		- port security
		- ARP inspection
		- ACLs
	- NFP Framework
		- Cisco Network Foundation Protection(NFP) Framework
		- routers and switches into three functional areas:
			- `Control plane` - Responsible for routing data correctly.
			- `Management plane` - Responsible for managing network elements.
			- `Data plane`- Responsible for forwarding data.
		- ![](../images/Screenshot%20from%202025-07-02%2001-17-02.png)

# IDS , IPS
- File : `Network Security v1.0 - Module 11.pptx`
- Intrusion Detection System (IDS) , Intrusion Prevention System(IPS)
- ![](../images/Screenshot%20from%202025-07-06%2011-17-16.png)
- 2 primary kinds of IPS available: 
	- host-based IPS (HIPS) 
		- - combination of antivirus software, antimalware software, and a firewall.
		- example of a HIPS is Windows Defender.
	- network-based IPS.
		- - implemented using a dedicated or non-dedicated IPS device such as a router
		- - can be implemented in several ways:
			- On a Cisco Firepower appliance
			- On an ASA firewall device
			- On an ISR router
			- As an NGIPSv for VMware
		- - The hardware of all network-based sensors includes three components:
			- **NIC** - The network-based IPS must be able to connect to any network, such as Ethernet, Fast Ethernet, and Gigabit Ethernet.
			- **Processor** - Intrusion prevention requires CPU power to perform intrusion detection analysis and pattern matching.			    
			- **Memory** - Intrusion detection analysis is memory-intensive. Memory directly affects the ability of a network-based IPS to efficiently and accurately detect an attack.)
- Modes of Deployment
	- inline mode (interface pair mode)
		- ![](../images/Screenshot%20from%202025-07-06%2011-22-15.png)
	- promiscuous mode (passive mode)
		- ![](../images/Screenshot%20from%202025-07-06%2011-22-34.png)
- IPS Component
	- - **IPS detection and enforcement engine** -
		- To validate traffic, the detection engine compares incoming traffic with known attack signatures that are included in the IPS attack signature package.
    
	- **IPS attack signatures package** - 
		- This is a list of known attack signatures that are contained in one file. The signature pack is updated frequently as new attacks are discovered. Network traffic is analyzed for matches to these signatures.
	
- Network Monitoring Methods
	- common **methods** used to capture traffic and send it to network monitoring devices:
		- Network taps, sometimes known as test access points (TAPs)
			- - passive splitting device implemented inline between a device of interest and the network.
			- ![](../images/Pasted%20image%2020250706112542.png)
		- Traffic mirroring using Switch Port Analyzer (SPAN) or other port mirroring approaches.
		- SPAN Features![](../images/Screenshot%20from%202025-07-06%2011-25-58.png)![](../images/Screenshot%20from%202025-07-06%2011-27-41.png)
- File : `Network Security v1.0 - Module 12.pptx`
- IPS Signature 
	- 3 distinctive attributes
		- Type
		- Trigger
		- Action
	- - There are two types of signatures:
		- **Atomic Signature -** This is the simplest type of signature because a single packet, activity, or event identifies an attack. The IPS does not need to maintain state information and traffic analysis can usually be performed very quickly and efficiently.
		- **Composite Signature -** Also called a stateful signature because the IPS requires several pieces of data to match an attack signature. The IPS must also maintain state information which is referred to as the event horizon. The length of an event horizon varies from one signature to the next.
		- ![](../images/Screenshot%20from%202025-07-06%2011-33-30.png)![](../images/Screenshot%20from%202025-07-06%2011-33-59.png)
- Cisco IPS
	- - **Cisco Firepower Next-Generation IPS (NGIPS)** - These are dedicated in-line threat prevention appliances that provide industry leading effectiveness against both known and unknown threats.
	- NGIPS **features** include:
	    
		- IPS rules that identify and block attack traffic that target network vulnerabilities
		    
		- Tightly integrated defense against advanced malware incorporating advanced analysis of network and endpoint activity
		    
		- Sandboxing technology that uses hundreds of behavioral indicators to identify zero-day and evasive attacks
		    
		- Also includes Application Visibility and Control (AVC), Cisco Advanced Malware Protection (AMP) for Networks, and URL Filtering
	- **Cisco Snort IPS** - This is an IPS service that can be enabled on a second generation ISR (ISR G2) (i.e., ISR 4000s). Note that Cisco 4000 ISRs no longer support Cisco IOS IPS.
		- -functionalities:
			- Intrusion detection system (IDS) and IPS mode
			- Three signature level
			- An allowed list
			- Snort health monitoring
			- Fail open and close
			- Signature update			    
			- Event logging
	    
	- **External Snort IPS Server** - This is similar to the Cisco Snort IPS solution but requires a promiscuous (i.e., a SPAN switch port) port and an external Snort IDS/IPS.
	- - Snort IPS requires two VPG interfaces:
		- **Management interface** - This is the interface that is used to source logs to the log collector and for retrieving signature updates from Cisco.com. For this reason, this interface requires a routable IP address.
		    
		- **Data interface** - This is the interface that is used to send user traffic between the Snort virtual container service and the router forwarding plane.
		- ![](../images/Screenshot%20from%202025-07-06%2011-37-30.png)

# Inbound & Outbound Management
File : `Network Security v1.0 - Module 6.pptx

- **In-band** - Information flows across an enterprise production network, the Internet, or both, using regular data channels.
	- ![](../images/Screenshot%20from%202025-07-06%2011-47-27.png)
	- guidelines are:
		- Apply only to devices that need to be managed or monitored.
		- Use IPsec, SSH, or SSL when possible.
		- Decide whether the management channel needs to be open at all times.

- **Out-of-band (OOB)** - Information flows on a dedicated management network on which no production traffic resides.
	- ![](../images/Screenshot%20from%202025-07-06%2011-47-45.png)
	- - guidelines are:
		- Provide the highest level of security.
		    
		- Mitigate the risk of passing insecure management protocols over the production network.

# NTP
- `Network Security v1.0 - Module 6.pptx`
- NTP networks use a hierarchical system of time sources. Each level in this hierarchical system is called a stratum. The stratum level is defined as the number of hop counts from the authoritative source
- ![](../images/Screenshot%20from%202025-07-06%2011-58-03.png)
- command
```
- **ntp server** _ip-address_
- - **show clock detail**
- - **show ntp associations** and **show ntp status**
```


# SDN
- File : `ENSA_Module_13.pdf`

`Software-Defined Networking (SDN`) - A network architecture that virtualizes the
network, offering a new approach to network administration and management that
seeks to simplify and streamline the administration process.

• `Control plane` - This is typically regarded as the brains of a device. It is used to make
forwarding decisions. The control plane contains Layer 2 and Layer 3 route forwarding
mechanisms, such as routing protocol neighbor tables and topology tables, IPv4 and
IPv6 routing tables, STP, and the ARP table. Information sent to the control plane is
processed by the CPU.
• `Data plane `- Also called the forwarding plane, this plane is typically the switch fabric
connecting the various network ports on a device. The data plane of each device is
used to forward traffic flows. Routers and switches use information from the control
plane to forward incoming traffic out the appropriate egress interface. Information in
the data plane is typically processed by a special data plane processor without the
CPU getting involved.
- `management plane` is responsible for managing a device through its connection
to the network.
![](../images/Screenshot%20from%202025-07-06%2012-16-41.png)

- Components of SDN may include the following:
	• OpenFlow - This approach was developed at Stanford University to manage traffic
	between routers, switches, wireless access points, and a controller. The OpenFlow
	protocol is a basic element in building SDN solutions.
	• OpenStack - This approach is a virtualization and orchestration platform designed to
	build scalable cloud environments and provide an IaaS solution. OpenStack is often
	used with Cisco ACI. Orchestration in networking is the process of automating the
	provisioning of network components such as servers, storage, switches, routers, and
	applications.
	• Other components - Other components include Interface to the Routing System
	(I2RS), Transparent Interconnection of Lots of Links (TRILL), Cisco FabricPath (FP),
	and IEEE 802.1aq Shortest Path Bridging (SPB).
![](../images/Screenshot%20from%202025-07-06%2012-19-09.png)
![](../images/Pasted%20image%2020250706121939.png)
![](../images/Screenshot%20from%202025-07-06%2012-19-55.png)- Flow Table - This table matches incoming packets to a particular flow and specifies the functions
that are to be performed on the packets. There may be multiple flow tables that operate in a
pipeline fashion.
•Group Table - A flow table may direct a flow to a Group Table, which may trigger a variety of
actions that affect one or more flows.
•Meter Table - This table triggers a variety of performance-related actions on a flow including the
ability to rate-limit the traffic.

- SDN Types
	- Controller-based SDN: 
		- Uses a centralized controller that has knowledge of all devices inthe network, as shown in the figure. The applications can interface with the controller responsible for managing devices and manipulating traffic flows throughout the network.
		- The Cisco Open SDN Controller is a commercial distribution of OpenDaylight
		- ![](../images/Screenshot%20from%202025-07-06%2012-22-27.png)
	- Policy-based SDN: Similar to controller-based SDN where a centralized controller has a view of all devices in the network,as shown in the figure. Policy-based SDN includes an additional Policy layer that operates at a higher level of abstraction.It uses built-in applications that automate advanced configuration tasks via a guided workflow and user-friendly GUI.No programming skills are required.Cisco APIC-EM is an example of this type of SDN.
	![](../images/Screenshot%20from%202025-07-06%2012-23-09.png)