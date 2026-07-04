# Testing Results

This file documents the connectivity tests performed in the lab.

## DHCP Results

The router successfully assigned IP addresses to all PCs through DHCP.

| Device | VLAN | Assigned IP Address |
|--------|------|---------------------|
| Admin-PC1 | VLAN 10 | 192.168.10.11 |
| Admin-PC2 | VLAN 10 | 192.168.10.12 |
| IT-PC1 | VLAN 20 | 192.168.20.11 |
| IT-PC2 | VLAN 20 | 192.168.20.12 |
| Guest-PC1 | VLAN 30 | 192.168.30.11 |
| Guest-PC2 | VLAN 30 | 192.168.30.12 |

## Ping Tests Before ACL

| Test | Source | Destination | Result |
|------|--------|-------------|--------|
| Test 1 | Admin-PC1 | 192.168.10.1 | Success |
| Test 2 | Admin-PC1 | IT-PC1 / 192.168.20.11 | Success |
| Test 3 | Admin-PC1 | Guest-PC1 / 192.168.30.11 | Success |
| Test 4 | Guest-PC1 | Admin-PC1 / 192.168.10.11 | Success |

## Ping Tests After ACL

| Test | Source | Destination | Expected Result | Actual Result |
|------|--------|-------------|-----------------|---------------|
| Test 1 | Guest-PC1 | Admin-PC1 / 192.168.10.11 | Blocked | Success: Blocked |
| Test 2 | Guest-PC1 | IT-PC1 / 192.168.20.11 | Allowed | Success |
| Test 3 | Admin-PC1 | Guest-PC1 / 192.168.30.11 | Allowed | Success |

## ACL Result

The ACL successfully blocked Guest VLAN traffic from initiating access to the Admin VLAN while still allowing Guest VLAN access to the IT VLAN. Admin VLAN was also able to communicate with the Guest VLAN after allowing ICMP echo-reply traffic.
