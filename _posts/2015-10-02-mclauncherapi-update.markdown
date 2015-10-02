---
layout: post
title:  "MCLauncherAPI 1 will be on the way!"
date:   2015-10-02 20:30
categories: minecraft api launcher mclauncherapi
---

Hello readers, today I have a special announcement which is related to one of my newer projects - MCLauncherAPI.

As you may know, MCLauncherAPI is today more than 2 years old. 
With codebase getting bigger and bigger, it's becoming more and more difficult to add new features while not breaking the existing projects which rely on MCLauncherAPI.
Also, I was very strongly influenced by Effective Java book I read during summer holidays. 
I realised my projects contain so much antipatterns and I can't even count how many errors this bad code might have caused.

MCLauncherAPI is also included in the set of my projects with bad code. 
To be honest, I didn't think about the software architecture too much while writing the API. 
My only aim was to protect people from future changes in Minecraft Launcher, authentication, version lists etc. 
That was accomplished, many people were able to use the API for their own launcher, but we're now facing another problem: The code that is protecting us from launcher magic isn't protected! :)
I decided that many patterns from the book should be used in an API like this one.

With that decision in mind, I'm aware of the fact, that we can't just grab the existing code and "improve" it.
It'll be much easier to start from scratch and write brand new code with the knowledge we already have.
All programmers know that the easier way is to write new code than to improve the legacy code.

***

So here comes the announcement:
I've decided to rewrite MCLauncherAPI from scratch. There will be interfaces similar to `GlobalAuthenticationSystem` and also `MinecraftLauncherBackend` which will allow you to use the API very easily.
The API will be divided to modules(login, version list, installer, launcher, ...), which will make it easier to maintain it and also exclude some parts of API you don't need.
Also, if you want to become part of the project, now is the best time to join :)
