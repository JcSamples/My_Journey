
# Sticky keys

Uma característica interessante do sethc.exe é que ele também pode ser usado como uma porta de entrada para explorar o sistema, pois em algumas situações, um usuário mal-intencionado pode substituir o sethc.exe por um prompt de comando (cmd.exe). Isso pode permitir o acesso ao prompt de comando mesmo quando o computador está bloqueado, o que é conhecido como "exploit Sticky Keys".

Por esse motivo, é recomendável que os administradores de sistema protejam o acesso ao sethc.exe e monitorem atividades suspeitas relacionadas a esse arquivo para garantir a segurança do sistema.

Once the machine is rebooted, we can press `Shift` five times on the Windows login screen to invoke `Sticky Keys`. Since the executable has been overwritten, what we get instead is another Command Prompt - this time with `NT AUTHORITY\SYSTEM` permissions. We have bypassed any authentication and now have access to the machine as the super user.

# POWERSHELL DISABLE 

Organizations also often focus on blocking the `PowerShell.exe` executable, but forget about the other [PowerShell executable locations](https://www.powershelladmin.com/wiki/PowerShell_Executables_File_System_Locations) such as `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe` or `PowerShell_ISE.exe`. We can see that this is the case in the `AppLocker` rules shown below. All Domain Users are disallowed from running the 64-bit PowerShell executable located at:

`%SystemRoot%\system32\WindowsPowerShell\v1.0\powershell.exe`

So, we can merely call it from other locations. Sometimes, we run into