title: Set Visual Studio 2015 Working with Proxy
date: 2016-11-26

---

This topic is on proxy settings for Visual Studio 2015. I've only test it on ver.2015. Please comment if it works or not on other versions.

Visual Studio 2015 doesn't have proxy settings section in Options menue. But it can be configured in config file. Here is the simple guide.

<!--more-->

1. Open `C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe.config` with administrator privilege.

2. Locate `<system.net>` section. Append the following code inside it.

```
<defaultProxy enabled="true" useDefaultCredentials="true">
    <proxy
        bypassonlocal="True"
        proxyaddress="http://yourproxy:port"
    />
</defaultProxy>
```

3. Save and relaunch Visual Studio 2015.

There are some more options such as:

```
<proxy usesystemdefault="True" />

<bypasslist>
    <add address="[a-z]+.example.com$" />
</bypasslist>
```

Read more on:  
* [Proxy Configuration - MSDN](https://msdn.microsoft.com/en-us/library/dkwyc043(v=vs.110).aspx)  
* [Working in Visual Studio behind the Firewall](https://taeguk.co.uk/blog/working-in-visual-studio-behind-the-firewall/)