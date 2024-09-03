

Navigate to the bottom of this section and click on `Click here to spawn the target system!`

Now, navigate to `http://[Target IP]:5601`, click on the side navigation toggle, and click on "Discover". Then, click on the calendar icon, specify "last 15 years", and click on "Apply".

Please also specify a `Europe/Copenhagen` timezone, through the following link `http://[Target IP]:5601/app/management/kibana/settings`.


![](../THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501145549.png)

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501145746.png)

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501145814.png)

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501150253.png)

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501151949.png)
	event.code:"15" 


# STEP: 2

## SYSMON EVENT ID: 15 FILE STREAM 
`event.code:"15"  AND file.name:*invoice.one`


![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501152520.png)
![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501152731.png)

````
``event.code:`
    `15`
`file.name:`
    `invoice.one`
`@timestamp:`
    `Mar 26, 2023 @ 22:05:47.793`

`ile.directory:`
    `C:\Users\bob\Downloads`
`file.extension:`
    `one`
`file.hash.md5:`
    `127021207d6415a3b426732b782efc24`
    
`````



**Here we can see that when we search for sysmon 11 "file"**  
**we find an older event**

```shell-session
event.code:11 AND file.name:invoice.one*
```
![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501153743.png)

````

`Mar 26, 2023 @ 22:05:47.789`

`event.code:`
    `11`
`file.name:`
    `invoice.one:Zone.Identifier`
@
`````


##### We can verify that we only have 1 hit

# ANALYSE HOSTNAME

````
Agent hostname:     WS001

event.code:"15"  AND  host.hostname:    WS001



host.ip:
    fe80::1410:a2cc:5d5b:99c7, 
    192.168.28.130, 
    fe80::90be:194f:efaa:df6e, 
    169.254.251.85
host.mac:
    00-0C-29-43-6A-C3, 8C-F8-C5-B6-74-06
host.name:
    WS001.eagle.local
`````


# Sysmon event id 3 : Network checking

(Sysmon Event ID 3) from this machine (execute the following query `event.code:3 AND host.hostname:WS001` and check the `source.ip` field).


event.code:15 AND host.hostname:WS001 AND source.ip:192.168.28.130

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501155258.png)

````
evento criado : Mar 29, 2023 @ 18:54:10.619
indicando que o download foi efetuado nessa altura 
e
encontramos
destination.ip:
    52.113.194.132

88 hits
`````



ZEEK QUERRY

`Zeek query` will search for a source IP matching 192.168.28.130, and since we're querying about DNS queries, we'll only pick logs that have something in the `dns.question.name` field. Note that this will return a lot of common noise, like google.com, etc., so it's necessary to filter that out. Here's the query and some filters.

**Related fields**: [source.ip](https://www.elastic.co/guide/en/ecs/current/ecs-source.html) and [dns.question.name](https://www.elastic.co/guide/en/ecs/current/ecs-dns.html)


```shell-session
source.ip:192.168.28.130 AND dns.question.name:*
```

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501160728.png)

adicionar o filtro e mudar a data de pesquisa

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501161144.png)

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501161537.png)

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501162905.png)


### Filter

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501164230.png)


# After we find the event


```shell-session
event.code:1 AND process.parent.command_line:*invoice.bat*
```
![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501164739.png)
This query returns a single result: the initiation of PowerShell, and the arguments passed to it appear conspicuously suspicious (note that we have added `process.name`, `process.args`, and `process.pid` as columns)!

![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501165049.png)
![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501165107.png)
# Search for powershell events

process.pid:"9944" and process.name:"powershell.exe"


![](Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/SIEM%20LAB/Elastic%20Search/THREAT%20HUNTING%20&%20HUNTING%20WITH%20ELASTIC/Imagens/Pasted%20image%2020240501164427.png)

````
winlog.event_
file.name
@timestamp: Mar 29, 2023 @ 16:28:20.586 
`````


