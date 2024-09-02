# Check CDP Status


![](../Imagens/Pasted%20image%2020240611101951.png)


# Enable CDP on the Interface
![](../Imagens/Pasted%20image%2020240611102102.png)

# Check Neighbors
![](../Imagens/Pasted%20image%2020240611102147.png)


![](../Imagens/Pasted%20image%2020240611102242.png)

# Display the status of CDP on R1.

````
R1#show cdp

% CDP is not enabled


R1(config)#cdp run

R1(config)#interface s0/0/0

R1(config-if)#no cdp enable

R1(config-if)#end

*Oct  2 15:43:46.288: %SYS-5-CONFIG_I: Configured from console by console

Display the list of CDP neighbors on R1.

R1#show cdp neighbors

Capability Codes: R - Router, T - Trans Bridge, B - Source Route Bridge
                  S - Switch, H - Host, I - IGMP, r - Repeater, P - Phone,
                  D - Remote, C - CVTA, M - Two-port Mac Relay
Device ID        Local Intrfce     Holdtme    Capability  Platform  Port ID
S1               Gig 0/0/1         179              S I   WS-C3560- Fas 0/5

Display more details from the list of CDP neighbors on R1.

R1#show cdp neighbors detail

\-------------------------
Device ID: S1
Entry address(es):
Platform: cisco WS-C3560-24TS,  Capabilities: Switch IGMP
Interface: GigabitEthernet0/0/1,  Port ID (outgoing port): FastEthernet0/5
Holdtime : 174 sec
   
Version :
Cisco IOS Software, C3560 Software (C3560-IPSERVICESK9-M), Version 15.0(2)SE7, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2014 by Cisco Systems, Inc.
Compiled Thu 23-Oct-14 14:13 by prod_rel_team
   
advertisement version: 2
Protocol Hello:  OUI=0x00000C, Protocol ID=0x0112; payload len=27, value=00000000FFFFFFFF010221FF000000000000FCFBFB957300FF0000
VTP Management Domain: ''
Native VLAN: 1
Duplex: full
   
   
Total cdp entries displayed : 1
`````


You have successfully configured and verified CDP on the router.
