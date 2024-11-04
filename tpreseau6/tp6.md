️ Prouvez que...

une machine du LAN1 peut joindre internet (ping un nom de domaine)
```c
[root@dhcp ~]# ping ynov.com
PING ynov.com (184.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=1 ttl=254 time=514 ms 64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=2 ttl=254 time=513 ms 64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=3 ttl=254 time=515 ms
C
ynov.com ping statistics
4 packets transmitted, 3 received, 25% packet loss, time 3097ms rtt min/avg/max/mdev = 512.785/514.131/515.453/1.089 ms
[root@dhcp ~]#
```
une machine du LAN2 peut joindre internet (ping nom de domaine)
```c
[root@localhost ~]# ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=1 ttl=254 time=516 ms 64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=2 ttl=254 time=514 ms ^C64 bytes from 104.26.11.233: icmp_seq=3 ttl=254 time=514 ms
ynov.com ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 2066ms rtt min/avg/max/mdev = 513.719/514.678/515.957/8.941 ms [root@localhost ~]#
```
une machine du LAN1 peut joindre
```c
PING 10.6.2.12 (10.6.2.12) 56(84) bytes of data.
64 bytes from 10.6.2.12: icmp_seq=1 ttl=63 time=1.51 ms 64 bytes from 10.6.2.12: icmp_seq=2 ttl=63 time=1.20 ms 64 bytes from 10.6.2.12: icmp_seq=3 ttl=63 time=1.19 ms
c
--- 10.6.2.12 ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 2068ms rtt min/avg/max/mdev = 1.187/1.298/1.509/0.148 ms
```
une machine du LAN2 (ping une adresse IP)
```c
[root@dns ~]# ping 10.6.1.253
PING 10.6.1.253 (10.6.1.253) 56(84) bytes of data.
64 bytes from 10.6.1.253: icmp_seq=1 ttl=63 time=0.968 ms
64 bytes from 10.6.1.253: icmp_seq=2 ttl=63 time=1.18 ms
64 bytes from 10.6.1.253: icmp_seq=3 ttl=63 time=1.07 ms
C
--- 10.6.1.253 ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 2012ms rtt min/avg/max/mdev = 0.968/1.873/1.184/0.088 ms
```


☀️ Prouvez que...

le client a bien récupéré une adresse IP en DHCP
avec un ip a le mot-clé dynamic doit être écrit sur la ligne qui contient l'adresse IP
(y'a pas ce mot-clé quand tu définis une IP statique)
```c
ip a
2: enp0s8: <BROADCAST, MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP gr oup default qlen 1000
link/ether 08:00:27:dc:13:14 brd ff:ff:ff:ff:ff:ff
inet 10.6.1.37/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s8 valid_lft 598sec preferred_lft 598sec
inet6 fe80::a00:27ff:fedc:1314/64 scope link valid_lft forever preferred_lft forever
jinkyu@Jclient1:~$
```
vous avez bien 1.1.1.1 en DNS
commande dans le mémo pour 
consulter l'adresse IP du serveur DNS connu
```c
jinkyu@Jclient1:~$ nmcli device show enp0s8 | grep DNS IP4.DNS[1]:
1.1.1.1
```
vous avez bien la bonne passerelle indiquée
idem, dans le mémo, pour afficher l'adresse de la passerelle 
actuellement configurée :
```c
jinkyu@Jclient1:~$ ip route
default via 10.6.1.254 dev enp0s8 proto dhcp src 10.6.1.37 metric 100 10.6.1.0/24 dev enp0s8 proto kernel scope link src 10.6.1.37 metric 100
```
que ça ping un nom de domaine public sans problème magueule
```c
jinkyu@Jclient1:~$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=254 time=516 ms 64 bytes from 172.67.74.226: icmp_seq=2 ttl=254 time=420 ms 64 bytes from 172.67.74.226: icmp_seq=3 ttl=254 time=433 ms ^C
--- ynov.com ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 2151ms rtt min/avg/max/mdev = 420.351/456.354/515.927/42.428 ms jinkyu@Jclient1:~$
```


# III. LAN serveurzzzz

## 1. Serveur Web

### ☀️ Déterminer sur quel port écoute le serveur NGINX

```c
[root@web ~]# sudo ss -tuln | grep 80
tcp LISTEN Ø
tcp LISTEN Ø
[root@web ~]#
511
511
0.0.0.0:80 [::]:80
0.0.0.0:
[::]: *
```
### ☀️ Ouvrir ce port dans le firewall
```c
[root@web ~]# sudo firewall-cmd --permanent --add-port=80/tcp
success
[root@web ~]# sudo firewall-cmd --reload
success
[root@web ~]# sudo firewall-cmd --list-all public (active)
target: default
icmp-block-inversion: no
interfaces: enp0s9
sources:
services: cockpit dhcpv6-client ssh
ports: 80/tcp
protocols:
forward: yes masquerade: no forward-ports: source-ports: icmp-blocks: rich rules: [root@web ~]#
```
### ☀️ Visitez le site web !
```c
[root@web ~]# curl http://10.6.2.11 | head -5 % Total % Received % Xferd Average Speed Dload Upload 1<!doctype html> 0 0 0 0 <html>
00 7620 100 7620 0 0 930k <head>
<meta charset='utf-8'>
0
Time Total Spent
Time
Time Current Left Speed
0
0 --:--:-- --:--:-- --:--:--
<meta name="viewport" content="width=device-width, initial-scale=1'>
930k
[root@web ~]#
```

# III. 2. Serveur DNS
## 4. Analyse du service
### ☀️ Déterminer sur quel(s) port(s) écoute le service BIND9

```c
[jinq@dns ~]$ sudo ss -tuln | grep :53
udp   UNCONN 0      0          10.6.2.12:53        0.0.0.0:*
udp   UNCONN 0      0          10.6.2.12:53        0.0.0.0:*
udp   UNCONN 0      0          127.0.0.1:53        0.0.0.0:*
udp   UNCONN 0      0          127.0.0.1:53        0.0.0.0:*
udp   UNCONN 0      0              [::1]:53           [::]:*
udp   UNCONN 0      0              [::1]:53           [::]:*
tcp   LISTEN 0      10         127.0.0.1:53        0.0.0.0:*
tcp   LISTEN 0      10         127.0.0.1:53        0.0.0.0:*
tcp   LISTEN 0      10         10.6.2.12:53        0.0.0.0:*
tcp   LISTEN 0      10         10.6.2.12:53        0.0.0.0:*
tcp   LISTEN 0      10             [::1]:53           [::]:*
tcp   LISTEN 0      10             [::1]:53           [::]:*
```

isolez la ligne intéressante avec un ... | grep <PORT> une fois que vous avez repéré le port
bon normalement vous l'avez vu dans la conf, non ? :d
### ☀️ Ouvrir ce(s) port(s) dans le firewall
```c
[jinq@dns ~]$ sudo firewall-cmd --add-port=53/udp --permanent
success
[jinq@dns ~]$ sudo firewall-cmd --add-port=53/tcp --permanent
success
[jinq@dns ~]$ sudo firewall-cmd --reload
success
```
5. Tests manuels
### ☀️ Effectuez des requêtes DNS manuellement depuis le serveur 
DNS lui-même dans un premier temps
### cette commande demande à 10.6.2.12 à quelle IP correspond web.tp6.b1
#### ☀️ dig web.tp6.b1 @10.6.2.12
```c
[jinq@dns ~]$ dig web.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> web.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 24934
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: b9e619d4f497f6db010000006716102199fcbb725756a748 (good)
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

;; Query time: 2 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:26:09 CEST 2024
;; MSG SIZE  rcvd: 83
```

# lui doit fonctionner aussi
#### ☀️dig dns.tp6.b1 @10.6.2.12
```c

[jinq@dns ~]$ dig dns.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> dns.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 40278
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 8fe95ca2eaa87ffb0100000067161072b4ad2bd8224fa4c9 (good)
;; QUESTION SECTION:
;dns.tp6.b1.                    IN      A

;; ANSWER SECTION:
dns.tp6.b1.             86400   IN      A       10.6.2.12

;; Query time: 3 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:27:30 CEST 2024
;; MSG SIZE  rcvd: 83
```

# et ça aussi dukou !
#### ☀️ dig ynov.com @10.6.2.12

```c
[jinq@dns ~]$ dig ynov.com @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> ynov.com @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 62569
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: fdb973b47d216c6d010000006716138aa60c9888e9c6f5c5 (good)
;; QUESTION SECTION:
;ynov.com.                      IN      A

;; ANSWER SECTION:
ynov.com.               300     IN      A       104.26.10.233
ynov.com.               300     IN      A       104.26.11.233
ynov.com.               300     IN      A       172.67.74.226

;; Query time: 1284 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:40:42 CEST 2024
;; MSG SIZE  rcvd: 113
```

#### et on devrait aussi pouvoir faire l'inverse en ajoutant -x :
#### demander quel est le nom qui correspond à une IP donnée
### dig -x 10.6.2.11 @10.6.2.12
```c
[jinq@dns ~]$ dig -x 10.6.2.11 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.11 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 56082
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 534ed90bc236aec701000000671613b6db01d5c676d92fa8 (good)
;; QUESTION SECTION:
;11.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
11.2.6.10.in-addr.arpa. 86400   IN      PTR     web.tp6.b1.

;; Query time: 2 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:41:26 CEST 2024
;; MSG SIZE  rcvd: 103
```
### dig -x 10.6.2.12 @10.6.2.12
```c
[jinq@dns ~]$ dig -x 10.6.2.12 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.12 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 6135
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 376ef81f586ce4b001000000671613dc9ca41bbde357bbce (good)
;; QUESTION SECTION:
;12.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
12.2.6.10.in-addr.arpa. 86400   IN      PTR     dns.tp6.b1.

;; Query time: 1 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Mon Oct 21 10:42:04 CEST 2024
;; MSG SIZE  rcvd: 103
```

☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1

```c
jinkyu@Jclient1:~$ dig @10.6.2.12 web.tp6.b1

; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> @10.6.2.12 web.tp6.b1
; (1 server found)
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 42594
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: e06fc983fd8897ce0100000067161dc071b540b76c4815a0 (good)
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

;; Query time: 2 msec
;; SERVER: 10.6.2.12#53(10.6.2.12) (UDP)
;; WHEN: Mon Oct 21 11:24:16 CEST 2024
;; MSG SIZE  rcvd: 83

```

pour obtenir l'adresse IP qui correspond au nom web.tp6.b1
### ☀️ Capturez une requête DNS et la réponse de votre serveur


```c
jinkyu@Jclient1:~$ sudo tcpdump -w toto.pcap -i enp0s8
tcpdump: listening on enp0s8, link-type EN10MB (Ethernet), snapshot length 262144 bytes
```
[text](../../Documents/toto1.pcap)

## 3. Serveur DHCP
### vérifiez que vous avez bien 10.6.2.12 comme serveur DNS à contacter
```c
jinkyu@jinkyu-VirtualBox:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s8)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 10.6.2.12
       DNS Servers: 10.6.2.12
        DNS Domain: jin1
```

### Vous devriez pouvoir visiter http://web.tp6.b1 avec le navigateur, ça devrait fonctionner sans aucune autre action.
```c
jinkyu@jinkyu-VirtualBox:~$ ping web.tp6.b1
PING web.tp6.b1 (10.6.2.11) 56(84) bytes of data.
64 bytes from web.tp6.b1 (10.6.2.11): icmp_seq=1 ttl=63 time=1.56 ms
64 bytes from web.tp6.b1 (10.6.2.11): icmp_seq=2 ttl=63 time=0.696 ms
64 bytes from web.tp6.b1 (10.6.2.11): icmp_seq=3 ttl=63 time=0.758 ms
64 bytes from web.tp6.b1 (10.6.2.11): icmp_seq=4 ttl=63 time=0.872 ms
^C
--- web.tp6.b1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3082ms
rtt min/avg/max/mdev = 0.696/0.972/1.563/0.346 ms
```

Ca a bien marché avec le navigateur 