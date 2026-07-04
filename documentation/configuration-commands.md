# Configuration Commands

This document contains the main configuration commands used in the Small Office Network Lab.

## Switch Configuration

The switch was configured with three VLANs: Admin, IT, and Guest. Access ports were assigned to the correct VLANs, and the port connected to the router was configured as a trunk.

```cisco
enable
configure terminal

hostname SW1

vlan 10
name Admin
exit

vlan 20
name IT
exit

vlan 30
name Guest
exit

interface range fastEthernet 0/2-3
switchport mode access
switchport access vlan 10
exit

interface range fastEthernet 0/4-5
switchport mode access
switchport access vlan 20
exit

interface range fastEthernet 0/6-7
switchport mode access
switchport access vlan 30
exit

interface fastEthernet 0/1
switchport mode trunk
switchport trunk allowed vlan 10,20,30
no shutdown
exit

end
write memory
```

## VLAN Configuration Evidence

![VLAN Configuration](../screenshots/vlan-configuration.png)

---

## Router Configuration

The router was configured using router-on-a-stick. Subinterfaces were created for each VLAN, and each subinterface was assigned as the default gateway for its VLAN.

```cisco
enable
configure terminal

hostname R1

interface gigabitEthernet 0/0
no shutdown
exit

interface gigabitEthernet 0/0.10
encapsulation dot1Q 10
ip address 192.168.10.1 255.255.255.0
exit

interface gigabitEthernet 0/0.20
encapsulation dot1Q 20
ip address 192.168.20.1 255.255.255.0
exit

interface gigabitEthernet 0/0.30
encapsulation dot1Q 30
ip address 192.168.30.1 255.255.255.0
exit

end
write memory
```

---

## DHCP Configuration

DHCP was configured on the router to automatically assign IP addresses to all PCs in each VLAN.

```cisco
enable
configure terminal

ip dhcp excluded-address 192.168.10.1 192.168.10.10
ip dhcp excluded-address 192.168.20.1 192.168.20.10
ip dhcp excluded-address 192.168.30.1 192.168.30.10

ip dhcp pool ADMIN
network 192.168.10.0 255.255.255.0
default-router 192.168.10.1
dns-server 8.8.8.8
exit

ip dhcp pool IT
network 192.168.20.0 255.255.255.0
default-router 192.168.20.1
dns-server 8.8.8.8
exit

ip dhcp pool GUEST
network 192.168.30.0 255.255.255.0
default-router 192.168.30.1
dns-server 8.8.8.8
exit

end
write memory
```

## DHCP Evidence

![DHCP Bindings](../screenshots/dhcp-bindings.png)

---

## ACL Configuration

The ACL below prevents the Guest VLAN from initiating access to the Admin VLAN. ICMP echo-reply traffic was allowed so that Admin VLAN devices can still ping Guest VLAN devices successfully.

```cisco
enable
configure terminal

no access-list 100

access-list 100 permit icmp 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255 echo-reply
access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 100 permit ip any any

interface gigabitEthernet 0/0.30
ip access-group 100 in
exit

end
write memory
```

## ACL Evidence

![ACL Test](../screenshots/acl-test-allowed%20and%20blocked.png)
