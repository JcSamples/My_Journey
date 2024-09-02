
# NET-BIOS 

NBT-NS cannot be disabled via Group Policy but must be disabled locally on each host. We can do this by opening `Network and Sharing Center` under `Control Panel`, clicking on `Change adapter settings`, right-clicking on the adapter to view its properties, selecting `Internet Protocol Version 4 (TCP/IPv4)`, and clicking the `Properties` button, then clicking on `Advanced` and selecting the `WINS` tab and finally selecting `Disable NetBIOS over TCP/IP`

While it is not possible to disable NBT-NS directly via GPO, we can create a PowerShell script under Computer Configuration --> Windows Settings --> Script (Startup/Shutdown) --> Startup with something like the following:

Code: powershell

```powershell

$regkey = "HKLM:SYSTEM\CurrentControlSet\services\NetBT\Parameters\Interfaces"
Get-ChildItem $regkey |foreach { Set-ItemProperty -Path "$regkey\$($_.pschildname)" -Name NetbiosOptions -Value 2 -Verbose}
````


