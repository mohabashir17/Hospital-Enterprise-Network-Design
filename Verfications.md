# Verification Outputs

---

## 1. HSRP Status (HQ Multilayer Switch)

~~~bash
HQ-MultilayerSW1#show standby brief

                     P indicates configured to preempt.
                     |
Interface   Grp  Pri P State    Active          Standby         Virtual IP
Vl10        1    150 P Active   local           192.168.100.3   192.168.100.1  
Vl20        1    150 P Active   local           192.168.100.35  192.168.100.33 
Vl30        1    150 P Active   local           192.168.100.67  192.168.100.65 
Vl40        1    50  P Standby  192.168.100.99  local           192.168.100.97 
Vl50        1    50  P Standby  192.168.100.131 local           192.168.100.129
Vl60        1    50  P Standby  192.168.100.163 local           192.168.100.161
~~~

---

## 2. OSPF Neighbor Adjacency (HQ Router)

~~~bash
HQ-Router#show ip ospf neighbor

Neighbor ID     Pri   State           Dead Time   Address         Interface
192.168.101.161   1   FULL/BDR        00:00:32    192.168.101.161 GigabitEthernet0/0
192.168.101.165   1   FULL/BDR        00:00:32    192.168.101.165 GigabitEthernet0/1
203.0.113.13      0   FULL/  -        00:00:32    192.168.101.178 Tunnel0
~~~

---

## 3. OSPF Routing Table

~~~bash
HQ-Router#show ip route ospf

     192.168.100.0/27 is subnetted, 8 subnets
O       192.168.100.0 [110/2] via 192.168.101.161, GigabitEthernet0/0
O       192.168.100.32 [110/2] via 192.168.101.161, GigabitEthernet0/0
O       192.168.100.64 [110/2] via 192.168.101.161, GigabitEthernet0/0
O       192.168.100.96 [110/2] via 192.168.101.161, GigabitEthernet0/0
O       192.168.100.128 [110/2] via 192.168.101.161, GigabitEthernet0/0
O       192.168.100.160 [110/2] via 192.168.101.161, GigabitEthernet0/0

O       192.168.100.192 [110/1002] via 192.168.101.178, Tunnel0
O       192.168.100.224 [110/1002] via 192.168.101.178, Tunnel0

O       192.168.101.0 [110/1002] via 192.168.101.178, Tunnel0
O       192.168.101.32 [110/1002] via 192.168.101.178, Tunnel0
O       192.168.101.64 [110/1002] via 192.168.101.178, Tunnel0
O       192.168.101.96 [110/1002] via 192.168.101.178, Tunnel0
~~~

---

## 4. GRE Tunnel Status

~~~bash
HQ-Router#show interface tunnel 0

Tunnel0 is up, line protocol is up (connected)
Internet address is 192.168.101.177/30
Tunnel source 203.0.113.1
Tunnel destination 203.0.113.9
Tunnel protocol GRE/IP
~~~

---

## 5. VLAN Configuration

~~~bash
ITS-SW#show vlan brief

VLAN Name                             Status    Ports
1    default                          active    Gig0/1, Gig0/2
40   VLAN0040                         active    Fa0/3 - Fa0/24
~~~

---

## 6. Trunk Interfaces

~~~bash
HQ-MultilayerSW1#show interfaces trunk

Port        Mode         Encapsulation  Status        Native vlan
Gig1/0/2    on           802.1q         trunking      1

Vlans allowed and active:
1,10,20,30,40,50,60
~~~

---

## 7. SVI Interfaces

~~~bash
HQ-MultilayerSW1#show ip interface brief | include Vlan

Vlan10   192.168.100.2   up  up
Vlan20   192.168.100.34  up  up
Vlan30   192.168.100.66  up  up
Vlan40   192.168.100.98  up  up
Vlan50   192.168.100.130 up  up
Vlan60   192.168.100.162 up  up
~~~

---

## 8. DHCP (Central Server)

📸 Insert screenshot here:
`![DHCP](your-image-link.png)`

---

## 9. DHCP Relay

~~~bash
HQ-MultilayerSW1#show running-config | include helper-address

ip helper-address 192.168.101.131
~~~

---

## 10. NAT (PAT)

~~~bash
HQ-Router#show ip nat translations

Pro  Inside global     Inside local
icmp 203.0.113.1       192.168.100.59
icmp 203.0.113.1       192.168.100.100
icmp 203.0.113.1       192.168.100.23
~~~

---

## 11. SSH

~~~bash
BR-MultilayerSW1#show ip ssh

SSH Enabled - version 2.0
~~~

---

## 12. Wireless (WPA2)

📸 Insert AP screenshot here:
`![Wireless](your-image-link.png)`

---

## 13. Static Route

~~~bash
BR-Router#show ip route static

S* 0.0.0.0/0 via 203.0.113.10
~~~

---

## 14. Ping Test

~~~bash
PC> ping 192.168.100.219

Reply from 192.168.100.219: bytes=32 time=36ms TTL=124
Reply from 192.168.100.219: bytes=32 time=76ms TTL=124
Reply from 192.168.100.219: bytes=32 time=46ms TTL=124
Reply from 192.168.100.219: bytes=32 time=60ms TTL=124
~~~

---

## 15. Traceroute

~~~bash
PC> tracert 192.168.100.219

1  192.168.100.66
2  192.168.101.162
3  192.168.101.178
4  192.168.101.169
5  192.168.100.219
~~~
