---
layout: post
title: Bodhi Linux 5.0.0 On T400
date: 2018-09-03 00:15:35-04:00
categories: linux legacy hardware
---

## Trying Out Bodhi 5.0.0 on *New* T400

Of course, this is the Thinkpad I bought off of Ebay for a few dollars
last week.  It was manufactured in 2008 or 2009, so there's not much *new*
about it, except to me.  I've been thinking about Bodhi Linux for years,
but I've never had occasion to install it until now.  I've tried the live
version several times to see if it would run on older hardware (it does),
but it wasn't until today that I thought I'd install it on another disk
for this laptop.  (I still have a 250G SSD that cames right out when I
swap in this SSD.  Both SSDs boot just fine.)

The install was pretty straightforward. I had to hunt a minute to find the
install program.  And then I needed to configure the network manager,
which wasn't immediately obvious.  But I eventually figured that out and
got the system installed just fine.  When I did, my system basically
looked like this (after I installed GKRellM and added some virtual
desktops):

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/deepbsd/43530817345/in/dateposted-public/" title="shot-2018-09-03_00-21-24"><img src="https://farm2.staticflickr.com/1851/43530817345_eff0d66280_b.jpg" width="1024" height="640" alt="shot-2018-09-03_00-21-24"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

# First Impressions

Since this system uses a variation of the old Enlightenment Window Manager
from the 90s, which I have never run in any form for more than a day or three, I
was both curious and confused.

I still don't know how to use this WM, but I do remember how cool it was
back in the day.  I think it's probably much cooler now than it ever was.
And it's probably also a whole lot better.  I'm talking about the very
early days of Linux.  Predominant WMs had names like FVWM and TWM.  There
were some other ones, all very new, but Enlightenment seemed to have been
designed by designers and artists.  It just had an artistic feel that
didn't seem to come from engineers.  It was beautiful.  Combine it with
nice wallpaper, and you had yourself an amazing desktop.  Unfortunately,
with great artistic expression comes the possibility for unstability, and
E, as it was known, could suffer from that from time to time.  I wound up
not using it longer than a week or so.  

But this is a whole new project.  Moksha grew out of the rubble of the old
project, I guess, but it's source tree probably has little if anything in
common with the original.  This is a very modern looking and
stable-running desktop.  I have no signs of instability.  Seems to run
like a top.

As far as me being confused, this is not your dad's desktop.  Or maybe it
is and that's the problem.  I cannot find things in a single click like I
can on a number of other desktops.  This desktop is different.  Perhaps
it's not *that* different, but I'm needing more time to get comfortable.
For example, the first thing I do when I open a new distro is find the
Terminal.  It took me some time to find it in the menus.  And then it took
me some time to configure it how I like it, which I still haven't fully
accomplished.  Normally these tasks are pretty straightforward.  But not
tonight.  The terminal is called *Terminology*, which I have not used
before.  It appears to be very lightweight, but it's different. And I
cannot tell if it's buggy or it's just me.

For example, in Terminology when I select the transparency level of the
background with a slider that's supposed to go by percentages, nothing
changes after I move the slider and apply.  Sometimes it won't let me
close the settings, as though there's something about the settings that
I've done wrong, except that I cannot see that I've done anything wrong.
Nothing is flashing red or doing anything except appearing to be stuck.
And the slider seems to switch transparency all the way on or all the way
off.  At times like this, when it's a program I am not already familiar
with, I usually just use a terminal that I know already and forget trying
to figure out whether it's me or the terminal who has the problem.  To
solve the problem, all I need to do is use a different terminal.

But I'd like to give Terminology a chance.  But it's being stubborn,
apparently.

# Terminals in Minimal Distros

There seems to be a meme in Linux distros.  The terminal is cool again.
Actually, it was always cool, but younger people are rediscovering the
terminal just like it was 1973.  It's a status symbol to have a cool status
line and PS1 prompt.  This meme seems to have inspired a lot of re-creating
of terminal emulators.  Terminology appears to be one of these new
re-creations.  

It used to be just Xterm or Rxvt.  But then people wanted more functionality,
so they created more features and forks for these old work horses.  Then you
had such powerful hardware in personal computers, people started building
luxury terminal emulators that were the SUV's of terminal emulators, like
Konsole and Gnome Terminal.  These just had every single comfort and amenity
you could ever want, because if you used a terminal at all, why not travel in
comfort and style?  The hardware was no limitation to a terminal emulator,
normally being very lightweight relative to the rest of the desktop.

And now, the meme seems to be swinging the other direction, where we seem to
want lightweight terminal emulators again.  Or we want the same functionality
as the luxo terminals, but with half of the footprint.  I think that's what
*Terminology* is trying to achieve.  There seem to be a lot of these today:
URxvt, Terminator, several forks of XTerm and RXVT.  More than I can count.
There are even two projects that share the same "Terminator" name, one
written in Python and the other written in Java.  Some of the terminal
emulators resemble the drop down terminals you could access while playing
Quake or Doom.  

My point is, the terminal is cool again, but now you have more choices just
to find a terminal that you'll be comfortable with.  The default terminal in
your distro might be an old faithful powerhouse like Gnome Terminal or
Konsole, or it could be one of the slick minimal terminals that you won't
even recognize. It's the latter for me on Bodhi Linux. 

# Conclusion

It's too soon to conclude anything!  I'm just trying to get comfortable with
this desktop.  But it's a rather attractive process.  Everything looks nice,
except those little things I cannot seem to figure out how to do.  (Like get
my Thinkpad Trackpad to work with 2-fingered scrolling.... The TrackPoint
works great though!) 

Moksha looks like there's been *a lot* of thought put into it.  And it has a
fascinating heritage that I remember from the early days of Linux.  In short,
it's a treat to be using Bodhi Linux and the Moksha desktop.







