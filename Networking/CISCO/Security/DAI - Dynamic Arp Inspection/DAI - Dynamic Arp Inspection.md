
# Network Security Configuration

---

## Block 1: Enable DHCP Snooping Globally

This block enables DHCP snooping across the entire switch.

```bash
# Enter global configuration mode on the switch "SwitchA"
SwitchA(config)# ip dhcp snooping
```

**Explanation:**
- This command enables DHCP snooping, which is used to prevent rogue DHCP servers from interfering with network operations.

---

## Block 2: Configure Interface Range for Trust

In this block, you'll configure a range of interfaces to trust DHCP snooping and Dynamic ARP Inspection (DAI).

```bash
# Enter interface configuration mode for interface range g1/1 - 2 on "SwitchA"
SwitchA(config)# interface range g1/1 - 2

# Trust the interfaces for both DHCP snooping and DAI
SwitchA(config-if-range)# ip dhcp snooping trust
SwitchA(config-if-range)# ip arp inspection trust

# Exit interface configuration mode
SwitchA(config-if-range)# exit
```

**Explanation:**
- These commands configure the specified interfaces (g1/1 - 2) to be trusted for both DHCP snooping and DAI, which means they will be allowed to forward DHCP messages and ARP packets.

---

## Block 3: Enable DHCP Snooping and DAI for Specific VLANs

This block enables DHCP snooping and DAI for specific VLANs.

```bash
# Enable DHCP snooping for VLANs 10, 20, 30-49 on "SwitchA"
SwitchA(config)# ip dhcp snooping vlan 10,20,30-49

# Enable DAI for the same VLANs
SwitchA(config)# ip arp inspection vlan 10,20,30-49
```

**Explanation:**
- These commands enable DHCP snooping and Dynamic ARP Inspection (DAI) on the specified VLANs (10, 20, 30-49). This configuration ensures that only legitimate DHCP and ARP traffic is allowed on these VLANs.

---

**Notes:**
- Ensure you replace `"SwitchA"` with the actual name or identifier of your switch.
- The interface range and VLANs should be adapted according to your specific network configuration.
