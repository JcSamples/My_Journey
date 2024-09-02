
# Network Equipment Commands Summary

## System Passwords
```shell
enable password secure1
line console 0
password secure2
login
exit
```

## Banner (Routers and Switches)
```shell
banner motd #Your Message Here#
```

## Secure Shell (SSH)
```shell
ip domain-name LastName.local
crypto key generate rsa
1024
username AdminUser password secure4
line vty 0 15
transport input ssh
login local
exit
```

## VLAN Configuration for Switches
*(Do not apply on routers)*
```shell
interface vlan 1
ip address [IP_ADDRESS] [SUBNET_MASK]
no shutdown
exit

ip default-gateway [GATEWAY_IP]
```

## Default Route
```shell
ip route 0.0.0.0 0.0.0.0 [EXIT_INTERFACE]
```

## Save Configuration
```shell
write memory
```
or
```shell
copy running-config startup-config
```

## Router Interfaces

### Gateway Interface
```shell
interface g0/0/0
ip address [IP_ADDRESS] [SUBNET_MASK]
no shutdown
exit
```

### Serial Interfaces
```shell
interface s0/0/0
ip address [IP_ADDRESS] [SUBNET_MASK]
clock rate 64000  # Only if clock is required
no shutdown
exit
```

## DHCP Configuration on Router

### Step 1 – Exclude Addresses
```shell
ip dhcp excluded-address 192.168.16.254
```

### Step 2 – Create DHCP Pool
```shell
ip dhcp pool DHCP_POOL_NAME
network 192.168.16.0 255.255.255.0
default-router 192.168.16.254
dns-server 10.10.10.250
exit
```

## VLANs on Switches

### Step 1: Create VLAN
```shell
vlan 10
exit
```

### Step 2: Assign VLAN to Interfaces
```shell
interface range Fa0/5-8
switchport mode access
switchport access vlan 10
exit
```

### VLAN 99 Example: Create VLAN, Assign IP, Set Default Gateway
```shell
vlan 99
exit
interface vlan 99
ip address 30.30.30.253 255.255.255.0
exit
ip default-gateway 30.30.30.254
```

## Trunk Configuration on Switch

### Create Trunk on Interface Connected to Router
```shell
interface G0/1
switchport mode trunk
switchport trunk allowed vlan 10-99
exit
```

## Router on a Stick (ROAS) Configuration

### Step 1: Activate Main Interface
```shell
interface G0/0/0
no shutdown
exit
```

### Step 2: Create Subinterface
```shell
interface G0/0/0.10
encapsulation dot1q 10
ip address 10.10.0.126 255.255.255.128
exit
```
