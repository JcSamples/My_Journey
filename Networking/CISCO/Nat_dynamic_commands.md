
## NAT Dynamic Commands and Configuration

### Show NAT Translations
```bash
sh ip nat translations
```

### Show NAT Statistics
```bash
sh ip nat statistics
```

### NAT Creation
#### Start to End Configuration
```bash
Router(config)#ip nat pool Mypool 89.123.10.50 89.123.10.55 netmask 255.255.255.0
```

### Create Access Control List (ACL)
```bash
Router(config)#access-list 1 permit 192.168.5.0 0.0.0.255
# (This ACL allows traffic from our network)
```

### Associate ACL to NAT Pool
```bash
Router(config)#ip nat inside source list 1 pool Mypool
```

### Note
In this case, the interface is only used when performing PAT (Port Address Translation).
