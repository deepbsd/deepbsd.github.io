---
layout: post
title: AntiX Best Lightweight Distro!
date: 2018-06-27 15:27:37-04:00
categories: linux vintagepc
---

## The Proof is in the Pudding

I say this because there are lots of distros that claim to be lightweight distros.  They claim to
have non-PAE and 32-bit distros, but they still require more RAM than I had in order to install
the distro.  But AntiX got straight to work on the live distro, and the system was booted up and
operational from the DVD in a very reasonable time.

I recently wrote a post about resurrecting an old IBM T-40.  That's the machine I installed AntiX
on (pronounced _antics_ as in _The Three Stooges and their antics_).  

# 256MB RAM

True to their word, the installer completed without complaint with only 256MB of RAM.  This
distro did not complain one little bit.  I cannot tell you how refreshing that was.  Even under
XP, I was getting nagged right and left about needing newer versions of things, and those things,
I knew, required many more resources than this little laptop had to offer.  No such complaints
from AntiX.  

And, there were pleasant surprises along the way:

1. The ancient wifi card now started working with an WPK2/AES key.  Or at least something close
   to it so I could have a wifi connection to my home router.

2. The desktop renders at a humble but honest 1024x768 resolution.  There are no artifacts or
   flickers or any residual graphical problems.  The display just works and updates as you would
   expect.

3. All of the old window managers that were around when I started using Linux in the mid-90's
   still work great on this hardware spec.  Right now, I'm using a the Openbox window manager,
   and it's every bit as good and fast as I remember it.  My hardware doesn't _feel_ old running
   this environment.

4. I'm getting to know the Debian distribution again, through AntiX.  Debian has perhaps the
   largest software universe in all of Linux land.  Being one of the oldest distros and certainly
   one of the most forked, Debian is one of the most copied and reused distributions available
   anywhere.  So there's a good chance that if I've ever run it at any time in the past, or if I
   care to try to run it today, that software is probably available as a package for AntiX
   through Debian (I think AntiX can use normal Debian packages).

5. There's no overheating.  Anywhere on this system.  I thought this modern Linux distro would
   cause the machine to struggle.  But no, I cannot hear the fan spin up, and as I put my hand
   underneath the laptop, nothing feels hot or even very warm.  The new fan is doing its job, and
   the temparatures are very reasonable.  

# Wifi Whitelist

I will have to say there is one negative, and it doesn't have anything to do with AntiX.  The
wifi card is on a whitelist, so it cannot really be upgraded.  It can be replaced by another card
on the whitelist, but those are all the same speed.  The only way to use a card that is not on
the whitelist is to modify the bios or modify the bios of the wifi card to identify itself as
something other than what it is.  So, unless I want to reflash my bios, I'm stuck with this card,
for practical intents and purposes.  

I learned all this the hard way.  I ordered an 802.11b/g card from Amazon.  It arrived promptly.
It would have worked well with my router.  But I got the dreaded `ERROR 802: Wifi card is not
approved for use on this product` or words to that effect.  I was told to disconnect the wifi
card and try again.  There are work arounds, but they all require me to modify my bios,
apparently.  

This error was very stubborn.  The machine simply would not boot normally.  I tried to disable
the wifi card in the BIOS settings, but I could not.  Nor could I change the identification
number or any such thing.  All I could do was replace the original wifi card.

Which started working great under AntiX, by the way.  It wouldn't work at all under XP.  Runs
like a, err, slow top under AntiX.  Even AntiX cannot make an 802.11b adapter connect at faster
speeds than it was designed for.  But the wifi card still works better than I've ever seen it run
on this laptop.

<a data-flickr-embed="true" href="https://www.flickr.com/photos/deepbsd/42999363462/in/dateposted-public/" title="AntiX Linux running on an ancient T40."><img src="https://farm1.staticflickr.com/917/42999363462_68951f9df2_k.jpg" width="2048" height="1536" alt="AntiX Linux running on an ancient T40."></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

As you can see, the wifi card is working fine while performing a routine update.  The speeds are
humble, but as long as the connection is tolerant of such a slow connection, my machine gets
updated very reliably.  

Normally I'm a GKrellM guy and not so much a Conky guy.  However, Conky is starting to grow on
me.  Since I've transitioned to i3wm on many of my other machines, GKrellM has a problem being
seen unless the outter window gaps are quite large or unless the GKrellM width is very small.
Conky does very well in tiling window managers.

All in all, I am very impressed by AntiX.  As I mentioned I tried several other distros on this
laptop, and the live editions would start to run and fail or something bad would happen.  Of all
the distros I tried, AntiX was the only one that just ran immediately with no drama.  

Apparently, this little distro is exactly what it says it is.  And for me, it's a fountain of
youth for my older hardware!
