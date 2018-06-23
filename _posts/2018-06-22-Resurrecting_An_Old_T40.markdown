---
layout: post
title: Resurrecting An Old T40
date: 2018-06-22 23:11:55-04:00
categories: pc vintage_computing
---

## It Lives!

I recently found my wife's old work laptop, a vintage IBM Thinkpad T40.  This would have been
from about 2004 or so.  It was the bee's knees at the time.  It was a very popular business
notebook computer.  This particular example came with a Pentium M mobile CPU with a Radeon Mobile
7500 video adapter (soldered to the logic board) with about 16-32MB of video RAM.  The hard disk
was a 30G HD with an IDE connector.  There was a built-in modem, 100BT RJ45 connector,  a couple
of PCMCIA slots, a PS/2 connector, an RJ11 connector for the dialout.  The XGA display was
capable of 1024X768 pixels.  The OS was a 32-bit Windows XP.  By today's standards, this was a
humble machine, but it was a slick machine in its day.

# The First Power-On

Unfortunately, this old thing would not post.  I kept getting "Fan Error" on start up, and then
the machine would shut down.  Apparently, the fan did not work, and to keep the CPU from melting
itself through the bottom of the notebook, the BIOS would shutoff the computer and power down.

I thought that spelled the end for this old work horse.  It had seen its day.  It had fought the
good fight, and now it was time for the laptop graveyard.  Or was it?  

# Replacing the Fan

Out of curiosity, I did some googling.  Was it possible to replace the fan?  These old IBMs were
quite popular; was it possible there are still suppliers for parts like the heat-sink and fan
assembly?  Turns out there was and still are sources for all kinds of parts for these things.
The parts are often gently used or recycled.  Perhaps they're old inventory?  Who knows.  But I
found a fan for about $9 or so and ordered it.  It arrived the same week.  

I googled for how to replace the fan, and it turned out to be rather simple.  These old notebooks
were rather easy to work on.  They come right apart and are not nearly as complicated as I
thought they might be.  After watching one or two YouTube videos, I was an expert.

As you can see, the new fan assembly went right in without a problem.

<a data-flickr-embed="true" href="https://www.flickr.com/photos/deepbsd/42961135021/in/dateposted-public/" title="T40 New Fan"><img src="https://farm2.staticflickr.com/1824/42961135021_ab236c0985_k.jpg" width="2048" height="1536" alt="T40 New Fan"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

That shiny copper-colored thing is the new fan/heatsink.  I needed to remove the old thermal
paste from the CPU and apply a dab of new paste, which I happen to have lying around.  I put in
the new fan, and the next thing ya know, I'm looking at a Windows XP boot up screen.

Now, this computer is very slow.  I mainly wanted to see whether it could boot and run anything
at all.  It passed that test!

<a data-flickr-embed="true" href="https://www.flickr.com/photos/deepbsd/42059421735/in/dateposted-public/" title="The T40 Lives!"><img src="https://farm2.staticflickr.com/1810/42059421735_f73c1669f3_k.jpg" width="2048" height="1536" alt="The T40 Lives!"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

You cannot see just how slow this computer is from the pictures, but at least it boots.  I just
installed Service Pack 3 for 32-bit XP.  It's *still* slow!  

# New RAM, Wifi, and HD

Just out of curiosity, I wanted to see how much I could upgrade this old thing.  I'm curious if
there's anything it could still do today.  So for under $60 I ordered the above parts.  These
will help.  Some of the parts have already arrived (the wifi card and the hard disk), but I'm
still waiting on the RAM.  

Is this machine worth $60?  Probably not.  Will it actually be able to do anything?  Well, I'm
hoping it can run a copy of Linux, perhaps.  The HD that arrived today is 120GB, and the wifi
card will do up to 802.11g.  So it should be able to talk to my router using WPA2/AES I hope.

The RAM, at 2GB, should be enough to run some kind of 32-bit linux distro.  I'm pretty sure
Slackware will work if nothing else.  The RAM is really the go/no go piece of it.  I can use a
very simple window manager that won't tax the video memory, I hope.  FVWM is still out there, and
it ran on graphics chipsets even more modest than this one.

