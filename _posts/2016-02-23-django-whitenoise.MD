---
layout: post
title:  "Serving staticfiles in Django with WhiteNoise"
date:   2016-02-23 12:00:00 -0200
categories: python
comments: true
published: true
---

Hi, in this post I'm going to show you how to use WhiteNoise to serve static files using Django. 
WhiteNoise (http://whitenoise.evans.io/) is a library to radically simplified static file serving for Python web applications. With a couple of lines of config WhiteNoise allows your web app to serve its own static files, making it a self-contained unit that can be deployed anywhere without relying on nginx, Amazon S3 or any other external service. (Especially useful on Heroku, OpenShift and other PaaS providers.)
<br />
#Isn’t serving static files from Python horribly inefficient?  
The short answer to this is that if you care about performance and efficiency then you should be using WhiteNoise behind a CDN like CloudFront. If you’re doing that then, because of the caching headers WhiteNoise sends, the vast majority of static requests will be served directly by the CDN without touching your application, so it really doesn’t make much difference how efficient WhiteNoise is.  
<br />
That said, WhiteNoise is pretty efficient. Because it only has to serve a fixed set of files it does all the work of finding files and determining the correct headers upfront on initialization. Requests can then be served with little more than a dictionary lookup to find the appropriate response. Also, when used with gunicorn (and most other WSGI servers) the actual business of pushing the file down the network interface is handled by the kernel’s very efficient ```sendfile``` syscall, not by Python.
<br />
#Shouldn’t I be pushing my static files to S3 using something like Django-Storages?  
No, you shouldn’t. The main problem with this approach is that Amazon S3 cannot currently selectively serve gzipped content to your users. Gzipping can make dramatic reductions in the bandwidth required for your CSS and JavaScript. But while all browsers in use today can decode gzipped content, your users may be behind crappy corporate proxies or anti-virus scanners which don’t handle gzipped content properly. Amazon S3 forces you to choose whether to serve gzipped content to no-one (wasting bandwidth) or everyone (running the risk of your site breaking for certain users).
<br />  
The correct behaviour is to examine the ```Accept-Encoding``` header of the request to see if gzip is supported, and to return an appropriate ```Vary``` header so that intermediate caches know to do the same thing. This is exactly what WhiteNoise does.
<br />  
The second problem with a push-based approach to handling static files is that it adds complexity and fragility to your deployment process: extra libraries specific to your storage backend, extra configuration and authentication keys, and extra tasks that must be run at specific points in the deployment in order for everything to work. With the CDN-as-caching-proxy approach that WhiteNoise takes there are just two bits of configuration: your application needs the URL of the CDN, and the CDN needs the URL of your application. Everything else is just standard HTTP semantics. This makes your deployments simpler, your life easier, and you happier. Enough talking, let's go to action.
<br />  
Install the WhiteNoise package: 
<br />

```python
pip install whitenoise
```
<br /> 
Open your ```settings.py``` and add the following:
<br />

```python
STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```
<br />
Run ```python manage.py collectstatic``` to put all your static files into STATIC_ROOT. (If you’re running on Heroku then this is done automatically for you.)
<br >  
Also addin your ```settings.py```:
<br />

```python
from whitenoise import WhiteNoise

# Simplified static file serving with WhiteNoise adding cachable files and gzip support
STATICFILES_STORAGE = 'whitenoise.django.GzipManifestStaticFilesStorage'

```
<br />
Open your ```wsgi.py``` and install WhiteNoise into your Django application:
<br />

```python
from whitenoise.django import DjangoWhiteNoise

application = DjangoWhiteNoise(application)

```
<br />
Note in the code above that we are wrapping our existing WSGI application in a WhiteNoise instance with ```DjangoWhiteNoise(applications)``` this is how your application will now serve static assets directly from Gunicorn in production. This will be perfectly adequate for most applications, but top-tier applications may want to explore using a CDN with Django-Storages.
I hope you guys liked it and if you have any questions or suggestions leave a comment below.  
<br />
See ya!


