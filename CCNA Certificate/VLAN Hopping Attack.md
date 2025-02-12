### 2 Methods
- Double Tagging
- Switch Spoofing

### Double Tagging
![VLAN Security and Design (3.3) > Cisco Networking Academy's Introduction to  VLANs | Cisco Press](https://www.ciscopress.com/content/images/chap3_9781587133183/elementLinks/03fig29_alt.jpg)

### How to Prevent VLAN Hopping (Double Tagging)
1. Avoid Using Native VLANs on Trunk Ports
	- Set the native VLAN to an unused VLAN instead of VLAN 10 or VLAN 20.
2. Explicitly Tag All Trunk Traffic
	- Configure trunk ports to require tagging for all VLANs, preventing untagged packets from being forwarded.
3. Use VLAN Access Control Lists (ACLs)
	- Apply ACLs to restrict which devices can send packets to VLANs.
4. Disable Dynamic Trunking Protocol (DTP)
	- Manually configure trunk ports instead of allowing auto-negotiation, reducing attack vectors.

### Switch spoofing

Switch spoofing occurs when the attacker sends [Cisco's Dynamic Trunking Protocol](https://study-ccna.com/dynamic-trunking-protocol-dtp-cisco/) (DTP) packets to negotiate a trunk with a switch. It is possible only when using the dynamic auto or dynamic desirable default switch modes. Once there is a trunk connected to the computer, the attacker gains access to all VLANs. This is a misconfiguration as interfaces should not be configured to use the dynamic switch port modes.
