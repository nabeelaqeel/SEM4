- R1
```
ip access-list standard PERMIT-SNMP
permit 192.168.1.0 0.0.0.255

snmp-server view SNMP-RO iso included
snmp-server group SNMP-G1 v3 priv read SNMP-RO access PERMIT-SNMP

snmp-server user SNMP-ADMIN SNMP-G1 v3 auth sha Authpass priv aes 128 Encrypass
```

```
show snmp group
show snmp user
```

- R2
```
clock set 11:17:00 Apr 19 2025

ntp authentication-key 1 md5 NTPpassword
ntp trusted-key 1
ntp authenticate
ntp master 3
```

- R1,R3
```
debug ntp all

ntp authentication-key 1 md5 NTPpassword
ntp trusted-key 1
ntp authenticate
ntp server 10.1.1.2

undebug all
```

```
sh ntp ass
sh clock
```

- R1
```
service timestamps log datetime msec
logging host 192.168.1.3

logging trap warning

```

```
show logging
```