enable
configure terminal

!================================
! Basic Device Configuration
!================================

hostname ACC-A

enable secret Qwe123!$

username admin privilege 15 secret Qwe123!$

line console 0
 logging synchronous
 login local

line vty 0 15
 login local

!================================
! VLAN Configuration
!================================

vlan 10
 name MANAGEMENT

vlan 20
 name USERS

vlan 30
 name SERVERS

vlan 40
 name GUEST

vlan 100
 name FINANCE

vlan 999
 name NATIVE

!================================
! Management Interface
!================================

interface vlan 10
 ip address 10.42.10.21 255.255.255.0
 no shutdown

ip default-gateway 10.42.10.1

!================================
! Access Ports
!================================

interface GigabitEthernet1/0
 description HOST-A
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast

interface GigabitEthernet1/1
 description HOST-B
 switchport mode access
 switchport access vlan 20
 spanning-tree portfast

!================================
! Trunk Ports
!================================

interface GigabitEthernet0/0
 description TRUNK_TO_ACC-B
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,100

interface GigabitEthernet0/1
 description TRUNK_TO_MLS-CORE-A
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,100

interface GigabitEthernet0/2
 description TRUNK_TO_MLS-CORE-B
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,100

!================================
! Save Configuration
!================================

end
write memory
