
# BPDU Guard Configuration Example

## Step 1: Enable BPDU Guard on a Specific Interface

```bash
SwitchA(config)# interface fa0/1
SwitchA(config-if)# spanning-tree bpduguard enable
SwitchA(config-if)# exit
```

Explanation:
- **interface fa0/1**: Enter interface configuration mode for interface fa0/1.
- **spanning-tree bpduguard enable**: Enable BPDU Guard on this specific interface.
- **exit**: Exit interface configuration mode.

## Step 2: Enable BPDU Guard Globally for PortFast Interfaces

```bash
SwitchA(config)# spanning-tree portfast bpduguard default
SwitchA(config)# end
```

Explanation:
- **spanning-tree portfast bpduguard default**: Enable BPDU Guard by default on all PortFast-enabled interfaces.
- **end**: Exit global configuration mode.

## Step 3: Verify Spanning Tree Summary

```bash
SwitchA# show spanning-tree summary
```

Expected Output:
```plaintext
Switch is in pvst mode
Root bridge for: none
Extended system ID           is enabled
Portfast Default             is enabled
PortFast BPDU Guard Default  is enabled
Portfast BPDU Filter Default is disabled
Loopguard Default            is disabled
EtherChannel misconfig guard is enabled
UplinkFast                   is disabled
BackboneFast                 is disabled
Configured Pathcost method used is short
(output omitted)
```

Explanation:
- **show spanning-tree summary**: Displays a summary of the current spanning tree configuration, including BPDU Guard status.

## Notes:
- BPDU Guard is a security feature that helps prevent loops by disabling interfaces that receive unexpected BPDU packets.
- PortFast is typically enabled on access ports to allow immediate transition to the forwarding state, bypassing the typical STP stages.
