- R1,R2,R3
```
no ip domain lookup

enable algorithm-type sha256 secret cisco12345

username user01 algorithm-type sha256 secret user01pass

username admin privilege 15 algorithm-type sha256 secret cisco12345 ip domain-name netsec.com

line con 0
login local
logging synchronous 
exec-timeout 5 0

line aux 0 
login local
exec-timeout 5 0

line vty 0 4   
login local 
exec-timeout 5 0
transport input ssh

ip domain-name netsec.com
crypto key generate rsa general-key modulus 1024
ip ssh version 2
```

- VM
```
cd ~/lab.support.files/scripts
./configure_as_static.sh

ip addr

ping -c 4 192.168.1.1

ssh -l user01 192.168.1.1


```


- R1ter
```
aaa new-model
aaa authentication login default group radius none

radius server Netsec
add ipv4 192.168.1.11
key $trongPass

test aaa group radius RadUser RadUserPass legacy

show radius server-group radius

radius server Netsec
add ipc4 192.168.1.11 auth-port 1812 acct-port 1813

test aaa group radius RadUser RadUserpass legacy

aaa authentication login SSH_LINES group radius

line vty 0 4
login authentication SSH_LINES
```

```
sudo systemctl start freeradius.service
sudo systemctl status freeradius.service
```

