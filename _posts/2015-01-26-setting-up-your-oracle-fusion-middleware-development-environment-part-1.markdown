---
layout: post
title:  "Setting Up Your Oracle Fusion Middleware
Development Environment - Part 1"
date:   date: 2015-01-26 15:35:32.000000000 -02:00
categories: middleware oracle linux
comments: true
___

Hi,

This series of posts are targeted for the beginners who wants to jump into the Oracle Fusion Middleware world! First of all, if you want to start building things or playing around with Fusion Middleware you will need an environment. I will teach you how to build your OFMW environment who runs on your own laptop or desktop.

I'm assuming that you already have VirtualBox (or VMWare) installed in your laptop / desktop. We gonna do a Virtual Machine with:

*   OEL 7 (Oracle Linux)
*   Weblogic 12c
*   Oracle SOA 12c
*   Oracle BPM 12c

Maybe we will add other products in the Oracle Fusion Middleware stack.

Let's start with installing our OS (Operational System) which in our case will be Oracle Enterprise Linux 7\. So, follow along the steps below and be happy =)

Boot your VM with the .iso file of OEL 7 and hit Install Oracle Linux 7.0

![oel-1]({{ site.url }}/assets/images/oel-1.png)


Select your language

![oel-2]({{ site.url }}/assets/images/oel-2.png)

Select your timezone

![oel-3]({{ site.url }}/assets/images/oel-3.png)

After that you have to set up some configurations before click Install.

![oel-4]({{ site.url }}/assets/images/oel-4.png)

Once you click Begin Installation, it starts to Install the Operational System. Then you must configure your User Settings like your User and password

![oel-5]({{ site.url }}/assets/images/oel-5.png)

After the installation is done, click Reboot

![oel-6]({{ site.url }}/assets/images/oel-6.png)

Accept the License Agreement

![oel-7]({{ site.url }}/assets/images/oel-7.png)

If you want to register on the ULN (Oracle Unbreakable Linux Network) go ahead. I skipped at this time.

![oel-8]({{ site.url }}/assets/images/oel-8.png)

Login screen. Click on your username and after that fill with your password.

![oel-10]({{ site.url }}/assets/images/oel-10.png)

Welcome Screen, select your language

![oel-11]({{ site.url }}/assets/images/oel-11.png)

Done. Click on Start using Oracle Linux Server

![oel-12]({{ site.url }}/assets/images/oel-12.png)

Cool, now we have our OEL 7 installed. But let's add the Virtual Box Additions.They consist of device drivers and system applications that optimize the guest operating system for better performance and usability.

![oel-13]({{ site.url }}/assets/images/oel-13.png)

The Guest Additions offer the following features:

Mouse pointer integration

Shared folders

Better video support

Seamless windows

Generic host/guest communication channels

Time synchronization

Shared clipboard

and so on...

For a complete list of all features and detailed explanation about them go to https://www.virtualbox.org/manual/ch04.html

On Virtual Box go to **Devices** and then **Guest Additions CD Image, **the pop-up window below will appear

![oel-14]({{ site.url }}/assets/images/oel-14.png)

Wait for the installation to finish and you will have VirtualBox Guest Additions installed and ready to use.

![oel-15]({{ site.url }}/assets/images/oel-15.png)

That's it. Pretty easy hun?  On the part. 2 we will install the Weblogic Server.

See ya

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

