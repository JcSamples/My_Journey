
# IPsec VPN Tunnel Configuration

## Step 1: Configure ISAKMP Policy
```
Router(config)#crypto isakmp policy 1  
Router(config-isakmp)#encryption 3des 
Router(config-isakmp)#authentication pre-share 
Router(config-isakmp)#group 2  (Ensure this matches on both ends)
Router(config-isakmp)#exit
```

## Step 2: Create Pre-shared Key
```
Router(config)#crypto isakmp key SecureKey1234 address 192.168.100.2 
Router(config)#crypto ipsec security-association lifetime seconds 86400  (Equivalent to 24 hours)
```

## Step 3: Define IPSec Transform Set
```
Router(config)#crypto ipsec transform-set ProjectX esp-aes esp-sha-hmac 
```

## Step 4: Create Crypto Map and Associate Peer
```
Router(config)#crypto map SecurityMap 100 ipsec-isakmp
Router(config-crypto-map)#set peer 192.168.100.2 
Router(config-crypto-map)#set pfs group2 
Router(config-crypto-map)#set security-association lifetime seconds 86400
Router(config-crypto-map)#set transform-set ProjectX
Router(config-crypto-map)#match address ACL_Customers  (We will create this ACL next)
```

## Step 5: Apply Crypto Map to Interface
```
Router(config-if)#crypto map SecurityMap
```

## Step 6: Create Static Route
```
Router(config)#ip route 192.168.2.0 255.255.255.0 192.168.100.2
```

## Step 7: Create Access Control List (ACL)
```
Router(config)#ip access-list extended ACL_Customers
Router(config-ext-nacl)#permit ip 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255
```
*(Source: 192.168.1.0/24, Destination: 192.168.2.0/24)*

## Step 8: Reverse Process on the Adjacent Router

## Step 9: Verify Tunnel Status
```
Router#show crypto isakmp sa
Router#show crypto ipsec sa
```
