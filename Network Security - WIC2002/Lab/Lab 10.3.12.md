
![](../../images/Pasted%20image%2020250522111945.png)
- R1
```
int g0/0
no switchport
ip add 192.168.1.1 255.255.255.0
no shut

int g0/1
no switchport
ip add 10.1.1.1 255.255.255.252
no shut

ip route 0.0.0.0 0.0.0.0 10.1.1.2

security passwords min-length 10
ip domain-name netsec.com

crypto key generate rsa general-keys modulus 1024

username admin01 algorithm-type scrypt secret cisco12345

line console 0 
login local 
exec-timeout 5 0
logging synchronous

line aux 0
login local
exec-timeout 5 0

line vty 0 4
login local
transport input ssh
exec-timeout 5 0

enable algorithm-type scrypt secret class12345
```

- R2
```
int g0/0
no switchport
ip add 10.1.1.2 255.255.255.252
no shut

int g0/1
no switchport
ip add 10.2.2.2 255.255.255.252
no shut

ip route 192.168.1.0 255.255.255.0 10.1.1.1
ip route 192.168.3.0 255.255.255.0 10.2.2.1
ip route 192.168.33.0 255.255.255.0 10.2.2.1
```

- R3
```
int g0/1
no switchport
ip add 10.2.2.1 255.255.255.252
no shut

ip route 0.0.0.0 0.0.0.0 10.2.2.2

int g0/0
no switchport
no shut

int g0/0.3
encapsulation dot1q 3
ip add 192.168.3.1 255.255.255.0

int g0/0.33
encapsulation dot1q 33
ip add 192.168.33.1 255.255.255.0

zone security INSIDE
zone security CONFROOM
zone security INTERNET

class-map type inspect match-any INSIDE_PROTOCOLS
match protocol tcp
match protocol udp
match protocol icmp

class-map type inspect match-any CONFROOM_PROTOCOLS
match protocol http
match protocol https
match protocol dns

policy-map type inspect INSIDE_TO_INTERNET
class type inspect INSIDE_PROTOCOLS
inspect

policy-map type inspect CONFROOM_PROTOCOLS
class type inspect CONFROOM_PROTOCOLS
inspect

zone-pair security INSIDE_TO_INTERNET source INSIDE destination INTERNET
zone-pair security CONFROOM_TO_INTERNET source CONFROOM destination INTERNET

show zone-pair security

zone-pair security INSIDE_TO_INTERNET
service-policy type inspect INSIDE_TO_INTERNET
zone-pair security CONFROOM_TO_INTERNET
service-policy type inspect CONFROM_TO_INTERNET

show policy-map type inspect zone-pair

int g0/0.33
zone-member security CONFROOM

int g0/0.3
zone-member security INSIDE

int g0/1
zone-member security INTERNET

show zone security

policy-map type inspect inside
class class-default
pass

zone-pair security INSIDE source INSIDE destination INSIDE

show zone-pair security
```

- S3
```
int f3/1
sw mode tru

int f3/0
sw mode acc
sw acc vlan 3

int f3/2
sw mode acc 
sw acc vlan 33
```