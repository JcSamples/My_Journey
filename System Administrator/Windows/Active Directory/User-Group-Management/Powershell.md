
## **AD User Commands**
### Add a user to AD and set attributes.

````powershell
New-ADUser -Name "first last" -Accountpassword (Read-Host -AsSecureString "Super$ecurePassword!") -Enabled $true -OtherAttributes @{'title'="Analyst";'mail'="f.last@domain.com"}
`````

 
#### Removes a user from AD with the identity of 'name'.

````powershell
Remove-ADUser -Identity <name>
`````

#### Unlocks a user account with the identity of 'name'.

````powershell
Unlock-ADAccount -Identity <name>
`````

#### Set the password of an AD user to the password specified.

````powershell
Set-ADAccountPassword -Identity <'name'> -Reset -NewPassword (ConvertTo- SecureString -AsPlainText "NewP@ssw0rdReset!" -Force)
`````

#### Force a user to change their password at next logon attempt.

````powershell
Set-ADUser -Identity amasters -ChangePasswordAtLogon $true
`````

## **AD Groups Commands**

#### Create a new AD OU container named "name" in the path specified.

````powershell
New-ADOrganizationalUnit -Name "name" -Path "OU=folder,DC=domain,DC=local"
`````

#### Create a new security group named "name" with the accompanying attributes.

````powershell
New-ADGroup -Name "name" -SamAccountName analysts -GroupCategory Security - GroupScope Global -DisplayName "Security Analysts" -Path "CN=Users,DC=domain,DC=local" -Description "Members of this group are Security Analysts under the IT OU"
`````

#### Add an AD user to the group specified.

````powershell
Add-ADGroupMember -Identity 'group name' -Members 'ACepheus,OStarchaser,ACallisto'
`````


## **GPO Commands**

#### Copy a GPO for use as a new GPO with a target name of "name"

````powershell
Copy-GPO -SourceName "GPO to copy" -TargetName "Name"
`````

Links an existing GPO to the specified OU path. The "-LinkEnabled Yes" ensures that once the link has been established, that the GPO and it's policies are actually enabled (as it is possibe for a GPLink to exist, but at the same time be disabled.)

````powershell
New-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" - LinkEnabled Yes
`````


#### Link an existing GPO for use to a specific OU or security group.

````powershell
Set-GPLink -Name "Security Analysts Control" -Target "ou=Security Analysts,ou=IT,OU=HQ-NYC,OU=Employees,OU=Corp,dc=INLANEFREIGHT,dc=LOCAL" - LinkEnabled Yes
`````

#### Add a new computer to the domain using the credentials specified.

````powershell
Add-Computer -DomainName 'INLANEFREIGHT.LOCAL' -Credential 'INLANEFREIGHT\HTB- student_adm' -Restart
`````



