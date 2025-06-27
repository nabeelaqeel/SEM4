![](../../images/Pasted%20image%2020250529091930.png)

- R1
```
int g1/0
ip add 192.168.1.1 255.255.255.0
no shut

int g2/0
ip add 10.1.1.1 255.255.255.252
no shut

router ospf 101
network 192.168.1.0 0.0.0.255 area 0
network 10.1.1.0 0.0.0.3 area 0
```

- R2
```
int g1/0
no switchport
ip add 10.1.1.2 255.255.255.252
no shut

int g2/0
no switchport
ip add 10.2.2.2 255.255.255.252
no shut


router ospf 101
network 10.1.1.0 0.0.0.3 area 0
network 10.2.2.0 0.0.0.3 area 0
```

- R3
```
int g2/0
no switchport
ip add 10.2.2.1 255.255.255.252
no shut

int g1/0
no switchport
ip add 192.168.3.1 255.255.255.0
no shut

router ospf 101
network 192.168.3.0 0.0.0.255 area 0
network 10.2.2.0 0.0.0.3 area 0

```

- R1 , R3
```
security passwords min-length 10
enable algorithm-type scrypt secret cisco12345

username admin01 algorithm-type scrypt secret cisco12345

line console 0
login local
exec-timeout 5 0 
logging synchronous

ip domain-name netsec.com
crypto key generate rsa general-key modulus 2048
ip ssh version 2

line vty 0 4
login local
exec-timeout 5 0
transport input ssh

crypto isakmp enable
crypto isakmp policy 10
hash sha
authentication pre-share
group 24
lifetime 3600
encryption aes 256

crypto isakmp key cisco123 address 10.2.2.1

crypto ipsec transform-set 50 esp-aes 256 esp-sha-hmac
crypto ipsec security-association lifetime seconds 1800

access-list 101 permit 101 192.168.1.0 0.0.0.255 192.168.3.0 0.0.0.255

crypto map CMAP 10 ipsec-isakmp
match address 101
set peer 10.2.2.1
set pfs group24
set transform-set 50
set security-association lifetime seconds 900

int g2/0
crypto map CMAP

show crypto ipsec transform-set
show crypto map
```


- R3
```
crypto isakmp enable
crypto isakmp policy 10
hash sha
authentication pre-share
group 24
lifetime 3600
encryption aes 256

crypto isakmp key cisco123 address 10.1.1.1

crypto ipsec transform-set 50 esp-aes 256 esp-sha-hmac
crypto ipsec security-association lifetime seconds 1800

access-list 101 permit 101 192.168.3.0 0.0.0.255 192.168.1.0 0.0.0.255

crypto map CMAP 10 ipsec-isakmp
match address 101
set peer 10.1.1.1
set pfs group24
set transform-set 50
set security-association lifetime seconds 900

int g2/0
crypto map CMAP

show crypto ipsec transform-set
show crypto map
show crypto isakmp sa
```
