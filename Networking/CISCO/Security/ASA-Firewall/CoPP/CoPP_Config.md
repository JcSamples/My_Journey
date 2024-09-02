
# Control Plane Policing (CoPP) Configuration


### Default CoPP Configuration

CoPP is enabled by default. To disable the default CoPP configuration, use the following command:

```bash
no service-policy input policy-default-autocopp
```

This command should be run in control plane configuration mode.

### CoPP Class Maps

Here are the default CoPP class maps organized into blocks:

#### ICMP and Network Failures

```bash
class-map match-any class-icmp-redirect-unreachable
class-map match-all class-network-glean
class-map match-all class-receive-errors
class-map match-all class-options-errors
class-map match-all class-broadcast
class-map match-all class-multicast-acl-bridged
class-map match-all class-slow-balancing
class-map match-all class-mtu-failures
class-map match-all class-ttl-failures
class-map match-all class-arp-snooping
class-map match-any class-multicast-copy
```

#### IP and Protocol Matching

```bash
class-map match-any class-ip-connected
class-map match-any class-igmp-matching
 match access-group name acl-igmp-matching
class-map match-all class-unknown-protocol
class-map match-any class-vacl-log
```

#### IPv6 and Multicast

```bash
class-map match-all class-ipv6-multicast-control
class-map match-any class-pimv6-data-matching
 match access-group name acl-pimv6-data-matching
class-map match-any class-ipv4-multicast-punt
```

#### Rewrite and Admission Control

```bash
class-map match-all class-unsupported-rewrite
class-map match-all class-unicast-egress-acl-bridged
class-map match-all class-ip-admission
class-map match-all class-service-insertion
class-map match-all class-mac-pbf
class-map match-any class-mld-matching
 match access-group name acl-mld-matching
```

#### DHCP and ND

```bash
class-map match-all class-dhcp-snooping
class-map match-all class-web-cache-coordination
class-map match-all class-neighbor-discovery
class-map match-any class-ipv6-connected
```

#### Routing and Failures

```bash
class-map match-all class-multicast-rpf-fail
class-map match-any class-unicast-rpf-fail
class-map match-all class-multicast-ip-control
class-map match-any class-pim-data-matching
 match access-group name acl-pim-data-matching
class-map match-any class-ndv6-matching
 match access-group name acl-ndv6-matching
class-map match-any class-multicast-v4-data-on-routed-port
class-map match-any class-multicast-v6-data-on-routed-port
```

### Default CoPP Policy Map

The following is the default CoPP policy map:

```bash
policy-map policy-default-autocopp
 class class-multicast-v4-data-on-routed-port
  police rate 10 pps burst 1 packets
  conform-action drop
  exceed-action drop

 class class-multicast-v6-data-on-routed-port
  police rate 10 pps burst 1 packets
  conform-action drop
  exceed-action drop

 class class-icmp-redirect-unreachable
  police rate 100 pps burst 10 packets
  conform-action transmit
  exceed-action drop

 class class-unicast-rpf-fail
  police rate 100 pps burst 10 packets
  conform-action transmit
  exceed-action drop

 class class-vacl-log
  police rate 2000 pps burst 1 packets
  conform-action transmit
  exceed-action drop

 class class-multicast-punt
  police rate 1000 pps burst 256 packets
  conform-action transmit
  exceed-action drop

 class class-multicast-copy
  police rate 1000 pps burst 256 packets
  conform-action transmit
  exceed-action drop

 class class-ip-connected
  police rate 1000 pps burst 256 packets
  conform-action transmit
  exceed-action drop

 class class-ipv6-connected
  police rate 1000 pps burst 256 packets
  conform-action transmit
  exceed-action drop

 class class-pim-data-matching
  police rate 1000 pps burst 1000 packets
  conform-action transmit
  exceed-action drop

 class class-pimv6-data-matching
  police rate 1000 pps burst 1000 packets
  conform-action transmit
  exceed-action drop

 class class-mld-matching
  police rate 5000 pps burst 5000 packets
  conform-action set-discard-class-transmit 48
  exceed-action transmit

 class class-igmp-matching
  police rate 5000 pps burst 5000 packets
  conform-action set-discard-class-transmit 48
  exceed-action transmit

 class class-ndv6-matching
  police rate 1000 pps burst 1000 packets
  conform-action set-discard-class-transmit 48
  exceed-action drop
```
