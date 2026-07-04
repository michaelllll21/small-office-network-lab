# Small Office Network Lab

## Project Overview
This project simulates a small office network using Cisco Packet Tracer. The network is divided into three departments: Admin, IT, and Guest. VLANs are used to separate network traffic, and inter-VLAN routing allows communication between VLANs.

## Objectives
- Design a small office network topology
- Configure VLANs for different departments
- Configure inter-VLAN routing
- Configure DHCP for automatic IP addressing
- Apply a basic ACL for network control
- Test connectivity using ping
- Document configuration and troubleshooting steps

## Network Departments

| Department | VLAN | Network | Gateway |
|-----------|------|---------|---------|
| Admin | VLAN 10 | 192.168.10.0/24 | 192.168.10.1 |
| IT | VLAN 20 | 192.168.20.0/24 | 192.168.20.1 |
| Guest | VLAN 30 | 192.168.30.0/24 | 192.168.30.1 |

## Tools Used
- Cisco Packet Tracer
- Router
- Switch
- PCs
- VLAN configuration
- DHCP configuration
- Ping testing

## Project Status
Completed.

## Key Features Implemented
- VLAN segmentation for Admin, IT, and Guest departments
- Router-on-a-stick inter-VLAN routing
- DHCP configuration for automatic IP addressing
- Trunk configuration between router and switch
- ACL rule to block Guest VLAN access to Admin VLAN
- Connectivity testing and troubleshooting documentation

## Topology
The topology diagram will be added in the `topology` folder.

## Documentation
- [IP Addressing Plan](documentation/ip-addressing.md)
- [Configuration Commands](documentation/configuration-commands.md)
- [Testing Results](documentation/testing-results.md)
- [Troubleshooting Notes](documentation/troubleshooting-notes.md)

## Project Status
In progress.
