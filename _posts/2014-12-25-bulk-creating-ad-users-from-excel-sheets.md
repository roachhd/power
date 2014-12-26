---
layout: post
title: Bulk Creating Add Users From Excel Sheets
categories: [Active Directory]
---
###### Active Directory 

To create a large number of new Active Directory users, you can import the user data from a CSV file, for example export an Excel sheet to CSV.

Next, this piece of code will turn the CSV data into real Active Directory user accounts:

{% highlight powershell %}
Import-Csv -Path F:\userlist.csv -UseCulture -Encoding Default |
ForEach-Object {
  
  $_.AccountPassword = $_.AccountPassword | 
                           ConvertTo-SecureString -Force -AsPlainText
  $_ 

} |
New-ADUser -WhatIf 
{% endhighlight %}
All the CSV file needs are column headers that represent the parameters expected by New-ADUser. A very trivial list could use headers like this: 

{% highlight powershell %}
Name,SamAccountName,Description,Company,City,Path,AccountPassword
{% endhighlight %}

Just notice that CSV files by nature can only submit string data types. Since the property AccountPassword needs to be a SecureString datatype, the PowerShell code takes the string from the CSV file and converts it to SecureString before the data is handed over to New-ADUser. 

This technique can be used to polish any raw data before you use it to create the user. 

---

###### Power Tip #4

---

