- ASA
```
route OUTSIDE 0.0.0.0 0.0.0.0 209.165.200.225

show route 


object network INSIDE-NET
subnet 192.168.1.0 255.255.255.0
nat (INSIDE,OUTSIDE) dynamic interface

show run object
show run nat
show mat 
show xlate

policy-map global_policy
class inspection_default
inspect icmp

show run policy-map

dhcpd address 192.168.1.5-192.168.1.100 INSIDE
dhcpd dns 209.165.201.2
dhcpd option 3 ip 192.168.1.1
dhcpd enable INSIDE

show run dhcpd

username admin password cisco12345
aaa authentication ssh console LOCAL

crypto key generate rsa modulus 2048
write mem

ssh 192.168.1.0 255.255.255.0 INSIDE
ssh 172.16.3.3 255.255.255.255 OUTSIDE
ssh timeout 10

int g0/2
ip add 192.168.2.1 255.255.255.0
nameif DMZ
security-level 70
no shut

object network DMZ-SERVER
host 192.168.2.3
nat (DMZ,OUTSIDE) static 209.165.200.227


access-list OUTSIDE-DMZ permit ip any host 192.168.2.3
access-group OUTSIDE-DMZ in interface OUTSIDE

clear nat counters
show nat
show xlate
```