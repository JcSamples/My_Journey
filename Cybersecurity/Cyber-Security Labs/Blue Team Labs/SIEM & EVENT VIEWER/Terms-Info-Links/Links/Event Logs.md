
[https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4625](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventid=4625)


### SPLUNK
https://www.splunk.com/en_us/blog/security/hunting-for-malicious-powershell-using-script-block-logging.html
### Powershell script by Alex Teixeira



https://github.com/splunk/security_content/blob/develop/detections/endpoint/powershell_4104_hunting.yml

### Get Invoke-SPLPowerShellAuditLogging here.

![](Pasted%20image%2020240616171208.png)


Update a currently used Windows inputs.conf on the Splunk Universal Forwarder or use Invoke-SPLPowerShellAuditLogging to create the inputs. 
````
Update a currently used Windows inputs.conf on the Splunk Universal Forwarder or use Invoke-SPLPowerShellAuditLogging to create the inputs. 

[WinEventLog://Microsoft-Windows-PowerShell/Operational]
source = XmlWinEventLog:Microsoft-Windows-PowerShell/Operational
renderXml = 0
disabled = false
index = win   

[monitor://c:\pstransactions\]
sourcetype = powershell:transcript
disabled = false
multiline_event_extra_waittime = true
time_before_close = 300
index = win

`Invoke-SPLPowerShellAuditLogging -method CreateInputs`
`````


### ATOMIC RED TEAM SCRIPTING

https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1059.001/T1059.001.md

![](Pasted%20image%2020240616171438.png)

````
IEX (IWR 'https://raw.githubusercontent.com/redcanaryco/invoke-atomicredteam/master/install-atomicredteam.ps1' -UseBasicParsing);
`````


````powershell
Install-AtomicRedTeam -getAtomics -force
`````

````powershell
invoke-AtomicTest T1059.001
`````

