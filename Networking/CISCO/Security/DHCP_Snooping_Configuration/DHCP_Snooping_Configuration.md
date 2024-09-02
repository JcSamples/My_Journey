
# Enabling DHCP Snooping - Configuration Guide

To configure DHCP Snooping on your network switch, follow these steps:

## Step 1: Enable DHCP Snooping Globally
First, enable DHCP Snooping on the switch at a global configuration level.

```shell
Switch(config)# ip dhcp snooping
```

## Step 2: Configure Trusted Interfaces
Mark interfaces connected to legitimate DHCP servers or other trusted network devices as trusted interfaces. This is crucial to ensure that DHCP offers from legitimate servers are accepted.

```shell
Switch(config)# interface <interface-id>
Switch(config-if)# ip dhcp snooping trust
```

Example:
```shell
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# ip dhcp snooping trust
```

## Step 3: Limit DHCP Discovery Rate on Untrusted Interfaces
To prevent DHCP starvation attacks, limit the number of DHCP discovery messages that can be received per second on untrusted ports.

```shell
Switch(config)# interface <interface-id>
Switch(config-if)# ip dhcp snooping limit rate <rate>
```

Example:
```shell
Switch(config)# interface gigabitEthernet 0/2
Switch(config-if)# ip dhcp snooping limit rate 15
```

## Step 4: Enable DHCP Snooping on VLANs
Finally, specify the VLANs on which DHCP Snooping should be active.

```shell
Switch(config)# ip dhcp snooping vlan <vlan-id>
```

Example:
```shell
Switch(config)# ip dhcp snooping vlan 1
```

## Explanation and Best Practices

1. **Global DHCP Snooping Activation**: The `ip dhcp snooping` command at the global level enables DHCP Snooping on the entire switch. This command must be issued before any other DHCP Snooping configurations are applied.

2. **Trusted Interfaces**: Trusting the correct interfaces is critical to prevent unauthorized DHCP servers from injecting malicious DHCP offers into the network. Typically, only ports leading to known DHCP servers or uplinks to other trusted network segments are marked as trusted.

3. **Rate Limiting**: The rate-limiting feature helps mitigate DHCP starvation attacks by limiting the number of DHCP requests an interface can process per second. It is recommended to set this rate based on the expected number of DHCP clients and the overall network traffic.

4. **VLAN Configuration**: Applying DHCP Snooping on specific VLANs ensures that only legitimate DHCP traffic is allowed within those VLANs. It also provides granularity in managing DHCP traffic across different segments of the network.

## Sample Configuration Block
```shell
Switch(config)# ip dhcp snooping
Switch(config)# interface gigabitEthernet 0/1
Switch(config-if)# ip dhcp snooping trust
Switch(config)# interface gigabitEthernet 0/2
Switch(config-if)# ip dhcp snooping limit rate 15
Switch(config)# ip dhcp snooping vlan 1
Switch(config)# ip dhcp snooping vlan 10
```

This configuration ensures that DHCP Snooping is active on VLANs 1 and 10, with trusted and rate-limited interfaces properly configured.
