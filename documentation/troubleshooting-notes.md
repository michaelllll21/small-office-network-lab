# Troubleshooting Notes

## Issue 1: Trunk Port Not Showing

**Problem:**  
The `show interfaces trunk` command did not display FastEthernet0/1 as a trunk port.

**Cause:**  
The router interface connected to the switch was still administratively down.

**Solution:**  
Enabled the router interface using the `no shutdown` command on GigabitEthernet0/0.

**Verification:**  
After configuring the router subinterfaces and enabling the physical interface, the trunk link became active.

---

## Issue 2: Admin VLAN Could Not Ping Guest VLAN After ACL

**Problem:**  
After applying the ACL, Admin-PC1 could not ping Guest-PC1.

**Cause:**  
The ACL blocked all traffic from the Guest VLAN to the Admin VLAN, including ICMP echo-reply traffic.

**Solution:**  
Modified the ACL to allow ICMP echo-reply from Guest VLAN to Admin VLAN before denying other Guest-to-Admin traffic.

**Verification:**  
Guest-to-Admin ping was blocked, Guest-to-IT ping was allowed, and Admin-to-Guest ping worked successfully.
