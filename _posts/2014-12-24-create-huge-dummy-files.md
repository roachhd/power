---
layout: post
title: Creating Huge Dummy Files
---
###### All PowerShell versions

If you need to stress test systems, or need large dummy files for other purposes, here is some code that can create even very large files in a split second:

{% highlight terminal %}
$Path = "$env:temp\hugefile.txt"
$Size = 200MB

$stream = New-Object System.IO.FileStream($Path, [System.IO.FileMode]::CreateNew)
$stream.Seek($Size, [System.IO.SeekOrigin]::Begin)
$stream.WriteByte(0)
$Stream.Close()

explorer.exe "/select,$Path" 
{% endhighlight %}

---

###### Post tip #1
