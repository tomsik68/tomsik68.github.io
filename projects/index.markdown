---
layout: post
date: 2015-08-17 20:51:29
title: Other Projects
---

Besides games, I work on number of other projects that don't fit games category, so I just write them down here, so I don't have to categorize them. C'mon, I haven't got so many projects :D

# Development environment

## docker-xampp

Having more than 1 PHP projects is a pain. Especially if you have to copy files from your dev folder to your web server and change PHP versions often because of complicated dependencies.
I've set up a docker container for each of my PHP projects and keep web servers and databases separate from my machine's `/srv/http` or `/var/www`.
If you don't know what docker is, you should really check it out. It's extremely cool tool! It's like a virtual machine, but it's not entirely virtual machine. It's faster and more resource-friendly... http://docker.com/
This project consists of single file used to build docker image which contains XAMPP(apache + PHP + MySQL + phpmyadmin) and openssh server. Real must-have for web developers!

Project page: https://github.com/tomsik68/docker-xampp


# Interpreters

## chip-m8

A few programming sessions with @dudoslav have done some magic :D We were creating our chip8 interpreters while not looking at each other's code. 
Lots of fun and bugs. I've utilized some knowledge from brainfuck.c.

Project page: https://github.com/tomsik68/chip-m8

## brainfuck.c

After reading first chapters of C programming book, I thought I'd test my knowledge with a little project. 
After I found an interesting programming language called Brainfuck, which contains just a few simple instructions, I was inspired to create an interpreter for it.
This is how brainfuck.c was born. During programming this, I tried to utilize some good practices like verbose variable names and extremely verbose comments for nearly every line.
I also came up with convenient human-readable way to put brackets around things in C!

Project page: https://github.com/tomsik68/brainfuck.c

# Kodi / XBMC media center

## sdl-xbmc-remote

I've got an XBMC media center in my room and I'm using wired keyboard to control it atm.
It's very uncomfortable and the wire always gets in the way. So how cool would it be to control your XBMC with your OpenPandora(http://openpandora.org)?
Simple answer: really cool. I've collected my C++ skills and setup sdl-xbmc-remote. 
It's a simple application which reads user input and sends it to XBMC.
"Why GPL3? you said MIT is better!" - Yes, it is, but I've used official XBMC library which is "under GPL2 or higher", so I sticked with GPL3. 

Project page: https://github.com/tomsik68/sdl-xbmc-remote

# Wifi

## WifiMapper

WifiMapper's aim is to help people to create their own wifi maps. I'm currently using this on my OpenPandora along with external GPS and rendering to GeoJSON. Then, I import GeoJSON to QGIS with OpenLayers Street Layer and voila, I see the wifis. 

I use this a lot when I commute from/to school, so I can track WIFI networks around me.

Project page: https://github.com/tomsik68/WifiMapper

# Linux desktop

## passity

I started using password manager when someone hacked my 8-characters-long twitter password. I got really angry and setup long passwords for each web service, where I'm registered. I've been using KeePassX for some time, but KeePassX was too slow to start and it consumed all of my screen, so I didn't like it so much.
That's why I switched to pass, the standard unix password manager. It's really awesome so far, I was able to import all my passwords from KeePassX using a python script and all the passwords were encrypted using a GPG key. However, something was missing. How do I lock the database? Now anyone who logs into system can see my passwords. That's not what I want!
So I started to create passity. The name passity comes from pass + zenity. Passity can show a little menu of what you can do with pass and using similar small dialogues, you can lock the database, which will make pass command useless and then unlock it back. It works based on copying files, tar-gzipping them and of course encrypting using some OpenSSL magic.
In the future, I'd like to add scripts to manage your passwords like insert, edit, remove & list and also copy.

Project page: https://github.com/tomsik68/passity
