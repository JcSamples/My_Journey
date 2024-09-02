We start by searching for the file name with event.code 15, where we will filter the file hash

![Pasted image](My_Journey/Cybersecurity/Cyber-Security%20Labs/Blue%20Team%20Labs/SIEM%20&%20EVENT%20VIEWER/1-Image/Pasted%20image%2020240616173909.png)

We had 3 hits.

By analysing these, we can see that the file was downloaded using the Microsoft Edge application.

![Pasted image](../../1-Image/Pasted%20image%20240616174044.png)

_ATTENTION_ This discovery simply shows how the file arrived on the victim's machine; it does not show the execution of the file.

![Pasted image](../../1-Image/Pasted%20image%20240616174430.png)


Let's switch to event.code 11: File create  
Use an asterisk at the end of the file name.

```shell-session
event.code:11 AND file.name:invoice.one*
```

This event points us to the folder:

````Powershell
    C:\Users\bob\Downloads
`````

![Pasted image](../../1-Image/Pasted%20image%20240616174938.png)

## Event.Code 3 in conjunction with the hostname


![Pasted image](../../1-Image/Pasted%20image%20240616175117.png)


 `event.code:3 AND host.hostname:WS001`

By filtering by Source IP, we can access the IP of the WS001 host.

![Pasted image](../../1-Image/Pasted%20image%20240616175531.png)

192.168.23.130


"TIP": If we inspect network connections leveraging [Sysmon Event ID 3](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=90003) (Network connection) around the time this file was downloaded, we'll find that Sysmon has no entries. This is a common configuration to avoid capturing network connections created by browsers, which could lead to an overwhelming volume of logs, particularly those related to our email provider.

This is where Zeek logs prove invaluable. We should filter and examine the DNS queries that Zeek has captured from WS001 during the interval from `22:05:00` to `22:05:48`, when the file was downloaded.

![Pasted image](../../1-Image/Pasted%20image%20240616175815.png)


Filter out trustworthy domains.

![Pasted image](../../1-Image/Pasted%20image%20240616180546.png)

And let's focus on a shorter time frame:

	de `March 26th 2023 @ 22:05:00` to `March 26th 2023 @ 22:05:48`.

![Pasted image](../../1-Image/Pasted%20image%20240616181144.png)

![Pasted image](../../1-Image/Pasted%20image%20240616181848.png)

![Pasted image](../../1-Image/Pasted%20image%20240616183135.png)

After discovering the source of the file download, we can expand the timestamp and remove the `dns.question.name` query.


### PROCESS CREATION - EVENT.CODE 1


````
event.code:1 AND process.command_line:*invoice.one*     
`````


(THIS COULD BE COMMAND_LINE OR POWERSHELL OR EVEN ANOTHER PROCESS)

![Pasted image](../../1-Image/Pasted%20image%20240616184010.png)

![Pasted image](../../1-Image/Pasted%20image%20240616184051.png)
![Pasted image](../../1-Image/Pasted%20image%20240616184730.png)
![Pasted image](../../1-Image/Pasted%20image%20240616184909.png)

Let's check the `Invoice.bat`.

```shell-session
event.code:1 AND process.parent.command_line:*invoice.bat*
```
![Pasted image](../../1-Image/Pasted%20image%20240616191203.png)

In addition to `process.name` and `process.args`, let's introduce `process.pid` and check, starting from the `process.pid`, which commands were executed by PowerShell.


![Pasted image](../../1-Image/Pasted%20image%20240616191955.png)

```shell-session
process.pid:"9944" and process.name:"powershell.exe"
```

![Pasted image](../../1-Image/Pasted%20image%20240616200355.png)
process.name:"default.exe"

![Pasted image](../../1-Image/Pasted%20image%20240616201000.png)
