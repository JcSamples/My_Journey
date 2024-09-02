
````Powershell
# Script to monitor a specific registry key
$path = "HKCU:\Software\MyTestKey"
$oldValues = Get-ItemProperty -Path $path

# Wait 10 seconds for changes
Start-Sleep -Seconds 10

$newValues = Get-ItemProperty -Path $path

# Compare and display the changes
$differences = Compare-Object -ReferenceObject $oldValues -DifferenceObject $newValues
if ($differences) {
    Write-Output "Changes detected:"
    $differences
} else {
    Write-Output "No changes detected."
}
`````