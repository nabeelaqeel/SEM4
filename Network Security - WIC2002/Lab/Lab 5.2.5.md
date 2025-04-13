![](../../res/5.2.5-lab---configure-administrative-roles.pdf)

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

### Configure Administrative Roles
- R1,R3
```
aaa new-model
enable secret cisco12345

enable view

parser view admin1
secret admin1pass
commands exec include all show
commands exec include all config terminal
commands exec include all debug

enable view admin1
admin1pass
```

```
enable view
pass : cisco12345

parser view admin2
secret admin2pass

command exec include all show 
```

```
enable view
pass : cisco12345

parser view tech
secret techpasswd

command exec include show version 
command exec include show interface
command exec include show ip int br
command exec include show parser view
```

- Verify 
```
show parser view
```