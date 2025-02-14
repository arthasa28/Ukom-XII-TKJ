# Ukom-XII-TKJ

<div align="center"> 
  <img src="https://github.com/arthasa28/Ukom-XII-TKJ/blob/master/SiteA-NAP.png?raw=true" alt="screenshot" />
</div>

</br>

## Script Config SITE A
```bash
# CS-CORE-ISP-A

hostname CS-CORE-ISP-A
int fa0/1
ip add 202.11.3.1 255.255.255.252
no sh
int fa1/0
ip add 202.11.3.5 255.255.255.252
no sh
router ospf 1
router-id 5.5.3.1
network 202.11.3.0 0.0.0.3 area 0
network 202.11.3.4 0.0.0.3 area 0


# R-CS-ISPA-01

hostname R-CS-ISPA-01
int fa0/0
ip add 202.11.3.2 255.255.255.252
no sh
int fa0/1
ip add 202.11.3.14 255.255.255.252
no sh
int fa1/0
ip add 202.11.3.17 255.255.255.252
no sh
int lo0
ip add 1.1.3.1 255.255.255.0
router ospf 1 
router-id 1.1.3.1
network 1.1.3.0 0.0.0.255 area 0
network 202.11.3.0 0.0.0.3 area 0
network 202.11.3.12 0.0.0.3 area 0
network 202.11.3.16 0.0.0.3 area 1
area 1 virtual-link 3.3.3.3


# R-CS-ISPA-02

hostname R-CS-ISPA-02
int fa0/0
ip add 202.11.3.6 255.255.255.252
no sh
int fa0/1
ip add 202.11.3.9 255.255.255.252
no sh
int fa1/0
ip add 192.168.3.17 255.255.255.252
no sh
router ospf 1
router-id 6.6.3.1
network 202.11.3.4 0.0.0.3 area 0
network 202.11.3.8 0.0.0.3 area 0
network 192.168.3.16 255.255.255.252 area 0
ip dhcp pool pool1
network 192.168.3.16 255.255.255.252
default-router 192.168.3.17


# R-CS-ISPA-03

hostname R-CS-ISPA-03
int fa0/0
ip add 202.11.3.13 255.255.255.252
no sh
int fa0/1
ip add 202.11.3.10 255.255.255.252
no sh
int fa1/0
ip add 202.11.3.25 255.255.255.252
no sh
int lo0 
ip add 2.2.3.2 255.255.255.0
router ospf 1
router-id 2.2.3.2
network 2.2.3.0 0.0.0.255 area 0
network 202.11.3.12 0.0.0.3 area 0
network 202.11.3.8 0.0.0.3 area 0
network 202.11.3.24 0.0.0.3 area 2
area 2 virtual-link 4.4.3.4


# RB-ISPA-01

-system identity set name=RB-ISPA-01
-ip add add address=202.11.3.18/30 interface=ether1
-ip add add address=202.11.3.21/30 interface=ether2
-routing ospf area add name=area1 area-id=0.0.0.1
-routing ospf area add name=area3 area-id=0.0.0.3
-routing ospf network add network=202.11.3.16/30 area=area1
-routing ospf network add network=202.11.3.20/30 area=area3
-int bridge add name=loopback
-routing ospf instance add router-id=3.3.3.3
-ip add add add=3.3.3.3/24 int=loopback
-routing ospf network add network=3.3.3.0/24 area=area1
-routing ospf virtual-link add neighbor-id=1.1.3.1 transit-area=area1
PERINGATAN: KALO BELOM CONNECT MATIIN DULU R-CS-ISPA-01 SAMA RB-ISPA-01 tapi di simpen dlu "write buat cisco ama exp buat mikrotik"


# RB-ISPA-02

-system identity set name=RB-ISPA-02
-ip add add address=202.11.3.22/30 interface=ether1
-ip add add address=192.168.3.1/29 interface=ether2
-routing ospf area add name=area3 area-id=0.0.0.3
-routing ospf network add network=202.11.3.20/30 area=area3
-routing ospf network add network=192.168.3.0/29 area=area3
-ip firewall nat add chain=srcnat action Masquerade
-ip dhcp-server setup
-masukkin ether2
-"ip dhcp"         DI VPC YAAA BUKAN DI ROUTER


# RB-ISPA-03

-system identity set name=RB-ISPA-03
-ip add add address=202.11.3.26/30 interface=ether1
-ip add add address=202.11.3.29/30 interface=ether2
-ip add add address=202.11.3.33/30 interface=ether3
-ip add add address=192.168.3.9/29 interface=ether4
-routing ospf area add name=area2 area-id=0.0.0.2
-routing ospf area add name=area4 area-id=0.0.0.4
-routing ospf network add network=202.11.3.24/30 area=area2
-routing ospf network add network=202.11.3.28/30 area=area4
-routing ospf network add network=202.11.3.32/30 area=area4
-routing ospf network add network=192.168.3.8/29 area=area4
-int bridge add name=loopback
-routing ospf instance add router-id=4.4.3.4
-ip add add add=4.4.3.4/24 int=loopback
-routing ospf network add network=4.4.3.0/24 area=area2
-routing ospf virtual-link add neighbor-id=2.2.3.2 transit-area=area2
PERINGATAN: KALO BELOM CONNECT MATIIN DULU R-CS-ISPA-03 SAMA RB-ISPA-03 tapi di simpen dlu "write buat cisco ama exp buat mikrotik"
ip firewall nat add chain=srcnat action=Masquerade
-ip dhcp-server setup
-masukkin ether4
-"ip dhcp"         DI VPC YAAA BUKAN DI ROUTER


# RB-ISPA-04

-system identity set name=RB-ISPA-04
-ip add add address=202.11.3.30/30 interface=ether1
-ip add add address=192.168.3.21/30 interface=ether2
-routing ospf area add name=area4 area-id=0.0.0.4
-routing ospf network add network=202.11.3.28/30 area=area4
-routing ospf network add network=192.168.3.20/30 area=area4
-ip firewall nat add chain=srcnat action Masquerade
-ip dhcp-server setup
-masukkin ether2
-"ip dhcp"         DI VPC YAAA BUKAN DI ROUTER


# RB-ISPA-05

-system identity set name=RB-ISPA-05
-ip add add address=202.11.3.34/30 interface=ether1
-ip add add address=202.11.3.37/30 interface=ether2
-routing ospf area add name=area4 area-id=0.0.0.4
-routing ospf network add network=202.11.3.32/30 area=area4
-routing ospf network add network=202.11.3.36/30 area=area4


# RB-ISPA-06

-system identity set name=RB-ISPA-06
-ip add add address=202.11.3.38/30 interface=ether1
-ip add add address=192.168.3.25/30 interface=ether2
-routing ospf area add name=area4 area-id=0.0.0.4
-routing ospf network add network=202.11.3.36/30 area=area4
-routing ospf network add network=192.168.3.24/30 area=area4
-ip firewall nat add chain=srcnat action Masquerade
-ip dhcp-server setup
-masukkin ether2
-"ip dhcp"         DI VPC YAAA BUKAN DI ROUTER

```

## BGP SITE A

```bash
router bgp 65001
bgp router-id 5.5.5.1
neighbor 113.12.18.1 remote-as 65002
neighbor 113.12.18.1 update-source fa0/0
network 202.11.3.0 mask 255.255.255.252
network 202.11.3.4 mask 255.255.255.252
```

## BGP SITE B

```bash
router bgp 65002
bgp router-id 7.7.7.7
neighbor 202.11.3.1 remote-as 65001
neighbor 202.11.3.1 update-source fa2/0
network 113.12.18.0 mask 255.255.255.252
network 113.12.18.4 mask 255.255.255.252
network 113.12.18.12 mask 255.255.255.252
```
