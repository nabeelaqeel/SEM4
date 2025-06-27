# Module 13
![](../images/Pasted%20image%2020250509234758.png)

```
authentication port-control [auto | force-authorized(default) | force-unauthorized]
```

> [!NOTE]- 802.1X Configuration
> ```
> aaa new-model
> radius server NETSEC
> address ipv4 10.1.1.50 auth-port 1812 acct-port 1813
> key RADIUS-Pa55w0rd
> 
> aaa authentication dot1x default group radius
> dot1x system-auth-control
> 
> interface F0/1
> description Access Port
> switchport mode access
> authentication port-control auto
> dot1x pae authenticator
> ```

# Module 14

## Mitigate MAC Table Attack

> [!NOTE]- MAC flooding
> ```
> 1. The threat actor is connected to VLAN 10 and uses **macof** to rapidly generate many random source and destination MAC and IP addresses.
> 2. Over a short period of time, the switch’s MAC table fills up.
> 3. When the MAC table is full, the switch begins to flood all frames that it receives. As long as **macof** continues to run, the MAC table remains full and the switch continues to flood all incoming frames out every port associated with VLAN 10.
> 4. The threat actor then uses packet sniffing software to capture frames from any and all devices connected to VLAN 10.
> 
> Tool : macof
> ```

[!NOTE]- Mitigating
```
1.shutdown unused port
2.portsecurity

switchport port-security
switchport port-security [aging | mac-address | maximum | violation ]
switchport port-security mac-address [mac-address | sticky]
switchport port-security aging 
{ static | time <time> | type {absolute | inactivity}}
switchport port-security violation { protect | restrict | shutdown(default)}

NOTE : 
	maximum : default(1) , max depends on switch & IOS
	aging : time 0 - 1440 minutes : 0 = disable
	violation : if happen port = error-disabled state



show port-security
show port-security address
show switchport port-security int f0/1

SNMP:
mac address-table notification
```


![](../images/Pasted%20image%2020250510161037.png)
---

## Mitigate VLAN Attack
```
vlan attack 
1. Vlan Hopping
2. Double Tag Vlan 

Mitigate
1.


Private VLAN
1. promiscuous
2. isolated
3. community

PVLAN attack

mitigate PVLAN
use ACL
```

---
## Mitigate DHCP
```
1. DHCP starvation
2. DHCP spoofing : Rougue DHCP server . 
	1. Wrong dg
	2. Wrong DNS server
	3. Wrong IP

Mitigate
1. snooping 
	1. Deny Unauthorized DHCP server message
	2. Unauthorized DHCP client messages not adhering to the snooping binding table or rate limits
	3. DHCP relay-agent packets that include option-82 information on an untrusted port

Client Hardware Address (CHADDR)

Command:
ip dhcp snooping

interface f0/1
ip dhcp snooping trust

interface range f0/5 - 24
ip dhcp snooping limit rate 6

ip dhcp snooping vlan 5,10,50-52

show ip dhcp snooping
show ip dhcp snooping binding
```

---

## Mitigate ARP Attack

```
1.gratuitous ARP
2.unsolicited ARP reply

the attack basically change the dg

Tools : dsniff , Cain & Abel , ettercap , Yersinia
```


# Module 22

- PPDIOO : cisco network lifeocycle