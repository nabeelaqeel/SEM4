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
# SDN

# IDS , IPS
- File : `Network Security v1.0 - Module 11.pptx`