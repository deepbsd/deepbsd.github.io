---
layout: post
title: Debian Testing
date: 2019-11-20 16:05:08-05:00
categories: Linux Debian
---

## Running Debian Testing as a Daily Driver

I am told this is not a great idea.  However, I'm already running several rolling release 
distros, such as Tumbleweed, Manjaro, and Arch.  My thinking is that Debian Testing branch
is no more unstable than these distros.  Besides, I've been at this a while.  I've seen a
lot of update-induced problems and have fixed most of them.  Almost all of them in fact.
So since Testing is not even as full of land mines as Debian Unstable, I thought I would
try it out, and it's been maybe three months?  So far so good.

# What About Stable Releases?

Not a problem.  When an Testing release gets moved into the Stable branch, Unstable gets
moved into Testing.  You can read about how the release system works in the Debian Faq.  

Basically, you've got the Stable branch.  It is absolutely stable, but if you're a desktop
user who wants to use very recent software, this branch will leave you feeling left
behind when it comes to the latest software release versions.  For this reason, some
people follow the Testing branch, which provides more recent versions.  However, prior to
a new Debian release, the Testing branch is "frozen", meaning that little to no changes
are admitted into the Testing branch of Debian.  During this period, developers are
pounding the snot out of the Testing branch to ensure that it is as absolutely stable as
it can possibly be.  Only after this phase does the Testing branch get moved into Stable
in preparation for a new release.  

# Why The Risk?

It's purely about running more recent software.  There are many people who do *not* need
the latest software, and these people often choose to run the Stable branch.  They
couldn't care less about running the latest software, and frankly, they couldn't tell the
difference if you showed them, usually.  That's fine.  That's just what you want for
running a rack full of servers.  Those boxes get security updates and that's about it.
Sometimes they will have uptimes measured in years.  Or at least they used to before
Virtual Machines and containers.  But if you're running Linux on a home server and you
just want it to do its job for years, then you probably are running the Stable branch.

However, I want the latest LibreOffice, the latest Nodejs and Python, the latest Cinnamon
desktop, and so on.  I want the latest Nvidia drivers, the latest browsers, and the latest
whizbang goodies.  That's just me.  

# Why Not Run Another Distro Instead?

I do run other distros.  But Debian is one of my old favorites.  I feel I need to stay on
top of that one.  Debian is the launchpad for all of the Ubuntu distros.  And lots of
other Linux distros too.  Staying on top of Debian is essential for keeping your finger on
the upstream pulse of all of those related distros for which Debian is the ancestor.

The main objection folks have against Debian is that it tends to lag behind on software
versions.  But that's if you're running on the Stable branch.  Not so much if you're
running on Testing.  

Another objection can be related to non-free software.  If you want to run non-free
software, you simply enable non-free repos in your `/etc/apt/sources.list` file.  If you
want to run software like Google Chrome and VLC, you can do this.

Another option to the non-free problem is to use Snap packages.  I prefer snap packages
when running a Debian/Ubuntu distro and Flatpaks when using an RPM distro.  If I'm running
an Arch distro, I normally can find everything I need in the AUR.

# Spotify

This is one of those packages that can be kind of confusing, especially if you play files
locally a lot.  Basically, you need legacy versions of ffmpeg decoding software to
translate locally saved files into a version compatible with the latest Spotify version.
Since I play a lot of local files from my Music library, I encounter the `can't play local
files` bug a lot.  It hasn't been a problem with a Snap package on Debian so far.  The
standard Debian package did not include the proprietary codecs I needed to play all my
files.  But the Snap did, right off the bat.  

Normally, on other distros, it takes some tinkering to play local files, because each
distro will probably handle these proprietary codecs differently.  But Debian, being one
of the most conservative distros when it comes to non-free software, was a perfect
candidate for the Spotify Snap package.

# Problems

There have been a few problems.  One fairly large problem was a result of damaging a file
system from repeated overclocking attempts that left the filesystem with lots of errors.
I cannot blame that on Debian or even Linux.  I basically didn't take enough precautions
with my overclocking (such as maintaining a separate rescue partition).

Another problem happened when I was upgrading a module from the Nvidia driver.  It turned
out that one of the kernel modules wouldn't build, and it quietly bombed out and resulted
in a driver module that couldn't be inserted into the current kernel.

This was an easy fix, once I read the errors and googled them.  Fortunately, this time,
that particular error was the result of a change in how the linux kernel manages video
drivers.  After a certain kernel version, a version check must be made to see whether it
is appropriate to build a module dependency or not.  Prior to that kernel version, it was
the default behavior to build that module.  After that version, you would not build the
module with the same dependencies.  This change resulted in placing an if/then statement
around the block of code where this module dependency was built before.  I think it was
four lines of code that needed to be added.  The github issues page I was reading
contained the four lines of code, so I added them to my nvidia module's source tree.
Poof!  The modules built and installed flawlessly after that.  No problems.

A week or two later, this fix was included in a formal update for the Testing branch.  I
would have been good to go in about a week and a half anyway.  Fortunately, I didn't have
to wait that long.

# Who Should Run Testing?

I would say run testing if you need the latest software versions.  But be advised that
you'll get problems.  If you're okay with working through problems, then fine.  

Be sure to keep a backup of your system!!!

That said, I have really just had these two little problems.  Well, the first one resulted
in a reinstall, because I didn't keep backups on this machine!  (It's a machine that I
overclock on a fair amount!)

The nvidia problem was a typical problem that you might get on the Testing branch.  There
could be other ones, and those problems might not get resolved with 10 minutes of
Googling.  I can take longer.  I've been fortunate.  But this is how I treat any rolling
release distribution.  I normally don't get many problems from them, but when they happen,
they are not fun.  If you do not have backups or have alternate machines you can use to
get work done, it ain't fun.  I have lots of alternative machines I can use.  If one
breaks, it's not a problem for me to use another until I get the broken machine fixed.  In
fact, I normally have *at least one* machine that is broken.  

So, the Testing branch is not a problem for me.  I still can curse when it breaks, but I
realize I have said yes to these problems when I run a bleeding edge release.

For absolute stability, I recommend an LTS release of Ubuntu which are based on Debian
Stable.  Also, Linux Mint tends to be based on an LTS release and inherits great stability
from Debian.  And then running Debian Stable itself is about as stable as you can get.

If you really don't mind running software versions that are *not* the lastest and
greatest, you should try out Debian Stable.  If it turns out it's not recent enough, try
running Debian Testing and see what happens!  All the best in your journey!


