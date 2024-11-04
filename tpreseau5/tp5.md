# TP5 : Un ptit LAN à nous

## I. Setup

### ☀️ Uniquement avec des commandes, prouvez-que :

```
client1.tp5
```
### configurer un hostname pour la VM

```c
jinkyu@Jclient1:~/Desktop$ sudo hostnamectl [sudo] password for jinkyu:
Static hostname: Jclient1 
Icon name: computer-vm 
Chassis: vme
Machine ID: 5ddd3eb7b1ff464ead5f449a8c861c31 Boot ID: f08fb99c6ef344fca9603187f28b6b69
Virtualization:
oracle
Operating System: Ubuntu 24.04.1 LTS
Kernel: Linux 6.8.0-45-generic
Architecture: x86-64
Hardware Vendor: innotek GmbH
Hardware Model: VirtualBox Firmware Version: VirtualBox
Firmware Date: Fri 2006-12-01
Firmware Age: 17y 10month 2w 1d jinkyu@Jclient1:~/Desktop$
```


### configurer l'adresse IP demandée

```c
jinkyu@Jclient1:~/Desktop$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group defaul t qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host noprefixroute
valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP gr oup default qlen 1000
link/ether 08:00:27:dc:13:14 brd ff:ff:ff:ff:ff:ff
inet 10.5.1.11/24 brd 10.5.1.255 scope global noprefixroute enp0s8 valid_lft forever preferred_lft forever
inet6 fe80::a00:27ff:fedc:1314/64 scope link valid_lft forever preferred_lft forever jinkyu@Jclient1:~/Desktop$
```
### tout le monde peut se ping au sein du réseau 10.5.1.0/24
```c
jinkyu@Jclient1:~/Desktop$ ping 10.5.1.1
PING 10.5.1.1 (10.5.1.1) 56(84) bytes of data.
54 bytes from 10.5.1.1: icmp_seq=1 ttl=128_time=0.781 ms 54 bytes from 10.5.1.1: icmp_seq=2 ttl=128 time=0.455 ms 54 bytes from 10.5.1.1: icmp_seq=3 ttl=128 time=0.383 ms
C
--- 10.5.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2183ms -tt min/avg/max/mdev = 0.383/0.539/0.781/0.173 ms
jinkyu@Jclient1:~/Desktop$ ping 10.5.1.12
PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
54 bytes from 10.5.1.12: icmp_seq=1 ttl=64 time=0.877 ms
54 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=0.411 ms
54 bytes from 10.5.1.12: icmp_seq=3 ttl=64_time=0.563 ms
C
--- 10.5.1.12 ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 2076ms -tt min/avg/max/mdev = 0.411/0.617/0.877/0.194 ms jinkyu@Jclient1:~/Desktop$ ping 10.5.1.254
PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
54 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.499 ms
54 bytes from 10.5.1.254: icmp_seq=2 ttl=64_time=0.563 ms
54 bytes from 10.5.1.254: icmp_seq=3 ttl=64_time=0.533 ms
C
--- 10.5.1.254 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2064ms -tt min/avg/max/mdev = 0.499/0.531/0.563/0.026 ms jinkyu@Jclient1:~/Desktop$
```
client2.tp5

### configurer un hostname pour la VM
```c
jinkyu@Jclient2: ~/Desktop
jinkyu@Jclient2:~/Desktop$ sudo hostnamectl
[sudo] password for jinkyu:
Static hostname: Jclient2
Icon name: computer-vm
Chassis: vm
Machine ID: 5ddd3eb7b1ff464ead5f449a8c861c31
Boot ID: 8d4aca9c11194a59bc55199cca5e9fe5 Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS Kernel: Linux 6.8.0-45-generic
Architecture: x86-64
Hardware Vendor: innotek GmbH Hardware Model: VirtualBox Firmware Version: VirtualBox
Firmware Date: Fri 2006-12-01
Firmware Age: 17y 10month 2w 1d jinkyu@Jclient2:~/Desktop$
```
### configurer l'adresse IP demandée
```c
jinkyu@Jclient2:~/Desktop$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group defaul t qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6 ::1/128 scope host noprefixroute
valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST, MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP gr oup default qlen 1000
link/ether 08:00:27:d5:8c:45 brd ff:ff:ff:ff:ff:ff
inet 10.5.1.12/24 brd 10.5.1.255 scope global noprefixroute enp0s8 valid_lft forever preferred_lft forever
inet6 fe80::a00:27ff:fed5:8c45/64 scope link valid_lft forever preferred_lft forever iinkyu@Jclient2:~/Desktops
```
### tout le monde peut se ping au sein du réseau 10.5.1.0/24
```c
jinkyu@Jclient2:~/Desktop$ ping 10.5.1.1
PING 10.5.1.1 (10.5.1.1) 56(84) bytes of data.
64 bytes from 10.5.1.1: icmp_seq=1 ttl=128 _time=0.421 ms 64 bytes from 10.5.1.1: icmp_seq=2 ttl=128 time=0.301 ms 64 bytes from 10.5.1.1: icmp_seq=3 ttl=128 time=0.351 ms ^C
--- 10.5.1.1 ping statistics --
--
3 packets transmitted, 3 received, 0% packet loss, time 2019ms rtt min/avg/max/mdev = 0.301/0.357/0.421/0.049 ms
jinkyu@Jclient2:~/Desktop$ ping 10.5.1.11
PING 10.5.1.11 (10.5.1.11) 56(84) bytes of data.
64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=4.79 ms
64 bytes from 10.5.1.11: icmp_seq=2 ttl=64_time=0.413 ms
64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=0.621 ms
^C
10.5.1.11 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2035ms rtt min/avg/max/mdev = 0.413/1.942/4.792/2.017 ms jinkyu@Jclient2:~/Desktop$ ping 10.5.1.254
PING 10.5.1.254 (10.5.1.254) 56(84) bytes of data.
64 bytes from 10.5.1.254: icmp_seq=1 ttl=64 time=0.384 ms
64 bytes from 10.5.1.254: icmp_seq=2 ttl=64_time=0.547 ms
64 bytes from 10.5.1.254: icmp_seq=3 ttl=64 time=0.481 ms ^C
--- 10.5.1.254 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2019ms rtt min/avg/max/mdev = 0.384/0.470/0.547/0.066 ms
jinkyu@Jclient2:~/Desktop$
```

### routeur.tp5

### configurer un hostname pour la VM
```c
jinb1 login: root Password:
Last login: Tue Oct 15 17:07:29 on tty1 [root@jinb1 ~]# sudo hostnamectl
Static hostname: jinb1
Icon name: computer-um
Chassis:
M =
Machine ID: 4a42803bd9cb4cdf85521d4f8864607f Boot ID: c1537b36e40d4c429d447a21e423dd73 Virtualization: oracle
Operating System: Rocky Linux 9.4 (Blue Onyx) CPE OS Name: cpe:/o:rocky: rocky:9::baseos
Kernel: Linux 5.14.0-427.13.1.e19_4.x86_64 Architecture: x86-64
Hardware Vendor: innotek GmbH
Hardware Model: VirtualBox Firmware Version: VirtualBox [root@jinb1 ~]#
```
### configurer l'adresse IP demandée
```c
[root@jinb1 ~]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000 link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6:1/128 scope host
valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST, MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000 link/ether 08:00:27:01:36:ad brd ff:ff:ff:ff:ff:ff
inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic nopref ixroute enp0s3
valid_lft 85601sec preferred_lft 85601sec
inet6 fd00::a00:27ff:fe01:36ad/64 scope global dynamic mgtmpaddr
valid_lft 86222sec preferred_lft 14222sec
inet6 fe80::a00:27ff:fe01:36ad/64 scope link
valid_lft forever preferred_lft forever
3: emp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000 link/ether 08:00:27:a1:b1:79 brd ff:ff : f f : f f : f f : ff
inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8
valid_lft forever preferred_lft forever
inet6 fe80::a00:27ff:fea1:b179/64 scope link valid_lft forever preferred_lft forever
[root@jinb1 ~]#
```
### tout le monde peut se ping au sein du réseau 10.5.1.0/24
```c
[root@jinb1] 1# ping 10.5.1.1
PING 10.5.1.1 (10.5.1.1) 56(84) bytes of data.
364 bytes from 10.5.1.1: icmp_seq=1 ttl=128 time=0.445 ms 64 bytes from 10.5.1.1: icmp_seq=2 ttl=128_time=0.390 ms 64 bytes from 10.5.1.1: icmp_seq=3 ttl=128 time=0.402 ms J^c
P--- 18.5.1.1 ping statistics
63 packets transmitted, 3 received, 0% packet loss, time 2052ms rtt min/avg/max/mdev = 0.390/0.412/0.445/0.023 ms
[root@jinbi ~]# ping 10.5.1.11
6PING 10.5.1.11 (18.5.1.11) 56(84) bytes of data.
64 bytes from 10.5.1.11: icmp_seq=1 ttl=64 time=0.914 ms
64 bytes from 10.5.1.11: icmp_seq=2 ttl=64 time=0.663 ms
-64 bytes from 10.5.1.11: icmp_seq=3 ttl=64 time=0.369 ms
3°C
10.5.1.11 ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 2006ms jrtt min/avg/max/mdev = 0.369/0.648/0.914/0.222 ms
[root@jinb1] 1# ping 10.5.1.12
PING 10.5.1.12 (10.5.1.12) 56(84) bytes of data.
664 bytes from 18.5.1.12: icmp_seq=1 ttl=64 time=0.792 ms
664 bytes from 10.5.1.12: icmp_seq=2 ttl=64 time=0.482 ms
64 bytes from 10.5.1.12: icmp_seq=3 ttl=64_time=0.446 ms
c
^--- 18.5.1.12 ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 2006ms rtt min/avg/max/mdev = 0.446/0.573/0.792/0.155 ms [root@jinbi ~]#
```


## II. Accès internet pour tous

### ☀️ Déjà, prouvez que le routeur a un accès internet

```c
[root@vbox ~]# ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=255 time=93.8 ms 64 bytes from 1.1.1.1: icmp_seq=2 ttl=255 time=170 ms 64 bytes from 1.1.1.1: icmp_seq=3 ttl=255 time=447 ms 64 bytes from 1.1.1.1: icmp_seq=1 ttl=255 time=58.4 ms 64 bytes from 1.1.1.1: icmp_seq=5 ttl=255 time=106 ms 64 bytes from 1.1.1.1: icmp_seq=6 ttl=255 time=129 ms 64 bytes from 1.1.1.1: icmp_seq=2 ttl=255 time=162 ms 64 bytes from 1.1.1.1: icmp_seq=8 ttl=255 time=181 ms 64 bytes from 1.1.1.1: icmp_seq=9 ttl=255 time=202 ms
C
1.1.1.1 ping statistics
10 packets transmitted, 9 received, 10% packet loss, time 9011ms rtt min/avg/max/mdev = 58.376/172.119/447.481/106.591 ms [root@vbox ~]#
```
### ☀️ Activez le routage
```c
[root@vbox ~]# sudo firewall-cmd --list-all public (active)
target: default
icmp-block-inversion: no interfaces: enp0s3 enp0s8
sources:
services: ssh
ports: 8888/tcp protocols:
forward: yes masquerade: yes forward-ports: source-ports: icmp-blocks: rich rules:
[root@vbox ~]#
```
j'ai utilisé le commande 
sudo firewall-cmd --add-masquerade --permanent
sudo firewall-cmd --reload

### ☀️ Prouvez que les clients ont un accès internet

### client 1
```c
jinkyu@Jclient1:~/Desktop$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233: icmp_seq=1 ttl=254 time=554 ms 64 bytes from 104.26.11.233: icmp_seq=2 ttl=254 time=516 ms 64 bytes from 104.26.11.233: icmp_seq=3 ttl=254 time=536 ms 64 bytes from 104.26.11.233: icmp_seq=4 ttl=254 time=51.1 ms ^C
---
ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3138ms rtt min/avg/max/mdev = 51.094/414.213/553.760/210.061 ms jinkyu@Jclient1:~/Desktop$
```

### client 2
```c
jinkyu@Jclient2:~/Desktop$ ping ynov.com
PING ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233: icmp_seq=1 ttl=254 time=557 ms 64 bytes from 104.26.10.233: icmp_seq=2 ttl=254 time=532 ms 64 bytes from 104.26.10.233: icmp_seq=3 ttl=254 time=50.0 ms
C
---ynov.com ping statistics ---
4 packets transmitted, 3 received, 25% packet loss, time 3087ms rtt min/avg/max/mdev = 50.047/379.572/556.569/233.223 ms
jinkyu@Jclient2:~/Desktop$
```

### ☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau
client2.tp5.b1
```c
jinkyu@Jclient2:~/Desktop$ cat /etc/netplan/01-netcfg.yaml
network:
version: 2
renderer: networkd
ethernets:
enp0s8:
dhcp4: no
addresses: [10.5.1.12/24]
gateway4: 10.5.1.254
nameservers:
addresses: [1.1.1.1,1.0.0.1] jinkyu@Jclient2:~/Desktop$
```
# III. Serveur SSH
### ☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH
```c
[root@jinbi ~]# sudo systemctl status sshd
➡ sshd.service OpenSSH server daemon
Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: enabled) Active: active (running) since Mon 2824-10-14 18:36:44 CEST: 1h 3min ago Docs: man: sshd (8)
man: sshd_config (5)
Main PID: 730 (sshd)
Tasks: 1 (limit: 11098)
Memory: 2.6M
CPU: 19ms
CGroup: /system.slice/sshd.service
L730 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
Oct 14 18:36:44 jinb1 systemd[1]: Starting OpenSSH server daemon... Oct 14 18:36:44 jinb1 sshd[730]: Server listening on 0.0.0.0 port 22. Oct 14 18:36:44 jinb1 sshd[730]: Server listening on :: port 22. Oct 14 18:36:44 jinb1 systemd[1]: Started OpenSSH server daemon.
```
### ☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert
```c
[root@jinb1 ~]# cat /etc/services | grep ssh
# SSH
# The Secure Shell (SSH) Protocol # The Secure Shell (SSH) Protocol # SSH X11 forwarding offset
# SSLshell
SSLshell
# NETCONF over SSH
# NETCONF over SSH
# Simple Distributed Objects over SSH
ssh
22/tcp
ssh
22/udp
```

# IV. Serveur DHCP
## ☀️ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1
### installation du paquet qui contient le serveur DHCP
``` c
[jing@jinb1 -]$ sudo dnf install dhcp-server
[sudo] password for jing:
Last metadata expiration check: 0:01:47 ago on Tue 15 Oct 2024 05:15:03 PM CEST. Dependencies resolved.
Package
Architecture
Installing:
dhcp-server
x86_64
Installing dependencies:
dhcp-common
noarch
Transaction Summary
Version
Repository
Size
12:4.4.2-19.b1.e19
baseos
1.2 M
12:4.4.2-19.b1.el9
baseos
128 k
Install 2 Packages
Total download size: 1.3 M
Installed size: 4.2 M
Is this ok [y/N] y
Down loading Packages:
(1/2): dhcp-common-4.4.2-19.b1.e19.noarch.rpm (2/2): dhcp-server-4.4.2-19.b1.e19.x86_64.rpm
Total
Running transaction check Transaction check succeeded. Running transaction test Transaction test succeeded. Running transaction
Preparing
Installing
dhcp-common-12:4.4.2-19.b1.e19.noarch
Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64
Installing
dhcp-server-12:4.4.2-19.b1.e19.x86_64
Running scriptlet: dhcp-server-12:4.4.2-19.b1.el9.x86_64
Verifying
161 kB/s | 128 kB
00:00
541 kB/s
1.2 MB
00:02
286 kB/s | 1.3 MB
00:04
2/2
Verifying
: dhcp-server-12:4.4.2-19.b1.e19.x86_64 dhcp-common-12:4.4.2-19.b1.e19.noarch
I~~~~~~
1/1
1/2
2/2
2/2
1/2
            2/2
Installed:
dhcp-common-12:4.4.2-19.b1.e19.noarch
dhcp-server-12:4.4.2-19.b1.e19.x86_64
Complete!
[j inq@jinb1 ~]$
```

### modification de la configuration
```c
# create new
# specify domain name
option domain-name "jin";
#specify DNS server's hostname or IP address option domain-name-servers 10.5.1.254;
# default lease time
default-lease-time 600; #max lease time
max-lease-time 7200;
# this DHCP server to be declared valid authoritative:
#specify network address and subnetmask subnet 10.5.1.0 netmask 255.255.255.0 { range 18.5.1.137 18.5.1.237; option routers 10.5.1.254;
option domain-name-servers 1.1.1.1;
# Plage d'adresses IP attribuables # Passerelle
# Serveur DNS
```


## B. Test avec un nouveau client
### ☀️ Créez une nouvelle machine client client3.tp5.b1

#### définissez son hostname
```c
[sudo] password for jinkyu: Static hostname: jinkyu-VirtualBox
Icon name: computer-vm
Chassis: vm
Machine ID: 5ddd3eb7b1ff464ead5f449a8c861c31
Boot ID: bd96954c02f944da9a498183dc72847e Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS Kernel: Linux 6.8.0-45-generic
Architecture: x86-64
Hardware Vendor: innotek GmbH
Hardware Model: VirtualBox
Firmware Version: VirtualBox
Firmware Date: Fri 2006-12-01
Firmware Age: 17y 10month 2w 1d
jinkyu@jinkyu-VirtualBox:~/Desktop$ sudo hostnamectl set-hostname jiiiin jinkyu@jinkyu-VirtualBox:~/Desktop$ sudo hostnamectl
Static hostname: jiiiin
Icon name: computer-vm Chassis: vm
Machine ID: 5ddd3eb7b1ff464ead5f449a8c861c31 Boot ID: bd96954c02f944da9a498183dc72847e
Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS
Kernel: Linux 6.8.0-45-generic
Architecture: x86-64
Hardware Vendor: innotek GmbH
Hardware Model: VirtualBox Firmware Version: VirtualBox
Firmware Date: Fri 2006-12-01
Firmware Age: 17y 10month 2w 1d jinkyu@jinkyu-VirtualBox:~/Desktop$
```
#### définissez une IP en DHCP
```c
GNU nano 7.2
network: version: 2
renderer: networkd ethernets:
enp0s8:
dhcp4: yes
/etc/netplan/01-netcfg.yaml
addresses: [10.5.1.137/24] gateway4: 10.5.1.254
nameservers:
addresses: [1.1.1.1,1.0.0.1]
```
#### vérifiez que c'est bien une adresse IP entre .137 et .237
```c
jinkyu@jiiiin:~/Desktop$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group defaul = qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6:1/128 scope host noprefixroute
valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST, MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP gr pup default qlen 1000
link/ether 08:00:27:d5:15:ca brd ff:ff:ff:ff:ff:ff
inet 10.5.1.137/24 brd 10.5.1.255 scope global noprefixroute enp0s8 valid_lft forever preferred_lft forever
inet6 fe80::a00:27ff:fed5:15ca/64 scope link valid_lft forever preferred_lft forever jinkyu@jiiiin:~/Desktop$
```
#### prouvez qu'il a immédiatement un accès internet
```c
jinkyu@jiiiin:~/Desktop$ ping ynov.com
PING ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233: icmp_seq=1 ttl=254 time=546 ms 64 bytes from 104.26.10.233: icmp_seq=2 ttl=254 time=144 ms 64 bytes from 104.26.10.233: icmp_seq=3 ttl=254 time=203 ms
^C
ynov.com ping statistics
3 packets transmitted, 3 received, 0% packet loss, time 2002ms rtt min/avg/max/mdev = 144.030/297.648/545.644/177.019 ms iinkyu@iiiiin:~/DesktopŜ
```

## C. Consulter le bail DHCP

### ☀️ Consultez le bail DHCP qui a été créé pour notre client

```c
}
lease 10.5.1.137 {
starts 2 2024/18/15 18:40:17; ends 2 2024/10/15 18:50:17: cltt 2 2024/18/15 18:40:17; binding state active:
next binding state free:
rewind binding state free:
hardware ethernet 08:00:27:d5:15:ca: uid "\001010\000 '\325\025\312";
client-hostname "jiiiin";
[root@jinb1 ~]#
```
### ☀️ Confirmez qu'il s'agit bien de la bonne adresse MAC
```c
jinkyu@jiiiin:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group defaul t qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo
valid_lft forever preferred_lft forever
inet6:1/128 scope host noprefixroute
valid_lft forever preferred_lft forever
2: enp0s8: <BROADCAST, MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP gr oup default qlen 1000
link/ether 08:00:27:d5:15:ca brd ff:ff:ff:ff:ff:ff
inet 10.5.1.137/24 brd 10.5.1.255 scope global dynamic noprefixroute enp0s8 valid_lft 366sec preferred_lft 366sec
inet6 fe80::ed7f:64c4:59c7:d19e/64 scope link noprefixroute
valid_lft forever preferred_lft forever
jinkyu@jiiiin:~$
```





