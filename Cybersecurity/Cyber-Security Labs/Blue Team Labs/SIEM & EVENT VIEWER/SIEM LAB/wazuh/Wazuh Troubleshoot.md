
- Verify that the Wazuh dashboard configuration file has the correct Wazuh indexer IP:  

````shell
    File: "/etc/wazuh-dashboard/opensearch_dashboards.yml"  
    Line: "opensearch.hosts: https://<wazuh-indexer-ip>:9200"
`````

- Verify that you have connectivity between the Wazuh dashboard node and the Wazuh indexer node:  

````shell
curl -v telnet://<wazuh-indexer-ip>:9200
`````

- Check Wazuh dashboard service status is active  

````Shell
systemctl status wazuh-dashboard
`````


- Check Wazuh indexer service status is active  
````
systemctl status wazuh-indexer
`````

- If the status is not active, then check possible issues reported in Wazuh indexer log file  
````Shell
cat /var/log/wazuh-indexer/<cluster-name>.log | grep -E "ERROR|WARN|Caused"
`````

