
# Firewall Configuration Commands

## Interface Configuration

### Display Interface and VLAN Information
```bash
::show interface ip brief::
::show switch vlan::
```

### Configure Internal Interface (VLAN 1)
```bash
FW1(config)# interface vlan10
FW1(config-if)# nameif internal
FW1(config-if)# ip address 192.168.10.63 255.255.255.192
FW1(config-if)# no shutdown
FW1(config)# exit
FW1# write memory
```

### Configure External Interface (VLAN 2)
```bash
FW1(config)# interface vlan20
FW1(config-if)# nameif external
FW1(config-if)# ip address 203.0.113.201 255.255.255.192
FW1(config-if)# no shutdown
FW1(config-if)# end
```

## Network Object and NAT Configuration

### Create Network Object for Internal LAN
```bash
FW1(config)# object network INTERNAL_NET
FW1(config-network-object)# subnet 192.168.10.0 255.255.255.192
FW1(config-network-object)# nat (internal, external) dynamic interface
FW1(config-network-object)# end
```

### Create Network Object for External Network
```bash
FW1(config)# object network EXTERNAL_NET
FW1(config-network-object)# subnet 203.0.113.0 255.255.255.192
```

## Routing and Access Control

### Configure Default Route
```bash
FW1(config)# route external 0.0.0.0 0.0.0.0 203.0.113.201
```

### Configure Access Control Lists (ACLs)
```bash
FW1(config)# access-list internet_access extended permit tcp any any
FW1(config)# access-list internet_access extended permit icmp any any
```
