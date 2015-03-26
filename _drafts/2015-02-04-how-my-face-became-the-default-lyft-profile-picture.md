---
layout: post
title: "How My Face Became the Default Lyft Profile Picture"
modified: 2015-02-04 21:57:07 -0800
tags: [lyft, android, reverse engineering, lulz]
image:
  feature: 
  credit: 
  creditlink: 
comments: "For about 7 hours, my face was the default profile picture on Lyft's mobile app"
share:
---

When you're decompiling closed-source apps, you're bound to find some *ahem* interesting code. Open source encourages better practices because you've got that many more eyes looking at your work, so you want to do the best work that you can. On the other hand, closed source promotes hacky hacks and spaghetti code because it's only seem by a handful of people and... hackers.

And I mean the bad kind of hackers. The ones who will decompile your code and look for exploits. But that's a point for another blog post.

Last time, I took a look at the Uber app. Well, it's only fair to do the same for their competitor, Lyft. Let's take a peek...

Interesting... There's even less obfuscation! I don't think they even run it through Proguard!

And what the holy heck is this... a placeholder string that points to "urlisnull.io"? Let's see what's there.

Looks like it's not registered. So that explains why I get an infinite spinny loading page on the app when I tap on my own profile picture.

Let's see what we can do with this. I'm going to buy the domain and point it to an S3 bucket. Turn on static site hosting on the bucket, and point the domain at a picture in my bucket...

Absolute madness! If you don't have a profile picture, the Lyft app now happily loads my picture.

Now, I wonder what would happen if I point the URL to some ridiculously large file? Would the app crash? Maybe it would burn through the drivers' cell data plan and run up thousands of dollars in overages. I didn't try this because it could have gotten the engineer responsible for this fired.

I turned on stats for the S3 bucket and at this point, I left for a concert. When I got back home at about midnight, I had a few thousand hits on the bucket and the exploit had been patched. It looks like they simply return an empty string for the profile picture now, instead of a null value. Which leaves me wondering why they didn't just use an empty string as the placeholder in the first place!

A few people have reported seeing my picture in parts of the driver app as well, so they obviously still have some other instances of the placeholder string elsewhere in the app.

