---
layout: post
title: Active Directory wasn't working if I changed the user from OU (Organizational Unit)
date: 2011-07-12 14:36:16.000000000 -03:00
type: post
published: true
status: publish
categories:
- Dicas e Truques
- quick tips
- UCM
- universal content management
comments: true
---
Hi, I'm back with a quick tip.  
There was a trouble with a customers UCM 10g environment.<br />
The UCM 10g is integrated with Microsoft's Active Directory but one little problem occurs if I change on euser from his OU (Organizational Unit) to another OU (Organizational Unit).<br />  
The UCM losses the reference from AD and the user loses access to UCM. The workaround was to delete the user from UCM everytime I changed them from OU.<br />
This is exactly what UCM does: It caches that information internally. Store the users DN in the database so that UCM don't have to look it up everytime. Going into the User Admin Applet and physically deleting the user, removes him from the Users table in the database and forces a dump of the cache.
If you are using an LDAP provider, there is a solution to change this behavior:  <br />  
Just add to config.cfg the following line:  
<p><strong>RetryDefaultUserProvider=true</strong></p>
This variable will force a new check of the user in every login.<br />
Props to Ken from My Oracle Support for this tip.<br />
See ya...!  <br />
