---
layout: post
title: How to configure proxy in Play Framework
date: 2015-06-22 13:56:59.000000000 -03:00
type: post
published: true
status: publish
categories:
- java
- play framework
- programming
- software
comments: true
---
If you are struggling to get Play Framework up and running and you are behind a proxy server here is the solution.
<br />  
  - Go to your Play directory (in my case was:<em> /home/andrealmar/softwares/play</em>)  
  - Create the file <strong>activatorconfig.txt</strong> in<em> ~/.activator/</em> directory  
<br />
```
vim ~/.activator/activatorconfig.txt
```  
<br />
  - Put the configs below inside your activatorconfig.txt

```
This are the proxy settings we use for activator
# Multiple proxy hosts can be used by separating them with a '|' sign
# Do not enclose the proxy host(s) in quotes

-Dhttp.proxyHost=<strong>99.99.99.99 - your proxy IP/host</strong>
-Dhttp.proxyPort=<strong>82 - your proxy PORT</strong>
-Dhttps.proxyHost=<strong>99.99.99.99 - your proxy IP/host</strong>
-Dhttps.proxyPort=<strong>82 - your proxy PORT</strong>
# Here we configure the hosts which should not go through the proxy.  You should include your private network, if applicable.
-Dhttp.nonProxyHosts="localhost|127.0.0.1"
# These are commented out, but if you need to use authentication for your proxy, please fill these out.
-Dhttp.proxyUser=<strong>your network/proxy user</strong>
-Dhttp.proxyPassword=<strong>your network/proxy password</strong>
-Dactivator.timeout=20s
```

And that's it. Now you can use the <em>activator run</em> command and it will pass through your proxy without any problems.<br />
See ya!
