
````bash
wget http://www.observium.org/observium_installscript.sh 
chmod +x observium_installscript.sh 
./observium_installscript.sh
`````

1. **ManageEngine MibBrowser**:
    
    - Download and install **ManageEngine MibBrowser**.
    - Configure the IP address, SNMP community, and port.
    - Test SNMP connectivity and check if you can retrieve information from the host.

2. **Paessler SNMP Tester**:
    
    - Download and install **Paessler SNMP Tester**.
    - Configure the IP address, SNMP community, and port.
    - Run SNMP tests to verify connectivity.

## On the Client

```bash
sudo apt update
sudo apt install snmp snmpd
```

```bash
sudo nano /etc/snmp/snmpd.conf
```

**Modify the following lines**:

- Comment out the line that makes the SNMP daemon listen only on localhost by adding a `#` at the beginning of the line:
    
    ```bash
    #agentAddress  udp:127.0.0.1:161
    ```
    
- Add the following line so that the SNMP daemon listens on all network interfaces:

    ```bash
    agentAddress udp:161
    ```

- Add the SNMP community configuration to allow read-only access:

    ```bash
    rocommunity public  default    -V systemonly
    ```

Then, restart the SNMP service:

```bash
sudo systemctl restart snmpd
```

Test the SNMP setup:

```bash
snmpwalk -v2c -c public localhost
```

### SNMP Connectivity Troubleshooting

If connectivity tests fail, check the following:

- **Firewall**: Ensure that firewall rules allow SNMP traffic on port 161.
- **SNMP Configuration**: Review the SNMP configuration on the host to ensure the SNMP community and other settings are correct.
- **SNMP Service**: Verify that the SNMP service is running on the host.

### Alternative: HTTP/HTTPS Monitoring

If you cannot resolve the SNMP issues, consider using HTTP/HTTPS monitoring as an alternative to check the basic availability of the host:

1. **Add HTTP/HTTPS Service in Observium**:
    - In the Observium panel, go to **Devices** > **Add Service**.
    - Choose `HTTP` or `HTTPS` as the service to monitor.
    - Configure the IP address or hostname of the device.
