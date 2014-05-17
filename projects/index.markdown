---
layout: post
date: 2014-05-17 10:18:18
title: Other Projects
---

Besides games, I work on number of other projects that don't fit games category, so I just write them down here, so I don't have to categorize them. C'mon, I haven't got so many projects :D

## WifiMapper

WifiMapper's aim is to help people to create their own wifi maps. I'm currently using this on my OpenPandora along with external GPS and rendering to GeoJSON. Then, I import GeoJSON to QGIS with OpenLayers Street Layer and voila, I see the wifis. 

I use this a lot when I commute from/to school, so I can track WIFI networks around me.

## passity

I started using password manager when someone hacked my 8-characters-long twitter password. I got really angry and setup long passwords for each web service, where I'm registered. I've been using KeePassX for some time, but KeePassX was too slow to start and it consumed all of my screen, so I didn't like it so much.
That's why I switched to pass, the standard unix password manager. It's really awesome so far, I was able to import all my passwords from KeePassX using a python script and all the passwords were encrypted using a GPG key. However, something was missing. How do I lock the database? Now anyone who logs into system can see my passwords. That's not what I want!
So I started to create passity. The name passity comes from pass + zenity. Passity can show a little menu of what you can do with pass and using similar small dialogues, you can lock the database, which will make pass command useless and then unlock it back. It works based on copying files, tar-gzipping them and of course encrypting using some OpenSSL magic.
In the future, I'd like to add scripts to manage your passwords like insert, edit, remove & list and also copy.