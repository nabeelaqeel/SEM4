- R1
```
enable
configure terminal 

hostname R1
security passwords min-length 10
enable algorithm-type scrypt secret cisco12345

ip domain name netsec.com
username admin01 algorithm-type scrypt secret admin01pass 

interface GigabitEthernet2/0
ip address 172.16.3.1 255.255.255.0
no shutdown

interface GigabitEthernet1/0
ip address 209.165.200.225 255.255.255.248
no shutdown

crypto key generate rsa general-keys modulus 2048 

ip http server
ip http authentication local 

line con 0
exec-timeout 5 0 
logging synchronous 
login local

line vty 0 4
exec-timeout 5 0 
login local 
transport input ssh
```

- PC
```
ip 172.16.3.3 255.255.255.0 172.16.3.1
ip 192.168.1.3 255.255.255.0 192.168.1.1
ip 192.168.2.3 255.255.255.0 192.168.2.1

```

- ASA
```

```