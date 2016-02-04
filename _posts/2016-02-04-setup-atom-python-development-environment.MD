---
layout: post
title:  "How to setup ATOM as your Python development environment"
date:   2015-12-16 15:00:00 -0200
categories: python
comments: true
published: true
---

Hi,  
<br />
<br />
PyCharm is an awesome IDE for Python Development and I use it a lot. But sometimes it gets heavier that I want to kill myself. Then I've found ATOM. ATOM is a coding editor created by the GitHub team to be simple, powerful and highly customizable.  
<br />
There are some features that I really like in **ATOM** like:

* Built-in package manager
* Multiple panes
* File system browser  

If you want to give it a try and use **ATOM** as your Python development environment, follow me in this post and I'll show you how I configure my ATOM settings to make easier for us Python developers to have a very simple and powerful development environment.
<br />  
I'm using a Macbook so I'm assuming you are using one too. Hit "Command + ," and this will bring the Settings tab. If you use another OS change the "Command" key to "Ctrl" key.
<br />  
In *Editor Settings*, check the **"Back Up Before Saving"** box. This will avoid corrupt files in case of failure during file save process.
<br />  
Go below and check the **"Show Indent Guide"** and **"Show Invisibles"** boxes. This options will help you navigate through your code showing the indentation. This is very helpful specially when you are working with Web Development and HTML files.
<br />  
On the left Menu, click on *Install* option. We are going to install the following packages:

* linter-flake8
* linter-pep8
* autocomplete-python
* django-templates

The installation is pretty straightforward, you search for the package and after you've found you click on *Install*. It's simple as that.
<br />  
After that your **ATOM** will be ready to rock some Python code. But we are not finished yet. If you try to open a Python project using **ATOM** you will notice that things are not working well.
<br />  
![Atom_Error]({{ site.url }}/assets/images/atom-error.png)
<br />  
This happens because ATOM uses **pep8**, **flake8** and **jedi** packages in its plugins. That's why we need to install those Python packages.
<br />  
You already created your Python Virtual Environment following the best practices right? If so we are going to install the following Python packages:

* pep8
* flake8
* jedi

Activate your Virtualenv:

```
source venv/bin/activate
```

In my case *venv* is the name of my Virtualenv environment.
<br />  
More on Virtualenv's here: http://docs.python-guide.org/en/latest/dev/virtualenvs/
<br />  
Now proceed with the installation of the Python packages:
<br />  
```
pip install pep8 flake 8 jedi
```
<br />  
And we're done. Very simple and you will have your **ATOM** editor ready to use as your Python Development environment.  
<br />  
![Atom_Error]({{ site.url }}/assets/images/atom-python-dev-env-working.png)
<br />  
See ya !!!
