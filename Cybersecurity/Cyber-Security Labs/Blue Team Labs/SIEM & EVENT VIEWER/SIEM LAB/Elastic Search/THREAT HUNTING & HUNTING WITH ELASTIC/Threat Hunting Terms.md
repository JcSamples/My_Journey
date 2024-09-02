
- `Adversary`: An adversary, within the realm of Cyber Threat Intelligence (CTI), refers to an entity driven by shared objectives as your organization, albeit unauthorized, seeking to infiltrate your business and satisfy their collection requirements, which may include financial gains, insider information, or valuable intellectual property. These adversaries possess varying levels of technical expertise and are motivated to circumvent your security measures.
    
    Adversaries can be classified into distinct categories, including `cyber criminals`, `insider threats`, `hacktivists`, or `state-sponsored operators`. Each category exhibits unique characteristics and motivations in their pursuit of unauthorized access and exploitation.


IOC - indicator of compromise

Advanced Persistent Threat (APT)~-  APTs are typically associated with highly organized groups or nation-state entities that possess extensive resources, thereby enabling them to carry out their malicious activities over prolonged periods.
they show a marked preference for high-value targets,


TTP - Tactics Techniques Procedures
- `Tactics`: This term describes the strategic objectives and high-level concepts of operations employed by the adversary. Essentially, it addresses the 'why' behind their actions.
- `Techniques`: These are the specific methods utilized by an adversary to accomplish their tactical objectives, providing the 'how' behind their actions. Techniques don't provide step-by-step instructions but rather describe the general approach to achieving a goal.
- `Procedures`: These are the granular, step-by-step instructions, essentially the 'recipe' for the implementation of each technique.



 Cyber Threat Intelligence (CTI)
`Indicator`: An indicator, when analyzed in CTI, encompasses both technical data and contextual information. Isolated technical data lacking relevant context holds limited or negligible value for network defenders. Contextual details allow for a comprehensive understanding of the indicator's significance, enabling effective threat analysis and response

![[JOB/Ciber Segurança/Blue team/SIEM & EVENT VIEWER/SIEM LAB/Elastic Search/THREAT HUNTING & HUNTING WITH ELASTIC/Imagens/Pasted image 20240501122258.png]]


# PYRAMID - INFO RECOVERY
 [Intel-Driven Detection and Response to Increase Your Adversary’s Cost of Operations](https://rvasec.com/slides/2014/Bianco_Pyramid%20of%20Pain.pdf)
 

![[JOB/Ciber Segurança/Blue team/SIEM & EVENT VIEWER/SIEM LAB/Elastic Search/THREAT HUNTING & HUNTING WITH ELASTIC/Imagens/Pasted image 20240501122735.png]]


# CTF-STUDY

`The Available Data`

The cybersecurity strategy implemented is predicated on the utilization of the Elastic stack as a SIEM solution. Through the "Discover" functionality we can see logs from multiple sources. These sources include:

- `Windows audit logs` (categorized under the index pattern windows*)
- `System Monitor (Sysmon) logs` (also falling under the index pattern windows*, more about Sysmon [here](https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon))
- `PowerShell logs` (indexed under windows* as well, more about PowerShell logs [here](https://www.splunk.com/en_us/blog/security/hunting-for-malicious-powershell-using-script-block-logging.html))
- `Zeek logs`, [a network security monitoring tool](https://www.elastic.co/guide/en/beats/filebeat/current/exported-fields-zeek.html) (classified under the index pattern zeek*)
- 
_System Monitor_ (_Sysmon_) is a Windows system service and device driver that, once installed on a system, remains resident across system reboots to monitor and log system activity to the Windows event log. It provides detailed information about process creations, network connections, and changes to file creation time. By collecting the events it generates using [Windows Event Collection](https://msdn.microsoft.com/library/windows/desktop/bb427443(v=vs.85).aspx) or [SIEM](https://en.wikipedia.org/wiki/security_information_and_event_management) agents and subsequently analyzing them, you can identify malicious or anomalous activity and understand how intruders and malware operate on your network. The service runs as a [protected process](https://learn.microsoft.com/en-us/windows/win32/services/protecting-anti-malware-services-#system-protected-process), thus disallowing a wide range of user mode interactions.

Note that _Sysmon_ does not provide analysis of the events it generates, nor does it attempt to hide itself from attackers.