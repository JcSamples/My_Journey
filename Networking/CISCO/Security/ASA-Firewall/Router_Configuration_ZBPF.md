
# Router Configuration for Zone-Based Policy Firewall (ZBPF)

## Block 1: Initial Setup

```bash
# Enable privileged EXEC mode
Router>enable

# Enter global configuration mode
Router#configure terminal

# Configure GigabitEthernet 0/0 interface
Router(config)#interface GigabitEthernet0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#exit

# Configure GigabitEthernet 0/1 interface
Router(config)#interface GigabitEthernet0/1
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.3.1 255.255.255.0
Router(config-if)#exit

# Configure Serial 0/1/0 interface
Router(config)#interface Serial0/1/0
Router(config-if)#no shutdown
Router(config-if)#ip address 10.1.1.1 255.255.255.252
Router(config-if)#exit
```

## Block 2: OSPF Routing Configuration

```bash
# Configure OSPF routing for different networks
Router(config)#router ospf 1
Router(config-router)#network 192.168.1.0 0.0.0.255 area 0
Router(config-router)#network 10.1.1.0 0.0.0.3 area 0
Router(config-router)#network 192.168.3.0 0.0.0.255 area 0
Router(config-router)#network 10.2.1.0 0.0.0.3 area 0
Router#write memory  # Save configuration
```

## Block 3: License Activation

```bash
# Activate security license
Router(config)#license boot module c1900 technology-package securityk9
Router#reload  # Reload the router to activate the license
```

## Block 4: Zone-Based Policy Firewall (ZBPF) Setup

```bash
# Configure security zones
Router(config)#zone security IN-ZONE
Router(config-sec-zone)#exit
Router(config)#zone security OUT-ZONE
Router(config-sec-zone)#exit

# Define access list
Router(config)#access-list 101 permit ip 192.168.3.0 0.0.0.255 any

# Create class map
Router(config)#class-map type inspect match-all IN-NET-CLASS-MAP
Router(config-cmap)#match access-group 101
Router(config-cmap)#exit

# Create policy map
Router(config)#policy-map type inspect IN-2-OUT-PMAP
Router(config-pmap)#class type inspect IN-NET-CLASS-MAP
Router(config-pmap-c)#inspect
Router(config-pmap-c)#exit
Router(config-pmap)#exit

# Configure zone pairs
Router(config)#zone-pair security IN-2-OUT-ZPAIR source IN-ZONE destination OUT-ZONE
Router(config-sec-zone-pair)#service-policy type inspect IN-2-OUT-PMAP
Router(config-sec-zone-pair)#exit
```

## Block 5: Assign Interfaces to Security Zones

```bash
# Assign GigabitEthernet 0/1 to IN-ZONE
Router(config)#interface GigabitEthernet0/1
Router(config-if)#zone-member security IN-ZONE
Router(config-if)#exit

# Assign Serial 0/1/1 to OUT-ZONE
Router(config)#interface Serial0/1/1
Router(config-if)#zone-member security OUT-ZONE
Router(config-if)#exit
Router#write memory  # Save configuration
```

## Block 6: Intrusion Prevention System (IPS) Configuration

```bash
# Configure IPS settings
Router(config)#ip ips config location ipsdir
Router(config)#ip ips name iosips
Router(config)#ip ips signature-category
Router(config-ips-category)#category all
Router(config-ips-category-action)#retired true
Router(config-ips-category-action)#exit
Router(config-ips-category)#category ios_ips basic
Router(config-ips-category-action)#retired false
Router(config-ips-category-action)#exit
Router(config-ips-category)#exit

# Apply IPS to the interface
Router(config)#interface GigabitEthernet0/1
Router(config-if)#ip ips iosips out
Router(config-if)#exit
Router#write memory  # Save configuration
```

## Block 7: Logging Configuration

```bash
# Configure logging to a remote server
Router(config)#logging host 192.168.1.50
Router(config)#service timestamps log datetime msec
Router#write memory  # Save configuration
```
