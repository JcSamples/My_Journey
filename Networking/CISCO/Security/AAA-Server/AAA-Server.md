
# Router Configuration Commands

## 1. Enable Privileged EXEC Mode
```
Router>enable
```

## 2. Enter Global Configuration Mode
```
Router#configure terminal
```

## 3. Configure GigabitEthernet0/0 Interface
```
Router(config)#interface GigabitEthernet0/0
Router(config-if)#no shutdown
Router(config-if)#ip address 192.168.0.2 255.255.255.0
Router(config-if)#exit
```

## 4. Enable AAA (Authentication, Authorization, and Accounting)
```
Router(config)#aaa new-model
```

## 5. Configure AAA Authentication
```
Router(config)#aaa authentication login default local
Router(config)#aaa authentication login telnet-login local
Router(config)#aaa authentication login ssh-login local
```

## 6. Create a Local User
```
Router(config)#username user_test privilege 15 password secure_pass_123
```

## 7. Set Enable Secret Password
```
Router(config)#enable secret secure_enable_123
```

## 8. Configure Console and VTY Lines for Authentication
```
Router(config)#line console 0
Router(config-line)#login authentication default
Router(config)#line vty 0 4
Router(config-line)#login authentication telnet-login
Router(config-line)#login authentication ssh-login
```

## 9. Save the Configuration
```
Router#wr
```

## 10. Verify Configuration and Exit
```
Router#sh run
Router#exit
```

## 11. Change Hostname and Generate RSA Key for SSH
```
Router(config)#hostname Central_Router
Router(config)#ip domain-name example-domain.com
Router(config)#crypto key generate rsa
```

## 12. Configure VTY for SSH Only
```
Router(config)#line vty 0 4
Router(config-line)#transport input ssh
```

## 13. Save the Configuration Again
```
Central_Router#wr
```

## 14. Additional Show Commands
```
Central_Router#show users
```

# Notes:
- **Usernames, passwords, and domain names** have been anonymized.
- Ensure all passwords are complex and stored securely.
- Regularly update configurations to adhere to the latest security standards.
