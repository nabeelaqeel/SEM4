- Reconnaissance
- Weaponization
- Delivery
- Exploitation
- Installation
- Command & Control
- Actions on Objectives

### Reconnaissance
Tools : 
- https://github.com/laramies/theHarvester
- https://hunter.io/
- https://osintframework.com/

### Weaponization
Article : 
- https://www.trustedsec.com/blog/intro-to-macros-and-vba-for-script-kiddies/
- https://www.kaspersky.com/resource-center/threats/deep-web
- https://attack.mitre.org/tactics/TA0011/

### Delivery
Article :
- https://www.csoonline.com/article/3534693/cybercriminal-group-mails-malicious-usb-dongles-to-targeted-companies.html
Attack :
- Watering hole attack
- drive-by download

### Exploitation
Term :
- Lateral movement
	-  techniques that a malicious actor uses after gaining initial access to the victim's machine to move deeper into a network to obtain sensitive data.
- Zero day
	- unknown exploit in the wild that exposes a vulnerability in software or hardware and can create complicated problems well before anyone realizes something is wrong

Article :
- https://tryhackme.com/room/owasptop10

### Installation
Article :
- https://www.offensive-security.com/metasploit-unleashed/persistent-backdoors/
- https://www.microsoft.com/security/blog/2021/02/11/web-shell-attacks-continue-to-rise/

Tools :
- sc.exe
- https://www.offensive-security.com/metasploit-unleashed/meterpreter-backdoor/
- https://attack.mitre.org/software/S0075/
- https://attack.mitre.org/techniques/T1036/

Technique :
- [Creating or modifying Windows services](https://attack.mitre.org/techniques/T1543/003/)
- [Registry Run Keys / Startup Folder persistence](https://attack.mitre.org/techniques/T1547/001/)
- [Timestomping](https://attack.mitre.org/techniques/T1070/006/)

Learn :
- https://tryhackme.com/room/windowslocalpersistence

### Command & Control
- C&C or C2 Beaconing
	-  type of malicious communication between a C&C server and malware on the infected host
-  IRC (Internet Relay Chat) was the traditional C2 channel used by attackers

Attack 
- DNS Tunneling.

### Actions on Objective (Exfiltration) 
Achieve
- Collect the credentials from users.
- Perform privilege escalation (gaining elevated access like domain administrator access from a workstation by exploiting the misconfiguration).
- Internal reconnaissance (for example, an attacker gets to interact with internal software to find its vulnerabilities).
- Lateral movement through the company's environment.
- Collect and exfiltrate sensitive data.
- Deleting the backups and shadow copies. Shadow Copy is a Microsoft technology that can create backup copies, snapshots of computer files, or volumes. 
- Overwrite or corrupt data.
### Reference
- https://tryhackme.com/room/cyberkillchainzmt

