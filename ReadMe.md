

## PowerShell Scripts


#### Install PowerShell Module for ActiveDirectory
```PowerShell

Install-WindowsFeature RSAT-AD-PowerShell
Import-Module ActiveDirectory
```


#### Active Directory

- Get-ADUser - Reteives AD User account details.

```PowerShell

$ADUsers = Get-ADUser -Filter * -Properties * |
            select Name,
            @{E= 'SamAccountName' ; N= 'User ID' },
            @{E = {if($_.Enabled -eq "True") {return 'Enabled'} else {return 'Disabled'} }; N = 'Status'},
            @{E = 'DistinguishedName'; N = 'Distinguished Name'},
            @{E = 'PasswordNeverExpires'; N = 'Password Nerver Expire'},
            @{E = 'PasswordLastSet'; N = 'Password Last Set'}

$ADUsers | Format-Table

```


 - Export CSV output

```PowerShell
$ADUsers | Export-Csv -Path $env:USERPROFILE\Documents\$env:COMPUTERNAME.csv -NoTypeInformation


```
