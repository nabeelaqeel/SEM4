### Basic Configuration
- R1
```
hostname R1
int g0/1
no switchport
ip add 10.1.1.1 255.255.255.252
no sh

int g0/0
no switchport
ip add 192.168.1.1 255.255.255.0
no sh

int range g0/1
ip ospf network point-to-point

no ip domain-lookup

router ospf 1
network 192.168.1.0 0.0.0.255 area 0
network 10.1.1.0 0.0.0.3 area 0
passive-interface g0/0
```

- R2 
```
hostname R2
int g0/0
no switchport
ip add 10.1.1.2 255.255.255.252
no sh

int g0/1
no switchport
ip add 10.2.2.2 255.255.255.252
no sh

router ospf 1
network 10.1.1.0 0.0.0.3 area 0
network 10.2.2.0 0.0.0.3 area 0

int range g0/0 - 1
ip ospf network point-to-point
```

- R3
```
hostname R3
int g0/1
no switchport
ip add 10.2.2.1 255.255.255.252
no sh

int g0/0
no switchport
ip add 192.168.3.1 255.255.255.0
no sh

router ospf 1
network 10.2.2.0 0.0.0.3 area 0
network 192.168.3.0 0.0.0.255 area 0
passive-interface g0/0

int range g0/1
ip ospf network point-to-point
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

- S1
```
hostname S1

int vlan 1
ip add 192.168.1.2 255.255.255.0
no shut
```

- S3
```
hostname S3

int vlan 1
ip add 192.168.3.2 255.255.255.0
no shut
```



---



- R1,R2,R3
```
key chain NetAcad
key 1

key-string NetSeckeystring
cryptographic-algorithm hmac-sha-256
```

```
int g0/0
ip ospf authentication key-chain NetAcad

int g0/1
ip ospf authentication key-chain NetAcad
```

- Verify
```
sh ip ospf neighbor
```


### Issue

When i show run it just show this only
```
R1#sh run
Building configuration...

Current configuration : 3729 bytes
!
! Last configuration change at 11:40:26 UTC Sat Apr 19 2025
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname R1
!
boot-start-marker
boot-end-marker
!
!
!
no aaa new-model
!
!
!
!
```

Fix it 
```
terminal length 0
show running-config
```