
# Network Configuration Commands

## Router Configuration

### Enable Router and Enter Global Configuration Mode
```plaintext
RouterA> enable
RouterA# configure terminal
```

### Configure Gigabit Ethernet Interface
```plaintext
RouterA(config)# interface GigabitEthernet0/0
RouterA(config-if)# no shutdown
RouterA(config-if)# ip address 192.168.0.2 255.255.255.0
RouterA(config-if)# exit
```

### Enable AAA and Local Authentication
```plaintext
RouterA(config)# aaa new-model
RouterA(config)# aaa authentication login default local
RouterA(config)# aaa authentication login telnet-login local
RouterA(config)# aaa authentication login ssh-login local
```

### Create a Local User with Privilege Level
```plaintext
RouterA(config)# username UserX privilege 15 password SecurePass123
```

### Set the Enable Secret Password
```plaintext
RouterA(config)# enable secret SuperSecret123
```

### Configure Console and VTY Lines for Authentication
```plaintext
RouterA(config)# line console 0
RouterA(config-line)# login authentication default
RouterA(config-line)# exit
RouterA(config)# line vty 0 4
RouterA(config-line)# login authentication telnet-login
RouterA(config-line)# login authentication ssh-login
RouterA(config-line)# exit
```

### Save Configuration and Exit
```plaintext
RouterA# write memory
RouterA# exit
```

## SSH Configuration

### Set Hostname and Domain Name
```plaintext
RouterA(config)# hostname Central_Router
RouterA(config)# ip domain-name example.com
```

### Generate RSA Key for SSH
```plaintext
RouterA(config)# crypto key generate rsa
```

### Enable SSH Input on VTY Lines
```plaintext
RouterA(config)# line vty 0 4
RouterA(config-line)# transport input ssh
RouterA(config-line)# exit
```

### Save Configuration and Exit
```plaintext
Central_Router# write memory
Central_Router# exit
```

## RADIUS Configuration on Switch

### Enable RADIUS and Set Authentication
```plaintext
SwitchA(config)# aaa new-model
SwitchA(config)# aaa authentication login console-login group radius
SwitchA(config)# aaa authentication login telnet-login group radius
SwitchA(config)# aaa authentication login ssh-login group radius
```

### Configure RADIUS Server Details
```plaintext
SwitchA(config)# radius-server host 192.168.0.1 auth-port 1645 key SuperSecretKey
```

### Configure Console and VTY Lines for RADIUS Authentication
```plaintext
SwitchA(config)# line console 0
SwitchA(config-line)# login authentication console-login
SwitchA(config-line)# exit
SwitchA(config)# line vty 0 4
SwitchA(config-line)# login authentication telnet-login
SwitchA(config-line)# login authentication ssh-login
SwitchA(config-line)# exit
```

### Save Configuration and Exit
```plaintext
SwitchA# write memory
SwitchA# exit
```
