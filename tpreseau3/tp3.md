# TP3 : 32°13'34"N 95°03'27"W

☀️ Avant de continuer...

```
Adresse Mac . . . . . . . . : 84-C5-A6-76-62-B8
```

☀️ Affichez votre table ARP

```
interface: 192.168.56.1 --- 0x4
  인터넷 주소           Physical Address           유형
  192.168.56.255        ff-ff-ff-ff-ff-ff     Static
  224.0.0.22            01-00-5e-00-00-16     Static
  224.0.0.251           01-00-5e-00-00-fb     Static
  224.0.0.252           01-00-5e-00-00-fc     Static
  239.255.255.250       01-00-5e-7f-ff-fa     Static

interface: 10.33.77.61 --- 0xc
  인터넷 주소           Physical Address           유형
  10.33.64.250          34-6f-24-10-0a-99     Dynamic
  10.33.65.8            34-7d-f6-5a-20-da     Dynamic
  10.33.65.13           08-8e-90-06-a2-7a     Dynamic
  10.33.65.18           34-c9-3d-e4-52-69     Dynamic
  10.33.65.23           64-d6-9a-5c-b0-c0     Dynamic
  10.33.65.37           60-14-b3-ba-82-e9     Dynamic
  10.33.65.63           44-af-28-c3-6a-9f     Dynamic
  10.33.67.218          a8-7e-ea-46-e7-8b     Dynamic
  10.33.70.248          b8-9a-2a-0e-c2-5c     Dynamic
  10.33.73.75           70-d8-23-5e-1b-c2     Dynamic
  10.33.73.77           98-8d-46-c4-fa-e5     Dynamic
  10.33.74.61           50-76-af-12-75-6e     Dynamic
  10.33.77.160          c8-94-02-f8-ab-97     Dynamic
  10.33.78.142          28-16-ad-e0-cf-81     Dynamic
  10.33.79.254          7c-5a-1c-d3-d8-76     Dynamic
  10.33.79.255          ff-ff-ff-ff-ff-ff     Static
  224.0.0.22            01-00-5e-00-00-16     Static
  224.0.0.251           01-00-5e-00-00-fb     Static
  224.0.0.252           01-00-5e-00-00-fc     Static
  224.0.0.253           01-00-5e-00-00-fd     Static
  239.255.255.250       01-00-5e-7f-ff-fa     Static
  255.255.255.255       ff-ff-ff-ff-ff-ff     Static
```
☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école

```
 10.33.79.254          7c-5a-1c-d3-d8-76     Dynamic
```

☀️ Supprimez la ligne qui concerne la passerelle

```
PS C:\WINDOWS\system32> arp -d 10.33.79.254
```
```
interface: 10.33.77.61 --- 0xc
  Internet Address     Physical Address        Type
  10.33.79.254          7c-5a-1c-d3-d8-76     Dynamic
  10.33.79.255          ff-ff-ff-ff-ff-ff     Static
  224.0.0.22            01-00-5e-00-00-16     Static
  224.0.0.251           01-00-5e-00-00-fb     Static
  224.0.0.253           01-00-5e-00-00-fd     Static
  239.255.255.250       01-00-5e-7f-ff-fa     Static
  255.255.255.255       ff-ff-ff-ff-ff-ff     Static
```
☀️ Prouvez que vous avez supprimé la ligne dans la table ARP

```
Interface: 192.168.56.1 --- 0x4
  Internet Address     Physical Address        Type
  192.168.56.255        ff-ff-ff-ff-ff-ff     Static
  224.0.0.22            01-00-5e-00-00-16     Static
  224.0.0.251           01-00-5e-00-00-fb     Static
  224.0.0.252           01-00-5e-00-00-fc     Static
  239.255.255.250       01-00-5e-7f-ff-fa     Static

Interface: 169.254.143.125 --- 0xe
  Internet Address     Physical Address        Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     Static
  224.0.0.22            01-00-5e-00-00-16     Static
  224.0.0.251           01-00-5e-00-00-fb     Static
  224.0.0.252           01-00-5e-00-00-fc     Static
  239.255.255.250       01-00-5e-7f-ff-fa     Static
  255.255.255.255       ff-ff-ff-ff-ff-ff     Static

Interface: 169.254.12.239 --- 0x17
  Internet Address     Physical Address        Type
  169.254.255.255       ff-ff-ff-ff-ff-ff     Static
  224.0.0.22            01-00-5e-00-00-16     Static
  224.0.0.251           01-00-5e-00-00-fb     Static
  224.0.0.252           01-00-5e-00-00-fc     Static
  239.255.255.250       01-00-5e-7f-ff-fa     Static
  255.255.255.255       ff-ff-ff-ff-ff-ff     Static
```

☀️ Wireshark
[text](<../Desktop/ynov 수업/tp2reseau/arp1.pcap>)




## II. ARP dans un réseau local

☀️ Déterminer
```
Wireless LAN adapter Wi-Fi:

   Connection-specific DNS Suffix  . :
   Description  . . . . . . . . . . . : Intel(R) Wireless-AC 9560 160MHz
   Physical Address  . . . . . . . .  : 84-C5-A6-76-62-B8
   DHCP Enabled  . . . . . . . . . .  : Yes
   Autoconfiguration Enabled . . . .  : Yes
   Link-local IPv6 Address . . . . .  : fe80::1326:ba51:470c:3957%12 (Preferred)
   IPv4 Address  . . . . . . . . . .  : 192.168.80.127 (Preferred)
   Subnet Mask  . . . . . . . . . . . : 255.255.255.0
   Lease Obtained  . . . . . . . . .  : Tuesday, October 8, 2024, 10:40:11 AM
   Lease Expires  . . . . . . . . . . : Tuesday, October 8, 2024, 11:40:09 AM
   Default Gateway . . . . . . . . .  : 192.168.80.115
   DHCP Server  . . . . . . . . . . . : 192.168.80.115
   DHCPv6 IAID  . . . . . . . . . . . : 92587430
   DHCPv6 Client DUID . . . . . . . . : 00-01-00-01-2B-AD-F3-84-84-C5-A6-76-62-B8
   DNS Servers  . . . . . . . . . . . : 192.168.80.115
   NetBIOS over Tcpip  . . . . . . .  : Enabled

   ```

```
Ip reseau local 
192.168.80.115
```
```
☀️ DIY
```
```
changer d'adresse IP
celui d'avant
IPv4 Address  . . . . . . . . . .  : 192.168.80.127
celui d'après
IPv4 주소 . . . . . . . . . : 192.168.80.126(기본 설정)
```
☀️ Pingz !

vérifiez que vous pouvez tous vous ping avec ces adresses IP
vérifiez avec une commande ping que vous avez bien un accès internet
```
Site 
Ping wkcd.com [13.248.169.48] with 32 bytes of data:
13.248.169.48: bytes=32 time=113ms TTL=247
13.248.169.48: bytes=32 time=74ms TTL=247
13.248.169.48: bytes=32 time=66ms TTL=247
13.248.169.48: bytes=32 time=79ms TTL=247

13.248.169.48에 대한 Ping 통계:
    Packets: Sent = 4, Received = 4, Lost  = 0 (0% Lost ),
Round trip(밀리초):
    Minimum  = 66ms, Maximum  = 113ms, Average  = 83ms
PS C:\Users\SAMSUNG>

numero 1
Ping 192.168.80.113 with 32 bytes of data:
192.168.80.113: bytes=32 time=15ms TTL=128
192.168.80.113: bytes=32 time=105ms TTL=128
192.168.80.113: bytes=32 time=16ms TTL=128
192.168.80.113: bytes=32 time=109ms TTL=128

192.168.80.113에 대한 Ping 통계:
    Packets: Sent = 4, Received = 4, Lost  = 0 (0% Lost ),
Round trip(밀리초):
    Minimum  = 15ms, Maximum  = 109ms, Average  = 61ms

numero 2
Ping 192.168.80.169 with 32 bytes of data:
192.168.80.169: bytes=32 time=7ms TTL=128
192.168.80.169: bytes=32 time=39ms TTL=128
192.168.80.169: bytes=32 time=36ms TTL=128
192.168.80.169: bytes=32 time=56ms TTL=128

192.168.80.169에 대한 Ping 통계:
    Packets: Sent = 4, Received = 4, Lost  = 0 (0% Lost ),
Round trip(밀리초):
    Minimum  = 7ms, Maximum  = 56ms, Average  = 34ms

numero 3
Ping 192.168.80.200 with 32 bytes of data:
192.168.80.200: bytes=32 time=11ms TTL=64
192.168.80.200: bytes=32 time=7ms TTL=64
192.168.80.200: bytes=32 time=10ms TTL=64
192.168.80.200: bytes=32 time=22ms TTL=64

192.168.80.200에 대한 Ping 통계:
    Packets: Sent = 4, Received = 4, Lost  = 0 (0% Lost ),
 time(밀리초):
    Minimum  = 7ms, Maximum  = 22ms, Average  = 12ms
```

### 2. ARP

☀️ Affichez votre table ARP !

```
Interface: 192.168.80.126 --- 0xc
  Internet Address           물리적 주소           유형
  192.168.80.69         98-bd-80-8b-c9-fa     Dynamic
  192.168.80.113        d4-e9-8a-61-17-a0     Dynamic
  192.168.80.115        56-3d-07-f5-7b-07     Dynamic
  192.168.80.169        98-bd-80-8b-c9-fa     Dynamic
  192.168.80.200        2e-aa-24-77-3e-e2     Dynamic
  192.168.80.255        ff-ff-ff-ff-ff-ff     Static
```
```
videz tous vos tables ARP
PS C:\WINDOWS\system32> arp -d 192.168.80.113
PS C:\WINDOWS\system32> arp -d 192.168.80.69
PS C:\WINDOWS\system32> arp -d 192.168.80.115
PS C:\WINDOWS\system32> arp -d 192.168.80.169
PS C:\WINDOWS\system32> arp -d 192.168.80.200

Interface: 192.168.80.126 --- 0xc
  Internet Address     Physical Address        Type
  192.168.80.115        56-3d-07-f5-7b-07     Dynamic
  192.168.80.255        ff-ff-ff-ff-ff-ff     Static
```

☀️ Capture arp2.pcap
[text](<../Desktop/ynov 수업/tp2reseau/arp2.pcap>)왕복