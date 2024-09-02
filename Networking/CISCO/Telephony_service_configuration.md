# Telephony Service Configuration

## Telephony Service Settings
```bash
telephony-service
max-ephones 5  # Maximum number of phones
max-dn 5  # Maximum number of extensions
ip source-address 192.168.100.254 port 2000  # Source IP address for telephony service
auto assign 1 to 5  # Auto-assign extensions from 1 to 5
```

## Alternate Telephony Service Settings
```bash
telephony-service
max-ephones 5
max-dn 5        
ip source-address 172.16.1.254 port 2000  # Alternate source IP address for telephony service
auto assign 1 to 5  
```

# Extension and Phone Setup

## Extension Numbers
```bash
ephone-dn 1
number 54001  # Extension 54001
exit

ephone-dn 2
number 54002  # Extension 54002
exit

ephone-dn 3
number 54003  # Extension 54003
exit
```

## Phone Type and Button Mapping
```bash
ephone 1
type 7960  # Phone type model 7960
button 1:1  # Button mapping for line 1 on phone 1

ephone 2
type 7960
button 1:1  # Button mapping for line 1 on phone 2
```

# DHCP Pool Configuration

## DHCP Pool Setup (First Option)
```bash
ip dhcp pool data
network 192.168.100.0 255.255.255.0  # Define network and subnet mask
default-router 192.168.100.254  # Default gateway for DHCP clients
option 150 ip 192.168.100.254  # TFTP server for IP phones
```

## DHCP Pool Setup (Second Option)
```bash
ip dhcp pool data
network 192.168.1.0 255.255.255.0  # Alternate network and subnet mask
default-router 192.168.1.254  # Default gateway for alternate network
option 150 ip 192.168.1.254  # TFTP server for IP phones on alternate network
```

# Voice VLAN and Interface Configuration

## Interface Configuration for Voice VLAN
```bash
Switch(config-if)#switchport nonegotiate 
switchport voice vlan 7  # Assign voice VLAN 7 to the interface
```

## Interface Configuration for Data and Voice VLANs
```bash
Switch(config-if)#switchport access vlan 2  # Assign data VLAN 2 to the interface
Switch(config-if)#switchport voice vlan 7  # Assign voice VLAN 7 to the same interface
```

# VoIP Profile Configuration

## VoIP Profile Setup for OSPF Communication
```bash
dial-peer voice 4 voip
destination-pattern 2...  # Match dialed numbers starting with 2
session target ipv4:192.168.12.9  # Destination IP for VoIP traffic
exit

dial-peer voice 5 voip
destination-pattern 3...  # Match dialed numbers starting with 3
session target ipv4:192.168.12.2  # Alternate destination IP for VoIP traffic
```

## Additional VoIP Profile
```bash
dial-peer voice 100 voip
destination-pattern 3...  # Match dialed numbers starting with 3
session target ipv4:192.168.12.2  # Another destination IP for VoIP traffic
```

## Specific VoIP Profile for Incoming Traffic
```bash
dial-peer voice 1 voip
session target ipv4:"entry_ip_address"  # Placeholder for incoming IP address
```
