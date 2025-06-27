- R1
```
enable
configure terminal 
hostname R1
security passwords min-length 10
enable secret algorithm-type scrypt cisco12345 
ip domain name netsec.com
!username admin01 algorithm-type scrypt secret cisco12345 

interface GigabitEthernet2/0
ip address 172.16.3.1 255.255.255.0
no shutdown

interface GigabitEthernet1/0
ip address 209.165.200.225 255.255.255.248
no shutdown

crypto key generate rsa general-keys modulus 1024 

ip http server

line con 0
exec-timeout 5 0 
logging synchronous 
!login local

line vty 0 4
exec-timeout 5 0 
!login local 
transport input ssh
end

copy running start
```

- ASA
```
show version
show file system
show flash 

write erase
show start
reload 


hostname NETSEC-ASA
domain-name netsec.com

passwd cisco
enable password class

clock set 2:23:00 feb 22 2025

int g0/1
nameif INSIDE
ip add 192.168.1.1 255.255.255.0
security-level 100
no shut

int g0/0
nameif OUTSIDE
ip add 209.165.200.226 255.255.255.248
security-level 0
no shut

int m0/0
sh
no ip 

http server enable
http 192.168.1.0 255.255.255.0 INSIDE

```

- kALI
```
sudo ifconfig eth0 192.168.1.4 netmask 255.255.255.0
sudo route add default gw 192.168.1.1

sudo ip addr add 192.168.1.10/24 dev eth0
sudo ip link set eth0 u
sudo ip route add default via 192.168.1.1
```