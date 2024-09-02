
# ASA Configuration Guide

## VLAN Configuration

In this setup, VLAN 2 is connected to the exterior, and VLAN 1 is for internal use. DHCP is already active, and we need to connect the interface `eth0/2`, which is on VLAN 1.

## Static Route Configuration on Router

```shell
# Configure IP address and enable the interface
fictionalASA(config-if)# ip address 5.5.5.1 255.255.255.252
fictionalASA(config-if)# no shutdown

# Create a static route
fictionalASA(config)# route outside 0.0.0.0 0.0.0.0 5.5.5.2
```

## Web-VPN Configuration

```shell
# Enable WebVPN on the outside interface
fictionalASA(config)# webvpn
fictionalASA(config-webvpn)# enable outside
```

## Access Group Creation

```shell
# Create an internal group policy
fictionalASA(config)# group-policy Group1 internal 
fictionalASA(config)# group-policy Group1 attributes 

# Specify VPN tunnel protocols
fictionalASA(config-group-policy)# vpn-tunnel-protocol ssl-clientless webvpn 

# Associate URL list with the group policy
fictionalASA(config-group-webvpn)# url-list value Site1
```

## User Configuration

```shell
# Create a user with a password
fictionalASA(config)# username User1 password SecurePass123

# Assign the user to the group policy
fictionalASA(config)# username User1 attributes 
fictionalASA(config-username)# vpn-group-policy Group1

# Configure tunnel group for remote access
fictionalASA(config)# tunnel-group Group1 type remote-access
fictionalASA(config)# tunnel-group Group1 general-attributes

# Set the default group policy
fictionalASA(config-tunnel-general)# default-group-policy Group1
```

## Bookmark Manager Configuration

1. **Bookmark Title**: `Site1`
2. **URL**: `http://192.168.1.x` (IP of the servers)

## Final Steps

- Restart the packet tracer.
- To access, use the ASA's public IP address.

---

## Example Tunnel Group Commands

```shell
# Tunnel group remote access configuration
fictionalASA(config)# tunnel-group TunnelGroup1 type remote-access
fictionalASA(config)# tunnel-group TunnelGroup1 general-attributes
fictionalASA(config-tunnel-general)# default-group-policy GroupPolicy1
```

## Notes

- Replace `Group1`, `User1`, `SecurePass123`, `Site1`, `TunnelGroup1`, and `GroupPolicy1` with your actual group names, usernames, passwords, and policies for security purposes.
- Ensure the IPs and URLs match your specific network configuration.
