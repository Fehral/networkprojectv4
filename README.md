<p align=center>
  <ins>Overview of Concepts</ins>
</p>

Collapsed Core Architecture  
  * a two-tiered network design that combines the core and distribution layers into a single layer
  * more cost-effective than a three-tiered design with dedicated core, distribution, and access layers
  * not as scalable as three-tiered architectures and provides less redundancy

RIPv2  
  * Routing Information Protocol uses hop counts to determine the best path between routers using distance vectors
  * RIP version 2 is an improvement over version 1 by way of utilizing classless routing, support for variable length subnet masks, and authentication
    * VLSM allows for creation of subnets of varying sizes, optimizing IPv4 address usage
  * RIPv2 uses multicast for updates, reducing network bandwidth usage, while RIPv1 uses broadcasts

<p align=center>
  <ins>University Campus Network Toplogy</ins>
</p>

<p align=center>
  <img src="https://github.com/Fehral/networkprojectv4/blob/main/networkprojectv4topology.png?raw=true">
</p>

MAIN-CAMPUS-ROUTER Configuration

```
Router>en
Router#conf t
Router(config)#int s0/0/0
Router(config-if)#clock rate 64000
Router(config-if)#ip address 10.0.0.5 255.255.255.252
Router(config-if)#no shutdown
Router(config-if)#int s0/0/1
Router(config-if)#clock rate 64000
Router(config-if)#ip address 10.0.0.1 255.255.255.252
Router(config-if)#no shutdown
Router(config-if)#int g0/0
Router(config-if)#no shutdown
Router(config-if)#int g0/0.10
Router(config-subif)#encapsulation dot1Q 10
Router(config-subif)#ip address 192.168.1.1 255.255.255.0
Router(config-subif)#int g0/0.20
Router(config-subif)#encapsulation dot1Q 20
Router(config-subif)#ip address 192.168.2.1 255.255.255.0
Router(config-subif)#int g0/0.30
Router(config-subif)#encapsulation dot1Q 30
Router(config-subif)#ip address 192.168.3.1 255.255.255.0
Router(config-subif)#int g0/0.40
Router(config-subif)#encapsulation dot1Q 40
Router(config-subif)#ip address 192.168.4.1 255.255.255.0
Router(config-subif)#int g0/0.50
Router(config-subif)#encapsulation dot1Q 50
Router(config-subif)#ip address 192.168.5.1 255.255.255.0
Router(config-subif)#int g0/0.60
Router(config-subif)#encapsulation dot1Q 60
Router(config-subif)#ip address 192.168.6.1 255.255.255.0
Router(config-subif)#int g0/0.70
Router(config-subif)#encapsulation dot1Q 70
Router(config-subif)#ip address 192.168.7.1 255.255.255.0
Router(config-subif)#int g0/0.80
Router(config-subif)#encapsulation dot1Q 80
Router(config-subif)#ip address 192.168.8.1 255.255.255.0
Router(config-subif)#exit
Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#network 10.0.0.0
Router(config-router)#network 192.168.1.0
Router(config-router)#network 192.168.2.0
Router(config-router)#network 192.168.3.0
Router(config-router)#network 192.168.4.0
Router(config-router)#network 192.168.5.0
Router(config-router)#network 192.168.6.0
Router(config-router)#network 192.168.7.0
Router(config-router)#network 192.168.8.0
Router(config-router)#exit
Router(config)#service dhcp
Router(config)#ip dhcp pool Business
Router(dhcp-config)#network 192.168.1.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.1.1
Router(dhcp-config)#dns-server 192.168.1.1
Router(dhcp-config)#domain-name Business.com
Router(dhcp-config)#ip dhcp pool Admin
Router(dhcp-config)#network 192.168.2.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.2.1
Router(dhcp-config)#dns-server 192.168.2.1
Router(dhcp-config)#domain-name Admin
Router(dhcp-config)#ip dhcp pool HR
Router(dhcp-config)#network 192.168.3.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.3.1
Router(dhcp-config)#dns-server 192.168.3.1
Router(dhcp-config)#domain-name HR.com
Router(dhcp-config)#ip dhcp pool Finance
Router(dhcp-config)#network 192.168.4.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.4.1
Router(dhcp-config)#dns-server 192.168.4.1
Router(dhcp-config)#domain-name Finance.com
Router(dhcp-config)#ip dhcp pool EngComp
Router(dhcp-config)#network 192.168.5.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.5.1
Router(dhcp-config)#dns-server 192.168.5.1
Router(dhcp-config)#domain-name EngComp.com
Router(dhcp-config)#ip dhcp pool ArtDes
Router(dhcp-config)#network 192.168.6.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.6.1
Router(dhcp-config)#dns-server 192.168.6.1
Router(dhcp-config)#domain-name ArtDes.com
Router(dhcp-config)#ip dhcp pool StdLabOne
Router(dhcp-config)#network 192.168.7.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.7.1
Router(dhcp-config)#dns-server 192.168.7.1
Router(dhcp-config)#domain-name StdLabOne.com
Router(dhcp-config)#ip dhcp pool ITDept
Router(dhcp-config)#network 192.168.8.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.8.1
Router(dhcp-config)#dns-server 192.168.8.1
Router(dhcp-config)#domain-name ITDept.com
Router(dhcp-config)#exit
Router(config)#exit
Router#
%SYS-5-CONFIG_I: Configured from console by console
copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

MAIN-CAMPUS-L3-SWITCH Configuration

```
Switch>en
Switch#conf t
Switch(config)#int g1/0/1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 10
Switch(config-if)#int g1/0/2
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 20
Switch(config-if)#int g1/0/3
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 30
Switch(config-if)#int g1/0/4
Switch(config-if)#switchport access vlan 40
Switch(config-if)#int g1/0/5
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 50
Switch(config-if)#int g1/0/6
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 60
Switch(config-if)#int g1/0/7
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 70
Switch(config-if)#int g1/0/8
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 80
Switch(config-if)#int g1/0/24
Switch(config-if)#switchport mode trunk
Switch(config-if)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

Business Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 10
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

Admin Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 20
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

HR Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 30
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

Finance Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 40
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

Engineering & Computing Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 50
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

Art & Design Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 60
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

Student Lab 1 Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 70
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

IT Department Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 80
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

BRANCH-CAMPUS-ROUTER Configuration

```
Router>en
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#int s0/0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 10.0.0.2 255.255.255.252
Router(config-if)#int g0/0
Router(config-if)#no shutdown
Router(config-if)#int g0/0.90
Router(config-subif)#encapsulation dot1Q 90
Router(config-subif)#ip address 192.168.9.1 255.255.255.0
Router(config-subif)#int g0/0.100
Router(config-subif)#encapsulation dot1Q 100
Router(config-subif)#ip address 192.168.10.1 255.255.255.0
Router(config-subif)#exit
Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#network 10.0.0.0
Router(config-router)#network 192.168.9.0
Router(config-router)#network 192.168.10.0
Router(config-router)#exit
Router(config)#service dhcp
Router(config)#ip dhcp pool Staff
Router(dhcp-config)#network 192.168.9.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.9.1
Router(dhcp-config)#dns-server 192.168.9.1
Router(dhcp-config)#domain-name Staff
Router(dhcp-config)#ip dhcp pool StdLabTwo
Router(dhcp-config)#network 192.168.10.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.10.1
Router(dhcp-config)#dns-server 192.168.10.1
Router(dhcp-config)#domain-name StdLabTwo.com
Router(dhcp-config)#end
Router#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

BRANCH-CAMPUS-L3-SWITCH Configuration

```
Switch>en
Switch#conf t
Switch(config)#int g1/0/1
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 90
Switch(config-if)#int g1/0/2
Switch(config-if)#switchport mode access
Switch(config-if)#switchport access vlan 100
Switch(config-if)#int g1/0/24
Switch(config-if)#switchport mode trunk
Switch(config-if)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

Staff Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 90
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

Student Lab 2 Switch Configuration

```
Switch>en
Switch#conf t
Switch(config)#int range fa0/1-24
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#switchport access vlan 100
Switch(config-if-range)#end
Switch#copy run start
Destination filename [startup-config]? [Enter]
Building configuration...
[OK]
```

CLOUD-ROUTER Configuration

```
Router>en
Router#conf t
Router(config)#int s0/0/0
Router(config-if)#ip address 10.0.0.6 255.255.255.252
Router(config-if)#no shutdown
Router(config-if)#int g0/0
Router(config-if)#ip address 20.0.0.1 255.255.2
Router(config-if)#no shutdown
Router(config-if)#exit
Router(config)#router rip
Router(config-router)#version 2
Router(config-router)#network 20.0.0.0
Router(config-router)#network 10.0.0.0
Router(config-router)#end
Router#
%SYS-5-CONFIG_I: Configured from console by console
copy run start
Destination filename [startup-config]? 
Building configuration...
[OK]
```
