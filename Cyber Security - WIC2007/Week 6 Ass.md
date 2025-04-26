# MISSION SUMMARY
At 0300 hours on April 22, 2025, the hacktivist group R00TK1T successfully breached Maxis's backend infrastructure through a sophisticated supply chain attack. The attackers exploited vulnerabilities in a third-party vendor's system to gain unauthorized access to critical backend configurations. This incident has raised significant concerns regarding third-party risk management and SSH key security protocols.

Initial investigation reveals that the attackers leveraged compromised credentials from the vendor to access Maxis's configuration management system. The breach has highlighted critical vulnerabilities in our supply chain security and the urgent need for enhanced vendor access controls.

# MISSION OBJECTIVES
- Conduct appropriate investigation and research on the attack by R00TK1T
- Reconstruct the cyberattack using the 7 stages of the Cyber Kill Chain (CKC)
- Identify key Indicators of Compromise (IoCs) and attack vectors
- Propose practical mitigation strategies
- Present a 7-minute tactical briefing to CDU Command
📡 Tactical Communication Protocol
As a CTRT operative, you are expected to maintain tactical professionalism in your briefing. Use appropriate cybersecurity terminology and incident response language:

- Use precise terminology: Example - "Threat actor achieved initial access via compromised vendor SSH credentials" instead of "They got in through a vendor"
- Time references: Use "T-minus" for pre-incident, "T-zero" for incident detection, "T-plus" for post-detection
- Status indicators: Use "CONFIRMED" for verified intel, "PROBABLE" for high confidence assessments, "POSSIBLE" for unverified intel
- Threat levels: Reference using DEFCON-style classifications (1-5, where 1 is most severe)
- Asset references: Use designated codenames for critical infrastructure components (e.g., "TELCON-1" for primary telecom control system)


Chronology
1. 28 Jan 2024 : Announced to attack 
	- ![](../images/Pasted%20image%2020250426210952.png)
2. 30th January : Aminia , local Malaysian network solution and system integrator : screenshot Aminia's backend system in Telegram : no sensitive data leaked
	- ![](../images/Pasted%20image%2020250426210712.png)
	- Meanwhile, Aminia has noted on its corporate website (which somehow safe from the attack) that it also provides custom hardware to telcos. Maxis and TM appear to be among their main partners based on the information provided by the website
	- A quick search online reveals that they supply enterprise routers for fibre broadband. Some of their routers include MA-131 and MA-141 which come with a built-in backup 4G modem and can easily be obtained at popular online marketplaces.
3. 5th Feb : deface YouTutor's website
	- ![](../images/Pasted%20image%2020250426210459.png)
	- ![](../images/Pasted%20image%2020250426210521.png)
	- R00TK1T claimed that it contained plenty of personal information including name, addresses, phone numbers, and many more. We can confirm that the sample data not only contained those details but also featured a substantial amount of users in it
4. Maxis : screenshot backend : no abnormal within internal system : involve 3rd party vendor
5. 7.31pm : Infiltrated Maxis employee's dashboard : threaten to shutdown their system, expose sensitive data if Maxis doesn't acknowledge
6. 9.31pm : breach Kulim's Network bypass firewall , factory reset Agrotech-related system

Chronology  Maxis
1. [Maxis](https://soyacincau.com/tag/maxis/) has responded to [the claim made](https://soyacincau.com/2024/02/05/maxis-yoututor-r00tk1t-cyberattack/) by the [international hacker group R00TK1T](https://soyacincau.com/tag/r00tk1t/). The telco said that its investigation did not find anything abnormal within its internal system but it did identify an incident involving third-party vendor systems.
	- ![](../images/Pasted%20image%2020250426205721.png)
	- Maxis Message : 
		- Earlier today Maxis received a report alleging a cybersecurity breach. We immediately launched an investigation to determine the validity.

		- While we did not identify anything related to our own systems, we identified a suspected incident involving unauthorised access to one of our third-party vendor systems that resides outside of Maxis’ internal network environment. We are working with them to investigate further and have also informed the relevant authorities.

		- Our customers’ privacy and security are of the utmost importance to us, and our ongoing priority is a thorough assessment and containment. Additional defence measures are also being put in place to enhance the robustness of our systems with a view to reducing further risk. We will continue to provide necessary updates on developments.

2. At 7:31pm yesterday, R00TK1T claimed to have infiltrated what appears to be one of Maxis’ employee dashboards to prove that their systems are not as impenetrable as they seem. They issued another threat to shut down their systems and expose precious data and vulnerability every two hours if Maxis fails to acknowledge their successful breach.

	- ![](../images/Pasted%20image%2020250426205045.png)
	- ![](../images/Pasted%20image%2020250426205508.png)
	- ![](../images/Pasted%20image%2020250426205532.png)
https://thecyberexpress.com/maxis-berhad-cyberattack/
https://cybernage.com/r00tk1t-cyberattacks-malaysia/
https://soyacincau.com/2024/02/06/r00tk1t-claims-infiltrated-maxis-kulim-network-threatens-further-attacks-malaysia-xrs/

# CYBER KILL CHAIN RECONSTRUCTION

1. RECONNAISSANCE (T-minus 14d):

	- CONFIRMED: R00TK1T mapped Maxis’s third-party attack surface, focusing on Vendor-X (codenamed "GATEKEEPER").
	- PROBABLE: Open-source intel (GitHub, Shodan) exploited to identify outdated SSH key management tools.
	- https://www.sec.gov/search-filings
		- https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&CIK=0001285136&owner=include&count=40&hidefilings=0
	- https://www.cisa.gov/news-events/cybersecurity-advisories
	- https://cve.mitre.org/cve/search_cve_list.html

# Introduction
A common rootkit definition is a type of malware program that enables cyber criminals to gain access to and infiltrate data from machines without being detected[1]. 


# Reference
1. https://www.sangfor.com/blog/cybersecurity/r00tk1t-hacking-group-malaysia-needs-stronger-cybersecurity
2. https://www.fortinet.com/resources/cyberglossary/rootkit