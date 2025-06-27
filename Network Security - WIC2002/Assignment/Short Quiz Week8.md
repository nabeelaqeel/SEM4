# **Module 13 & 14 Security Questions**  

## **Module 13: Endpoint Security**  

1. What are the two key internal LAN elements that must be secured within an organization?  
   - Endpoints (workstations, laptops, mobile devices)  
   - Network infrastructure (switches, routers, servers)  

1. List three traditional host-based security measures used for endpoint protection.  
   - Antivirus/Anti-malware software  
   - Host-based firewalls  
   - Patch management and software updates  

1. Why is endpoint security more challenging in a “borderless network”?  
   - Due to the increased use of remote work, BYOD (Bring Your Own Device), and cloud services, endpoints are no longer confined to a traditional network perimeter, making them harder to monitor and secure.  

1. How does Network Access Control (NAC) improve endpoint security?  
   - NAC enforces security policies by checking device compliance before granting network access, ensuring only authorized and secure devices can connect.  

1. What is the main function of the 802.1X protocol in securing endpoints?  
   - It provides port-based authentication, ensuring only authorized devices can access the network.  

1. What are the roles of the supplicant, authenticator, and authentication server in 802.1X?  
   - Supplicant: The endpoint device requesting access.  
   - Authenticator: The network device (switch/WAP) controlling access.  
   - Authentication Server (RADIUS): Validates credentials and grants/denies access.  

1. What type of data does 802.1X use for communication between the supplicant and authenticator?  
   - EAP (Extensible Authentication Protocol) frames.  

1. What is a major benefit of using hardware or software encryption for local endpoint data?  
   - It protects sensitive data from unauthorized access even if the device is lost or stolen.  

1. Name two network-based tools used for endpoint protection in a borderless environment.  
   - Cisco Identity Services Engine (ISE)  
   - Next-Generation Firewalls (NGFW)  

1. What is the function of the Cisco Identity Services Engine (ISE) in endpoint security?  
   - It provides centralized authentication, authorization, and accounting (AAA), enforcing security policies across the network.  

---

## **Module 14: Layer 2 Security Considerations**  

1. Why is Layer 2 considered a vulnerable point in the OSI model?  
   - Because many attacks (MAC flooding, ARP poisoning, VLAN hopping) exploit Layer 2 protocols, which often lack built-in security.  

1. What is a MAC address table flooding attack and what does it target?  
   - An attacker floods a switch with fake MAC addresses, overflowing the MAC table and forcing the switch to act like a hub, allowing traffic sniffing.  

1. How does port security help defend against MAC address table attacks?  
   - It restricts which MAC addresses can use a port, preventing unauthorized devices from flooding the table.  

1. What is VLAN hopping, and how can it be mitigated?  
   - An attacker gains access to a different VLAN by exploiting double-tagging or switch spoofing. Mitigation includes disabling unused ports, using VLAN ACLs, and avoiding native VLANs for user traffic.  

1. What is DHCP spoofing and how is it prevented?  
   - An attacker provides fake DHCP responses to assign malicious gateway/DNS settings. Prevention includes DHCP snooping, which filters unauthorized DHCP servers.  

1. What is ARP poisoning, and what is one method to defend against it?  
   - An attacker sends fake ARP replies to redirect traffic. Defense includes Dynamic ARP Inspection (DAI) to validate ARP packets.  

1. What is the purpose of IP Source Guard (IPSG)?  
   - It prevents IP spoofing by allowing only verified IP-MAC bindings (based on DHCP snooping) to send traffic.  

1. How can you secure unused switch ports?
   - Disable them or configure them as access ports with port security to prevent unauthorized access.  

1. Which Spanning Tree Protocol (STP) features help protect against STP attacks?
   - BPDU Guard (blocks unauthorized BPDU packets)  
   - Root Guard (prevents rogue root bridge attacks)  

1. What Layer 2 attack targets the MAC address table, and what tool is commonly used for it?  
   - MAC flooding attack, commonly performed using macof (part of the dsniff toolkit).  
