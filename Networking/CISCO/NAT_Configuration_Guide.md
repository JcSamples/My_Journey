
# NAT Configuration Commands

This guide provides the necessary commands to configure and verify NAT (Network Address Translation) on a router. The commands are organized into blocks for easier understanding and execution.

## 1. Static NAT

### Verification Commands

```bash
show ip nat translations
show ip nat statistics
```

These commands allow you to verify the NAT translations and statistics.

### Configuration Commands

To set up a static NAT (1:1 mapping), where each internal IP address is mapped to a unique external IP address, follow these steps:

1. Enter global configuration mode:

    ```bash
    conf t
    ```

2. Specify the inside interface:

    ```bash
    interface g0/0
    ip nat inside
    ```

3. Configure the static NAT mapping:

    ```bash
    ip nat inside source static (local-ip) (global-ip)
    ```

## 2. Dynamic NAT Using Access Control List (ACL)

If multiple machines need to use NAT, you can create a standard ACL to define which internal IP addresses are allowed to be translated. Here is a basic outline of the steps:

1. Create a standard ACL:

    ```bash
    access-list 1 permit (local-ip-range)
    ```

2. Configure dynamic NAT using the ACL:

    ```bash
    ip nat inside source list 1 pool (pool-name)
    ```

3. Define the NAT pool:

    ```bash
    ip nat pool (pool-name) (start-ip) (end-ip) netmask (netmask)
    ```

4. Specify the inside and outside interfaces:

    ```bash
    interface g0/0
    ip nat inside

    interface g0/1
    ip nat outside
    ```

### Final Verification

After setting up, you can use the following commands to verify the NAT configuration and its operation:

```bash
show ip nat translations
show ip nat statistics
```
