Kali
```
sudo ifconfig eth1 192.168.10.2 netmask 255.255.255.0
sudo route add default gw 192.168.10.1

sudo dhclient eth1
```

- Metasploit
```
sudo ifconfig eth1 192.168.100.3 netmask 255.255.255.0
sudo route add default gw 192.168.100.1

sudo dhclient eth1
```

- Parrot
```
sudo ifconfig eth1 192.168.200.3 netmask 255.255.255.0
sudo route add default gw 192.168.200.1

sudo dhclient eth1
```

```
sudo ip addr flush dev eth1
```


- VPN
```
wg genkey | tee privatekey | wg pubkey > publickey

```

```
[Interface]
PrivateKey = UL4bcLo++etnxw/bT4mI3pV6av9YJlwW22lzodXjv3E=
Address = 10.10.10.2/24

[Peer]
PublicKey = L4sV24O5LY9XIxB4uSLGkfZA2WEam9haMspSvYOpM2w=
Endpoint = 192.168.59.168:51820
AllowedIPs = 0.0.0.0/0
```

```
sudo nano /etc/wireguard/wg0.conf
```

```
sudo wg show
```

```
sudo wg-quick up wg0 
```

```
wg genkey | tee private.key | wg pubkey > public.key
```

testing whether has error or not