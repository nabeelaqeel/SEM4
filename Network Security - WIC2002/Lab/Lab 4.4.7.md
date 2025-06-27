
![](../../res/4.4.7-lab---configure-secure-administrative-access.pdf)

iso image : https://software.cisco.com/download/home/286310700/type/282046477/release/Dublin-17.12.4b?i=!pp

### Basic Configuration
- R1
```
hostname R1
int g2/0
ip add 10.1.1.1 255.255.255.252
no sh

int g1/0
ip add 192.168.1.1 255.255.255.0
no sh

no ip domain-lookup

router ospf 1
network 192.168.1.0 0.0.0.255 area 0
network 10.1.1.0 0.0.0.3 area 0
passive-interface g1/0
```

- R2 
```
hostname R2
int g1/0
ip add 10.1.1.2 255.255.255.252
no sh

int g2/0
ip add 10.2.2.2 255.255.255.252
no sh

router ospf 1
network 10.1.1.0 0.0.0.3 area 0
network 10.2.2.0 0.0.0.3 area 0
```

- R3
```
hostname R3
int g2/0
ip add 10.2.2.1 255.255.255.252
no sh

int g1/0
ip add 192.168.3.1 255.255.255.0
no sh

router ospf 1
network 10.2.2.0 0.0.0.3 area 0
network 192.168.3.0 0.0.0.255 area 0
```

- Verify
```
sh ip ospf neighbor
```

- PC
```
ip 192.168.1.3 255.255.255.0 192.168.1.1
ip 192.168.3.3 255.255.255.0 192.168.3.1
```

> After configuring all these somehow i cannot ping from PC to default gateway 
> The solution is to add ip add to VLAN in the switch

> This might because I use layer3 switch where it doesnt support ping when it doesnt have ip

> I also change from layer 3 cable to layer 2 cable . It doesnt work on layer 3 cable

> if im ping from switch to router then it can work why??

- S1
```
int vlan 1
ip add 192.168.1.2 255.255.255.0
```

- S3
```
int vlan 1
ip add 192.168.3.2 255.255.255.0
```
---

### R1, R3

```
enable algorithm-type scrypt secret cisco12345
security passwords min-length 10

line console 0
password ciscoconpass
exec-timeout 0 0
login
logging synchronous

line aux 0
password ciscoauxpass
exec-timeout 0 0
login

line vty 0 4 
password ciscovtypass
exec-timeout 0 0
transport input telnet
login

```

> exec-timeout should be exec-timeout 5 0 
```

service password-encryption
banner motd $Unauthorzed access strictly prohibited!$
```

> default level 7


```
username user01 algorithm-type scrypt secret user01pass

line console 0
login local

```

```
ip domain-name netsec.com
username admin privilege 15 algorithm-type scrypt secret cisco12345

line vty 0 4
privilege level 15
login local 
transport input ssh

crypto key zeroize rsa

crypto key generate rsa general-keys modulus 1024
ip ssh version 2

sh ip ssh

ip ssh time-out 90
ip ssh authentication-retries 2

```
