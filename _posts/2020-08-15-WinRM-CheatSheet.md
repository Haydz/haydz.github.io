---
layout: posts
title: "WinRM Cheatsheet & PowerShell Syntax"
---

I've been doing some PowerShell exercises within the ![Mosse Cyber Security Institute](https://www.mosse-institute.com/) Online Platform. Most exercises require demonstrating the PowerShell executing locally and remotely so this is a cheatsheet for enabling WinRM/PS-Remoting.



Side note:  
* ISE does not have line wrapping. See ![here](https://superuser.com/questions/871178/line-wrapping-in-powershell-ise-console)



#To Enable PSRemoting
```powershell
Enable-PSRemoting -Force
```


#Adding a trusted host
If the machine is not connected to the Domain, you will need to adda  trusted host.


```powershell
winrm s winrm/config/client '@{TrustedHosts="172.16.2.30"}'^C
```
{% highlight powershell linenos %}
{% endhighlight %}