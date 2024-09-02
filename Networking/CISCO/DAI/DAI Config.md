![[Pasted image 20240320103808.png]]


````
s1(config)# ip dhcp snooping
s1(config)# ip dhcp snooping vlan 10
s1(config)# ip arp inspection vlan 10

s1(config)# int fa0/24
s1(config-if)# ip dhcp snooping trust
s1(config-if)# ip arp inspection trust
`````

