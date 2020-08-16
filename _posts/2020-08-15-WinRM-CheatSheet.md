---
layout: posts
title: "WinRM Cheatsheet & PowerShell Syntax"
---

TL;DR Enable-PSRemoting | Invoke-Command

I've been doing some PowerShell exercises within the [Mosse Cyber Security Institute](https://www.mosse-institute.com/) Online Platform. Most exercises require demonstrating the PowerShell executing locally and remotely so this is a cheatsheet for enabling WinRM/PS-Remoting.



Side note:  
* ISE does not have line wrapping. See [here](https://superuser.com/questions/871178/line-wrapping-in-powershell-ise-console)



#To Enable PSRemoting
```powershell
Enable-PSRemoting -Force
```


#Adding a trusted host
If the machine is not connected to the Domain, you will need to add a   trusted host.

```powershell
winrm s winrm/config/client '@{TrustedHosts="192.5.2.30"}'
```

A great reference for editing the registry is [here](https://blog.netwrix.com/2018/09/11/how-to-get-edit-create-and-delete-registry-keys-with-powershell/)


#Running Remote Commands
Use `Invoke-Command` from [here](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/invoke-command?view=powershell-7)

Such as: 
```powershell
Invoke-Command -ComputerName WINB -ScriptBlock { echo "Hello World"}
```