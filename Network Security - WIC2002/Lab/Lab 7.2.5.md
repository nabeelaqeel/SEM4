
- R1
```
int g0/0
no switchport
ip add 192.168.1.1 255.255.255.0
no sh

int g0/1
no switchport
ip add 10.1.1.1 255.255.255.252
no sh

no ip domain-lookup
ip route 0.0.0.0 0.0.0.0 10.1.1.2

security passwords min-length 10
enable algorithm-type sha256 secret cisco12345

line console 0
password ciscoconpass
exec-timeout 5 0
login
logging synchronous

line aux 0
password ciscoauxpass
exec-timeout 5 0
login

line vty 0 4
password ciscovtypass
exec-timeout 5 0
login

service password-encryption

do sh run | section line 

banner motd $Unathorized access strictly prohibited!$

username user01 algorithm-type sha256 secret user01pass

line console 0
login local

ip domain-name netsec.com

line vty 0 4
privilege level 15
login local 
transport input ssh

crypto key zeroize rsa

crypto key generate rsa general-keys modulus 1024
ip ssh version 2

line aux 0
login local
```

- R2
```
int g0/0
no switchport
ip add 10.1.1.2 255.255.255.252
no sh

int g0/1
no switchport
ip add 10.2.2.2 255.255.255.252
no sh

no ip domain-lookup
ip route 192.168.1.0 255.255.255.0 10.1.1.1
ip route 192.168.3.0 255.255.255.0 10.2.2.1
```

- R3
```
int g0/0
no switchport
ip add 192.168.3.1 255.255.255.0
no sh

int g0/1
no switchport
ip add 10.2.2.1 255.255.255.252
no sh

no ip domain-lookup
ip route 0.0.0.0 0.0.0.0 10.2.2.2

security passwords min-length 10
enable algorithm-type sha256 secret cisco12345

banner motd $Unathorized access strictly prohibited!$

---
AAA Server

username Admin01 privilege 15 algorithm-type sha256 secret Admin01pass

aaa new-model
aaa authentication login default local-case none

aaa authentication login SSH_LINES local
line vty 0 4
login authentication SSH_LINES

clock set 14:15:00 17 May 2025
show run | include timestamp
service timestamps bebug datetime msec

debug aaa authentication 
ssh -l Admin01 10.2.2.1
```