![](../../res/4.4.9-lab---configure-network-devices-with-ssh.pdf)
![](../../images/Pasted%20image%2020250410175152.png)

- R1
```
int g1/0
ip add 192.168.1.1 255.255.255.0
```

- S1
```
int vlan 1
ip add 192.168.1.11 255.255.255.0
no shut
ip default-gateway 192.168.1.1
```

- PC
```
ip 192.168.1.254 255.255.255.0 192.168.1.1
```

---
 - R1
```
hostname R1
no ip domain-lookup

enable algorithm-type scrypt secret class

line console 0
password cisco
exec-timeout 0 0
login
logging synchronous

line vty 0 4 
password cisco
exec-timeout 0 0
transport input telnet
login

service password-encryption
banner motd $Unauthorzed access strictly prohibited!$

exit 
copy run start
```

---

### Configured Router SSH access


```
ip domain-name r1.com

username admin privilege 15 algorithm-type sha256 secret Adm1nP@55 

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

---
### SSH Switch
- S1
```
no ip domain-lookup

enable algorithm-type sha256 secret class

line console 0
password cisco
exec-timeout 0 0
login
logging synchronous

line vty 0 4 
password cisco
exec-timeout 0 0
transport input telnet
login

service password-encryption
banner motd $Unauthorzed access strictly prohibited!$

exit
copy run start
```

```
ip domain-name s1.com

username admin privilege 15 algorithm-type sha256 secret Adm1nP@55 

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
