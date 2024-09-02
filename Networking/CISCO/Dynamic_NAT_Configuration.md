
# Dynamic NAT Configuration

## Commands Overview

### Show NAT Translations
```bash
show ip nat translations
```

### Show NAT Statistics
```bash
show ip nat statistics
```

## NAT Configuration

### Create NAT Pool

```bash
Router(config)#ip nat pool Mypool 89.123.10.50 89.123.10.55 netmask 255.255.255.0
```

### Create Access Control List (ACL)

```bash
Router(config)#access-list 1 permit 192.168.5.0 0.0.0.255
```
*This ACL allows traffic from our network.*

### Associate ACL with NAT Pool

```bash
Router(config)#ip nat inside source list 1 pool Mypool
```

*In this case, interfaces are only used when configuring PAT (Port Address Translation).*
