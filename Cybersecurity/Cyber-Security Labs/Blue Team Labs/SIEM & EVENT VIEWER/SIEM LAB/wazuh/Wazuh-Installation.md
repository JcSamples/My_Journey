
## Wazuh Installation
To install Wazuh, run the following command in your terminal:

````bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
`````

This command downloads and executes the Wazuh installation script with automatic configuration

## ## Extract Installation Files

If you have a tarball with specific Wazuh installation files, extract it using:

````shell
sudo tar -xvf wazuh-install-files.tar
`````


This command unpacks the contents of the `wazuh-install-files.tar` archive.

## Access the Wazuh Interface

Once the installation is complete, you can access the Wazuh web interface through your browser by visiting:

````
https://<your_machine_ip>
`````



![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613224712.png)

Replace `<your_machine_ip>` with the actual IP address of your machine.
### Adding an Agent

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613225027.png)

To add a new agent to Wazuh, follow these steps:

1. In the Wazuh web interface, go to the **Agents** section and follow the prompts to generate the agent installation command.
2. Execute the generated command on the target machine to connect the agent to the Wazuh server.

After setting up the agent, start the Wazuh service on the agent machine:

````Powershell
PS C:\Windows\system32> net start wazuhsvc
`````


Alternatively, you can start the service manually through the Windows Services Manager.

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613225447.png)
![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613225529.png)


# Configuring Agent Rules

1. Navigate to `C:\Program Files (x86)\ossec-agent` on the agent machine.

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613225622.png)

2. Find and open the `ossec.conf` file. **Make a backup** of this file before making any changes.
![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613225725.png)

3. Open the file with Notepad++ or Notepad, ensuring you run the editor as an Administrator.

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613233433.png)

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613234123.png)
![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613234157.png)
# Configuring Event Ingestion (e.g., Sysmon)

1. Open **Event Viewer** on the agent machine.

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613233031.png)


2. Right-click on the event you want to monitor and select **Properties**

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613233205.png)

3. Copy the event source name.

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613233310.png)

#### In the `ossec.conf` file:

4. Find the relevant section for event monitoring.

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613233821.png)

5. Duplicate an existing entry and replace the source name with the one you copied from Event Viewer.
![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613233927.png)

After saving your changes:

6. Restart the Wazuh service on the agent machine via the Windows Services Manager or using the command line.

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240614222820.png)

### Updating Server Configuration

On the Wazuh server, back up the current configuration file:
![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613234456.png)

````sh
cp /var/ossec/etc/ossec.conf ~/ossec-backup.conf
`````

Look for the following parameters and set them:

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613234624.png)
````
<global>
  <logging>
    <logall>yes</logall>
    <logall_json>yes</logall_json>
  </logging>
</global>
`````


![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613235020.png)

After editing the configuration file, restart the Wazuh service:

````bash
systemctl restart wazuh
`````


### Configuring Filebeat for Log Archiving

To ensure Wazuh logs are archived in `/var/logs/archives`, edit the Filebeat configuration:

````shell
nano /etc/filebeat/filebeat.yml
`````

````
enabled: true
`````

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613234937.png)


![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613235038.png)

Save and exit the file.

### Creating a New Index in Kibana

To store and visualize Wazuh logs:

1. Go to the Wazuh Dashboard.

2. Navigate to **Stack Management** > **Index Patterns**.
![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613235323.png)
![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613235341.png)

3. Create a new index pattern, using `wazuh-archives-**` as the pattern name to match all Wazuh archive logs.
![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613235402.png)

![](../../../../../../Cybersecurity/Imagens/Pasted%20image%2020240613235421.png)
4. Save the new index pattern.
5. 
This setup allows you to query and visualize Wazuh logs in Kibana.
