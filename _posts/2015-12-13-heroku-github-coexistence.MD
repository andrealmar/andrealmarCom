---
layout: post
title:  "Coexistence between GitHub and 'Heroku Git' "
date:   2015-12-16 15:00:00 -0200
categories: software engineering, github, heroku
comments: true
published: true
---

Ok, you've deployed your app to [Heroku](http://www.heroku.com) but there is something missing. You want to show the world your new work done. You want to show your brand new awesome code.  
How to do that? It's very simple actually.  <br />  
First you need to create a new repository in your GitHub account. Click on the green button (picture below) to create a new repository in your GitHub account:  
<br />
![Eventex-1]({{ site.url }}/assets/images/github-heroku-1.png)  
<br />  
Here I named the repository "eventex". After named the repository you can click on the green button (another one) "Create Repository".
<br />  
![Eventex-2]({{ site.url }}/assets/images/github-heroku-2.png)
<br />  
Now you just have to add GitHub as a separate remote repository:  
```
git remote add origin https://github.com/USERNAME/REPO
```    <br />  
In my case it was:  
```
git remote add origin https://github.com/andrealmar/eventex.git
```
<br />  
Now you can push to GitHub using the command below:  
```
git push origin master --force
```  <br />  
For the *first time* you will have to do a forced push (--force). Because now you are assuming that you're pushing what used to be the repository you used *exclusively* for Heroku. But don't worry. You'll still be able to push to Heroku using ```git push heroku master```.
