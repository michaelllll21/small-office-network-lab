## ACL Configuration

The ACL below prevents the Guest VLAN from initiating access to the Admin VLAN while still allowing Admin VLAN to receive ICMP echo replies from the Guest VLAN.

```cisco
no access-list 100

access-list 100 permit icmp 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255 echo-reply
access-list 100 deny ip 192.168.30.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 100 permit ip any any

interface gigabitEthernet 0/0.30
ip access-group 100 in
exit

## Router Configuration

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
## ACL Configuration

Commands will be added after basic access control configuration.
