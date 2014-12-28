---
layout: post
title:  "Mini talk about java IDEs - Eclipse vs IntelliJ"
date:   2014-11-20 20:12
categories: eclipse netbeans intellij which ide java development programming
---

I've recently started using IntelliJ Idea instead of Eclipse to do java programming.
I'm not really picky about IDEs I'm using, but I think I might try to write a little something for my followers :)

To start off, I'm not a professional, so you don't need to take it seriously. If you disagree, open a ticket on github ;)

So my first Java IDE was NetBeans. I've used NetBeans, because it worked and I liked things that "just work".
I have to say NetBeans might've changed a lot since I've last used it(it was version 6 at that time). 
What I liked about NetBeans was the WYSIWYG GUI editor which eclipse or intellij didn't have at that time.
I had no issues with NetBeans, but I've seen some guys use Eclipse, so I thought I might give it a shot.
I've been using Eclipse for most of the time(like 5 years), so I'd say I know it pretty well. 
Eclipse was fine. It was even better, because it allowed me to include project in a project, which I couldn't find in NetBeans and I kinda liked its environment more than NB.
Now my projects are getting more and more complex, get dependencies which are both my own and from others. 
It starts to get really chaotic with dependencies, because I need to download JARs, documentation, sources and map them to JARs for convenient use.
Recently, I've found out that a build system could manage this for you and you could get more control over the whole building, which was done by Eclipse.
So I said ok cool, let's try this! And I've tried maven(many bukkit plugin devs used maven so I just went with them..). 
I wasn't able to get a simple POM to work on Eclipse... I'm using Apache ANT + Ivy along with Eclipse to deal with deps.
Ivy Eclipse integration is I'd say really quick-and-dirty solution. Refreshing sources gives me non-existent errors and it's easy to see that they're not very well connected.

Today, I've checked out mclauncherapi from github using IntelliJ, added POM to manage deps and here I am changing the program. 
It's really much easier with IntelliJ, because the integration plugins are better. Eclipse is an awesome IDE, but I think IntelliJ has advantages that Eclipse can't offer - mainly stability.
What I'm missing in IntelliJ is having more projects opened at once. Since I usually need that, it's really uncomfortable having to switch windows.
Also, people say Eclipse Luna has dark theme. It's however not truly dark, because it doesn't integrate with system theme very well... IntelliJ's theme integrates better.

So to conclude this post and get back to programming, I recommend Eclipse to beginners and once you start doing something in team or using build system, switch to IntelliJ. 
It's not as complex as it looks and it handles most of these tasks better than eclipse. 