
````shell
sudo apt-get install -y dpkg
`````

````shell
cd /path/to/downloaded/file
`````

````shell
sudo dpkg -i splunk-9.2.1-78803f08aabb-linux-2.6-amd64.deb
`````

````shell
sudo /opt/splunk/bin/splunk start
`````


![](../../../../Cybersecurity/Imagens/Pasted%20image%2020240616033508.png)

![](Pasted%20image%2020240616033517.png)

![](Pasted%20image%2020240616033525.png)

![](Pasted%20image%2020240616033531.png)

![](Pasted%20image%2020240616033537.png)

![](Pasted%20image%2020240616033543.png)

![](Pasted%20image%2020240616033548.png)

### Go to the folder /opt/splunk/bin

````shell
./splunk add forward-server 192.168.192.2:9997
`````

![](Pasted%20image%2020240616033704.png)

Efetuar o Download do Splunk Forwarder
![](Pasted%20image%2020240616035901.png)

![](Pasted%20image%2020240616040239.png)


### Add ingestion logs Syslogs

````
./splunk add monitor /var/log/syslog -index Linux_host
`````

### Confirm the Ingestion on the machine 

````
logger " 1 2 3 Teste"

./splunk add forward-server 192.168.1.47:9997

````
