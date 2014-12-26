---
layout: post
title: Setting Permissions in AD or Windows Registry
categories: [active directory]
share: true
comment: true
---
###### ActiveDirectory Module

We already illustrated previously how you can use `Get/Set-Acl` to read and write permissions to files and folders.

The truth is that both `cmdlets` can deal with any valid PowerShell path. So you can use them in the exact same way to read, clone, and write permissions in the Windows Registry.


###### This example reads existing security information from a Registry key, and applies it to another:

{% highlight powershell %}
# both Registry keys must exist
$KeyToCopySecurityFrom = 'HKLM:\Software\Key1'
$KeyToCopySecurityTo = 'HKLM:\Software\Key1'

$securityDescriptor = Get-Acl -Path $KeyToCopySecurityFrom
Set-Acl -Path $KeyToCopySecurityTo -AclObject $securityDescriptor
{% endhighlight %}

Likewise, if you have installed the `RSAT` tools from Microsoft and enabled the ActiveDirectory PowerShell module, you can use its PowerShell drive AD: to do the very same with AD objects, and for example, clone delegation privileges from one OU to another.

Active Directory features like control of delegation, or accidental deletion prevention, really are just security settings that you now can read, change, and re-apply as needed.


###### Import-Module ActiveDirectory

{% highlight powershell %}
# both OUs must exist
$OUtoCopyFrom = 'AD:\OU=Employees,DC=TRAINING,DC=POWERSHELL'
$OUtoCopyTo = 'AD:\OU=TestEmployees,DC=TRAINING,DC=POWERSHELL'

$securityDescriptor = Get-Acl -Path $OUtoCopyFrom
Set-Acl -Path $OUtoCopyTo -AclObject $securityDescriptor
{% endhighlight %}

You can read and write security to any AD object that way, including DNS information. All you need is the LDAP path to the particular object you want to read or change.


---

###### Power Tip #3

---
