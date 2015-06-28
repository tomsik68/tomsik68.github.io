---
layout: post
title:  "Java Build Systems Overview"
date:   2015-06-28 21:28
categories: java build system maven ivy ant gradle
---

### Hello!

Hello everyone, I think it's about time for a new post :)
This time, I'd like to start some sort of "blog series" of posts about java build systems. 
I'm going to focus on Java, so C programmers or hardcore vim/make users please don't blame me. I'm just trying to make this post easier to understand :D 
Let's start with a basic question: 

### What is a build system?

Beginner java programmers in most cases don't need care about how their software is compiled. Eclipse, Idea, NetBeans or other IDE take care of this for you.
And it works perfectly fine for primitive programs. However, if you start working in a team where everyone uses different IDE and some people don't, 
you will start to see that you need to customize your environment to compile the project. It might involve setting the correct java version, adding resources to JAR file and different tweaks.
Also, you might start to see patterns in what you do after building your software - like signing JAR with a key, generating SHA256 sums, running test units, uploading to server etc.
Believe or not, most of these tasks can be automated by a build system. 

In my opinion, every programmer will sooner or later discover that they need a build system.

### Why did I start using build system?

For me, the main reason is that I work on multiple projects using multiple computers.
At the moment, I've got 2 laptops and a desktop PC. All of them run Linux. Does this mean I have to setup the project each time I want to switch PCs? I'm already using git to synchronize the code and it works very well. 
However, I can't synchronize project settings, because they use absolute paths to refer to files. Also, one of the laptops is slower, so I'm not using eclipse on it. However, that means I would need to run javac manually. Running javac manually?! How about no?
Many build systems also download specified versions of required libraries for you, which is really nice and saves lots of work.
So I've started to read about java build systems and in this series, I'll try to sum up my experiences with each of them.

You can also choose not to believe me, but consider that my BukkitDev profile has 10 plugins(all use java), I've got 41 github repositories at the moment(wow) and I've migrated my projects 4 or 5 times to different machine
so I know what I'm talking about.

### What can you expect?

In the upcoming week, I'm going to write blog posts about java build systems. One post per build system. 
In each post, I'll mention my beginner experience(the first use of the system), intermediate experience, pros and cons and at the end, I'll sum it all up.
These build systems will be discussed in future posts:

* ANT + IVY
* Maven
* Gradle
