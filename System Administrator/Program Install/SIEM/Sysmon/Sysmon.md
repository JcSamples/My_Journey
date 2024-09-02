
https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon


# Sysinternals Suite

Download Systernals Suite
https://learn.microsoft.com/en-us/sysinternals/downloads/sysinternals-suite
![](Imagens/Pasted%20image%2020240611222350.png)


## Using SwiftOnSecurity sysmon-config

https://github.com/SwiftOnSecurity/sysmon-config

The file should function as a great starting point for system change monitoring in a self-contained and accessible package
Note that this does not track things like authentication and other Windows events that are also vital for incident investigation.

- For a far more exhaustive and detailed approach to Sysmon configuration from a different approach, see also **[sysmon-modular](https://github.com/olafhartong/sysmon-modular)** by [@olafhartong](https://twitter.com/olafhartong), which can act as a superset of sysmon-config.
- Sysmon is a compliment to native Windows logging abilities, not a replacement for it. For valuable advice on these configurations, see **[MalwareArchaeology Logging Cheat Sheets](https://www.malwarearchaeology.com/cheat-sheets)** by [@HackerHurricane](https://twitter.com/hackerhurricane).
-

### Install
Run with administrator rights
````cmd.exe
sysmon.exe -accepteula -i sysmonconfig-export.xml
`````

### Update existing configuration

````
sysmon.exe -c sysmonconfig-export.xml
`````

Uninstall
````
sysmon.exe -u
`````


## TIP use Notepad ++ :
notepad++
https://notepad-plus-plus.org/
