
# Sticky keys

An interesting feature of sethc.exe is that it can also be used as an entry point to exploit the system. In some situations, a malicious user might replace sethc.exe with a command prompt (cmd.exe). This can allow access to the command prompt even when the computer is locked, which is known as the "Sticky Keys exploit."

For this reason, it is advisable for system administrators to protect access to sethc.exe and monitor suspicious activities related to this file to ensure system security.

Once the machine is rebooted, we can press `Shift` five times on the Windows login screen to invoke `Sticky Keys`. Since the executable has been overwritten, what we get instead is another Command Prompt - this time with `NT AUTHORITY\SYSTEM` permissions. We have bypassed any authentication and now have access to the machine as the super user.

# POWERSHELL DISABLE 

Organizations also often focus on blocking the `PowerShell.exe` executable, but forget about the other [PowerShell executable locations](https://www.powershelladmin.com/wiki/PowerShell_Executables_File_System_Locations) such as `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe` or `PowerShell_ISE.exe`. We can see that this is the case in the `AppLocker` rules shown below. All Domain Users are disallowed from running the 64-bit PowerShell executable located at:

`%SystemRoot%\system32\WindowsPowerShell\v1.0\powershell.exe`

So, we can merely call it from other locations. Sometimes, we run into
