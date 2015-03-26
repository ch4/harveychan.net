---
layout: post
title: "Fun With Android Decompilers"
modified: 2015-02-04 21:57:07 -0800
tags: [lyft, android, reverse engineering, lulz]
image:
  feature: 
  credit: 
  creditlink: 
comments: "How to explore your favorite closed-source Android apps"
share: 
---

One of the best ways to improve your own skills is to observe better-skilled people at work. In the software world, this is as simple as starring and subscribing to a repo. I like to take it one step further by taking apart and peering into the insides of things that I use on a daily basis (and are thus super-familiar with).

I decided to look into Uber's Android app. I still consider myself very much a n00b at Android development, and I wanted to figure out how the Uber app was so robust and fault tolerant. Unfortunately, Uber's source code is not open source... how can I dig into the app?

Well, there are a few options. If the app isn't compiled into a native app, then the APK is just a jar file that we can sorta-decompile. This works best with code that hasn't been obfuscated with Proguard or other obfuscation tools. Even if it is obfuscated, it can still be done, it just gets a little more difficult.

Righto, so we convert the APK into a JAR file and take a peek. First, we need to grab the APK off of our phone. We can either pull it through ADB or just use some file manager like "ES File Manager" to copy it from the internal phone memory to SD card and grab it from there. I prefer the latter.

Once we have the APK, the real fun starts. We run it through apktool and it spits out a folder containing everything inside the APK. The code is in smali, which is a simplified intermediate language that I have no experience with and hard to code for (at least for me).

Alright, well another option is to run the APK through the dex2jar utility to convert it into a JAR. Let's do that.

OK, so we have a JAR file now. Let's take a peek at it using JD.

Boom, much easier to read the familiar Java syntax.

Looks like Uber has obfuscated some of their code. Good for them!