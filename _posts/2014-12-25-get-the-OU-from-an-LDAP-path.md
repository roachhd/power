---
layout: post
title: Get the OU from an LDAP Path
---
###### All Versions

To extract certain parts from raw strings, you can often use a combination of text splitting and text substring commands.

For example, to extract the name of the last OU in an LDAP path, here is an approach:

{% highlight powershell %}
$dn = 'OU=Test,OU=People,CN=Testing,OU=Everyone,DC=Company,DC=com'

($dn.Split(',')  -like 'OU=*' ).Substring(3)[0]
{% endhighlight %}

The code will return the name of the last OU in the LDAP path (LDAP paths are read from right to left, so the last OU is the first OU in the string) and can be easily adjusted to extract other parts. For example, replace the index number 0 with -1 to get the first OU in the path.

---
Power Tip #2.
---
