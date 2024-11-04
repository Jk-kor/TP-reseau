# Serveur Web

### 🌞 Lister les ports en écoute sur la machine
```c
[jinq@web ~]$ sudo ss -tuln | grep ':80'
tcp   LISTEN 0      511          0.0.0.0:80        0.0.0.0:*
tcp   LISTEN 0      511             [::]:80           [::]:*
```

### 🌞 Ouvrir le port dans le firewall de la machine
```c
[jinq@web ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 80/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
  ```


### 🌞 Vérifier que ça a pris effet

#### faites un ping vers sitedefou.tp7.b1
```c
jinkyu@client1:~$ ping sitedefou.tp7.b1
PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=0.551 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=0.345 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=0.305 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=4 ttl=64 time=0.560 ms
^C
--- sitedefou.tp7.b1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3118ms
rtt min/avg/max/mdev = 0.305/0.440/0.560/0.116 ms
```

#### visitez http://sitedefou.tp7.b1
```c
jinkyu@client1:~$ curl http://sitedefou.tp7.b1
meow !
```
vous devriez avoir la page "meow !" quand vous visitez le site

# D. Analyze

### 🌞 Capture tcp_http.pcap
```
jinkyu@client1:~$ sudo tcpdump -i enp0s8 tcp port 80 -w tcp_http.pcap
```
[text](tcp_http.pcap)

### 🌞 Voir la connexion établie

```c
jinkyu@client1:~$ ss -t -a | grep http
ESTAB     0      0               10.7.1.101:33318            10.7.1.11:http
```


# 2. On rajoute un S

### 🌞 Lister les ports en écoute sur la machine
```c
[jinq@web ~]$ sudo ss -tuln | grep ':443'
tcp   LISTEN 0      511        10.7.1.11:443       0.0.0.0:*
```

🌞 Gérer le firewall

ouvrir le nouveau port sur lequel NGINX écoute pour HTTPS
```c
[jinq@web ~]$ sudo firewall-cmd --permanent --add-port=443/tcp
success
[jinq@web ~]$ sudo firewall-cmd --reload
^[[Asuccess
[jinq@web ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 443/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
[jinq@web ~]$
```

fermer l'ancien port qui était utilisé pour HTTP
```c
[jinq@web ~]$ sudo firewall-cmd --permanent --remove-port=80/tcp
success
```


🌞 Capture tcp_https.pcap
[text](capture_https.pcap)
```c
jinkyu@client1:~$ sudo tcpdump -i enp0s8 tcp port 443 -w capture_https.pcap
tcpdump: listening on enp0s8, link-type EN10MB (Ethernet), snapshot length 262144 bytes
^C38 packets captured
38 packets received by filter
0 packets dropped by kernel
```


# III. Serveur VPN

### 🌞 Prouvez que vous avez bien une nouvelle carte réseau wg0
```c
[jinq@vpn ~]$ ip a
4: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
```

### 🌞 Déterminer sur quel port écoute Wireguard

```c
[jinq@vpn ~]$ sudo ss -lun
State                 Recv-Q                Send-Q                               Local Address:Port                                  Peer Address:Port                Process
UNCONN                0                     0                                          0.0.0.0:51820                                      0.0.0.0:*
UNCONN                0                     0                                             [::]:51820                                         [::]:*
```

### 🌞 Ouvrez ce port dans le firewall
```c
[jinq@vpn ~]$ sudo firewall-cmd --permanent --add-port=51820/udp
[jinq@vpn ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s8 enp0s9
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 51820/udp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

```
# 3. Proofs

### 🌞 Ping ping ping !
```c
jinkyu@client1:~$ ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=0.740 ms
64 bytes from 10.7.200.1: icmp_seq=2 ttl=64 time=0.840 ms
64 bytes from 10.7.200.1: icmp_seq=3 ttl=64 time=0.606 ms
64 bytes from 10.7.200.1: icmp_seq=4 ttl=64 time=1.09 ms
^C
--- 10.7.200.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3095ms
rtt min/avg/max/mdev = 0.606/0.819/1.092/0.177 ms
```


### 🌞 Capture ping1_vpn.pcap
[text](ping1_vpn.pcap)

### 🌞 Capture ping2_vpn.pcap
[text](ping1_vpn.pcap)

### 🌞 Prouvez que vous avez toujours un accès internet
```c
jinkyu@client1:~$ traceroute 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 30 hops max, 60 byte packets
 1  10.7.200.1 (10.7.200.1)  1.270 ms  1.293 ms  1.278 ms
 2  _gateway (10.7.1.254)  1.650 ms  1.651 ms  1.648 ms
 3  10.0.2.2 (10.0.2.2)  262.235 ms  262.227 ms  262.215 ms
 4  10.0.2.2 (10.0.2.2)  264.888 ms  264.833 ms  265.387 ms
```

# 4. Private service

### 🌞 Visitez le service Web à travers le VPN

```
[jinq@web ~]$ curl -k https://sitedefou.tp7.b1
meow !
```
