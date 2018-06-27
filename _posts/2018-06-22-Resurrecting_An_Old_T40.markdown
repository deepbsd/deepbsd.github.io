---
layout: post
title: Resurrecting An Old T40
date: 2018-06-22 23:11:55-04:00
categories: pc vintage_computing
---

## It Lives!

I recently found my wife's old work laptop, a vintage IBM Thinkpad T40.  This would have been
from about 2004 or so.  It was the bee's knees at the time.  It was a very popular business
notebook computer.  This particular example came with a 1.5Ghz Pentium M mobile CPU with a Radeon
Mobile 7500 video adapter (soldered to the logic board) with about 16-32MB of video RAM.  The
hard disk was a 30G spinning HD with an IDE connector.  There was a built-in 56k modem, an
802.11a/b wifi adapter (WEP was all we had then), 100BT RJ45 connector,  a couple of PCMCIA
slots, a PS/2 connector, an RJ11 connector for the dialout.  I think there were two USB
connectors. (I believe this was even before USB2.) The XGA display was capable of 1024X768
pixels.  The OS was a 32-bit version of Windows XP.  By today's standards, this was humble
hardware, but it was a slick machine in its day.

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
paste from the CPU and apply a dab of new paste, which I happen to have had lying around.  I put
in the new fan, and the next thing ya know, I'm looking at a Windows XP boot up screen.

Looking at my old desktop was like traveling back in time!

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
hoping it can run a copy of Linux, perhaps.  If so, that's a game changer.  The HD that arrived
today is 120GB, and the wifi card will do up to 802.11g.  So it should be able to talk to my
router using WPA2/AES I hope.  I can plug in an 802.11ac USB wifi adapter.  That actually works.
But, since USB was actually slower than this wifi protocol, 802.11ac is actually overkill.

The RAM, at 2GB, should be enough to run some kind of 32-bit linux distro.  I'm pretty sure
Slackware will work if nothing else.  The RAM is really the go/no go piece of it.  I can use a
very simple window manager that won't tax the video memory, I hope.  FVWM is still out there, and
it ran on graphics chipsets even more modest than this one.  I'm sure I can find something that
will work in that tiny video RAM space.

# Humble Hardware

You know, we're pretty spoiled today by all of our powerful hardware.  But if you think about it,
this is the first time in history that we have personal computing devices whose power dwarfs our
needs in using them.  They're so powerful that we have no idea what to do with all that power,
and we take it for granted.  Or we spend it doing things like playing games or making home
movies.  Before in history, people solved their problems with pen and paper.  Computers were
reserved for the elite and only the erudite who could write programs actually used their
computers.  Really, we're just now starting to create uses for our personal computers.  But we're
still in our infancy with them and are only starting to use them up to their potential.

In fact, I would say computer programming is the New Literacy.  If you don't know how to program,
it's similar to not being able to read in the 18th or 19th century.  We take it for granted now
that people can read, write and do simple math in at least one language.  I believe it will soon
be expected of a productive citizen to be able to write some simple programs in at least one
computer language.  A person might easily learn to use the Linux command line and write scripts
on this old laptop.  None of that requires a graphical interface!  In fact, this old beast might
be just the ticket.

This laptop is substantially more powerful than the computational power used in calculating the
moon missions.  Our cell phones probably have thousands of times more computational power than
were applied to those trajectory and thrust calculations (I don't even know what all the
calculations were).  So forgive me if I'm not so quick to throw this old T40 on top of the
recycling pile.  I wrote my first BASIC programs on a C-64, my first Pascal programs on an Apple
II, and this beats the pants off those old things.  If this can run a BSD or Linux shell, I can
be in hog heaven.

I'll let you know what happens in the future when I get some more RAM in there.  This old war
horse isn't done for yet.  I think there could be quite a bit of life for this thing in the right
hands.

# Update: Now Running AntiX Linux!

Talk about a resurrection!  I'm now running a _modern_ OS on this old beast!  There are kernel
drivers that can control the antique wifi card, and I'm actually connecting with my router! I'm
connecting at 802.11b speeds, but hey!  I'm connecting at least!  

My new RAM sticks have not arrived for this machine yet.  When they do and I upgrade my RAM, I
should be operating with 2GB of RAM.  But until then, it's working fine!

AntiX is based on Debian Stretch. It's very stable. And I just ran `sudo apt update -y && sudo
apt upgrade` and the command just completed.  You can see this below:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/deepbsd/43042029011/in/dateposted-public/" title="Running AntiX in 256MB of RAM!"><img src="https://farm2.staticflickr.com/1803/43042029011_512ff72c5a_k.jpg" width="1536" height="2048" alt="Running AntiX in 256MB of RAM!"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

Now, this machine didn't win any speed contests completing this command.  In fact, I'm pretty
sure the download part timed out at least once because the speed was so slow.  But, it finally
completed.  It's a miracle that this thing is not on some junk heap anyway.  Any machine this old
that is still running deserves a round of applause.  

So thanks to the folks at AntiX!

