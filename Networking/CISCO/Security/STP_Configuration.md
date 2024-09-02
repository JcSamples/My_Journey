
# STP Mitigation Configuration Commands

## Configuration of Interface Settings

```
S1(config)# interface fa0/1
S1(config-if)# switchport mode access
S1(config-if)# spanning-tree portfast
```

### Explanation:
The above commands configure FastEthernet0/1 as an access port and enable 
PortFast. PortFast allows the port to bypass the listening and learning 
states of STP, which is useful for ports connected to a single host device. 
**WARNING**: Enabling PortFast on ports connected to multiple devices like hubs or switches 
can cause bridging loops.

## Exiting Interface Configuration Mode

```
S1(config-if)# exit
```

## Enabling PortFast Globally on All Access Ports

```
S1(config)# spanning-tree portfast default
```

### Explanation:
This command enables PortFast by default on all access ports. However, 
you should disable PortFast on ports connected to other switches, hubs, or bridges 
to prevent potential bridging loops.

## Exiting Global Configuration Mode

```
S1(config)# exit
```

## Displaying Spanning Tree Configuration

```
S1# show running-config | begin span
```

### Explanation:
This command displays the running configuration starting from the spanning-tree configuration section.

## Sample Output:

```
spanning-tree mode pvst
spanning-tree portfast default
spanning-tree extend system-id
```

### Note:
The above output shows that the switch is running in Per-VLAN Spanning Tree (PVST) mode, 
with PortFast enabled by default and the system ID extension configured.

