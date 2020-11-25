# Some usefull cmd tips
## Associate network share to letter
net use w: \\int.ofac.ch\OFAC\Collaborateurs\henriet\workspace
## Wait for 1 second
ping localhost -n 1 -w 1000 > nul
## Delete letter association (with network share)
net use w: /d

# PowerShell
## Curl
     Invoke-WebRequest -Uri "http://www.contoso.com" -OutFile "C:\path\file"

With credentials:

     Invoke-WebRequest -Uri https://www.contoso.com/ -OutFile C:"\path\file" -Credential "yourUserName"
or

     $Credentials = Get-Credential
     Invoke-WebRequest -Uri "https://www.contoso.com" -OutFile "C:\path\file" -Credential $Credentials

Other form

     Invoke-WebRequest "http://www.contoso.com" | Select-Object -ExpandProperty Content | Out-File "file"
     Invoke-WebRequest "http://www.contoso.com" -OutFile "file" -PassThru | Select-Object -ExpandProperty Content

## Grep
kubectl logs -f (kubectl get pod | where {$_ -match 'chaos'}).Split(" ")[0]

## Delete Cortona
    Get-appxpackage -allusers *Microsoft.549981C3F5F10* | Remove-AppxPackage

## Network
### Disable a network adapter PowerShell :
     Get-NetAdapter | format-list
     Disable-NetAdapter -Name "your network adapter name" -Confirm:$false
     Enable-NetAdapter -Name "your network adapter name" -Confirm:$false
### 
     netsh interface show interface
     netsh interface set interface "Ethernet" disable
     netsh interface set interface "Interface Name" enable
