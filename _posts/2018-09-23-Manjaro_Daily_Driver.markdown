---
layout: post
title: Manjaro Daily Driver
date: 2018-09-23 15:42:45-04:00
categories: Linux
---
# Manjaro Reliability

For those of you who have been reading my blog, you know I think highly of Manjaro.  Since I've only recently started using
Arch-based distros (like in the last year or two), I haven't known quite what to expect with such a rolling distro.  I've heard
stories of unstability and changes being rolled into the distro before they were ready.  And I hadn't really gotten the details of
those stories.  I had only heard them on forums or in YouTube videos, and I didn't have any first-hand experience myself.  My only
experience using a rolling distro, actually, is with OpenSUSE Tumbleweed.  That hasn't been bad, but there have been problems with
vendor repo changes and there being quite a bit of confusion on my part about what repos to use.  The upgrades seem to want to change
my repos without regard to my choice of vendor.  I don't really appreciate that.

Anyway, as far as Manjaro goes, I've had the the i3 edition installed on several of my laptops that I use a lot.  I haven't had a
hint of instability.  I think the worst thing that happened was that pamac would not resolve a conflict as easliy as I thought it
might, but as soon as I used pacman, it got resolved right away.  So that just tells me that pacman is more mature than pamac.  But
I'm more of a CLI type of guy anyway.  So no surprise.  Perhaps if I were more open to GUI repo tools like pamac, it wouldn't even
have been a problem.  I would have seen how to coax the tool into resolving my problem.  

I suspect that in the Linux world, CLI tools turn out to be more mature than the GUI tools.  After all, the GUI tools are just a
font-end for the same CLI tools anyway, aren't they?  I guess it shouldn't bee too big a surprise.

The bottom line is that it appears that rumors of instability with Manjaro simply haven't materialized in reality.  My experience so
far has been rock solid.  

## Branches and Repos

From what I can see, there are three main branches of Manjaro: STABLE, TESTING, and UNSTABLE. STABLE is for production users. If a
production user is adventurous or wants to contribute bug reports, he/she could switch to the TESTING branch and just resolve to deal
with whatever instability ensues.  The UNSTABLE branch would be for developers who are working with the rough sources that are not
ready for prime time yet.  These changes are unstable even for developers.  So these would be for devs or people who want to live on
the edge.  I would assume this would not be the ragged edge, and that UNSTABLE would be for devs to share with each other.

I think that's how it is on many other distros too, but I had always thought that updates made it into Arch repos earlier than in LTS
type of distros.  That if there are any errors in the package builds, that those become evident when the rebuilt packages are
released into the repos and everyone updates his/her system. But apparently Manjaro's STABLE branch gets more testing than the pure
Arch repos.  I guess that means that the Arch repos are not stable enough for Manjaro's developers.  Or that they want more control
than what you get with the normal Arch repos. 

Perhaps this precaution explains the rock solid experience I've been enjoying with Manjaro!

## Community Editions and Official Releases

The official releases are KDE, GNOME 3, and XFCE-centric releases.  There's also a Manjaro Architect version for designing your own
custom-rolled distribution, which is probably popular with IT departments.

The Community Editions offer a lot more desktop options.  There are specific editions for several tiling window managers, including
Awesome, BSPWM, i3.  There are also editions for other popular desktop environments like Budgie, Deepin, Cinnamon, LXDE, Openbox and
Mate.   I'm sure all the other desktops are available, but these desktops have specific community editions that revolve around them.
So truly, there are a lot of Manjaro supporters and enthusiasts to support this many specific editions of Manjaro.  Clearly, the
communities are very active and strong.

I only have personal experience with the i3 and the Cinnamon editions.  Cinnamon was the first one I installed on a new computer
build perhaps a year or two ago now.  That has been one of my favorite computers to log into.  It's a gorgeous default theme that is
highly polished.  All the coloring and fonts are just a little nicer than the defaults on many other default installs.  I can't even
put my finger on what the specifics are that make me think this.  It's sort of like dining at an exclusive restaurant versus dining
at a nice but budget restaurant.  I'm not a gormand, and much is lost on me, but there're a lot of subtle differences in the details.
I think that's how it is with Manjaro.  Subtle things like fonts, wallpapers, themes, default measurements and small choices have
been worked on more.  More than what?  I couldn't say.  But the choices just seem more polished.  I don't know how else to say it.
This is just my impression, but I don't believe I'm mistaken.

## An Example

So with the default installation of i3wm on another distro, you get some simple colors and a bar that all seem to work.  The only
choice you will need to make is whether you'll use the Super key or the Alt key as your default "i3" button.  And the default
installation is very plain and underwhelming, but it works very well right out of the box.  You just need to give it some love and
learn how to customize it, because it probably will look too plain to use as it is.

This is not the case with the default installation of Manjaro i3 Edition.  i3Gaps is installed by default.  The Super key (windows
key) is the default i3 button, and there are many other choices made right out of the box.  There's a terrific color scheme, some
small gaps are built in if you'd like to look at wallpaper, of which there are many custom possibilities that work great with
nitrogen.  In fact, Compton is installed and used right out of the box.  The default install includes a lovely bar with terrific font
awesome icons and applications.  You really don't *need* to change a thing, unless there's something you just don't care for.  The
default install is polished and refined.  So you could live with these defaults and still have a highly polished desktop, unlike the
the default i3wm install you get on most other distributions.

## Another Example

I'm a big fan of Linux Mint.  So I actually didn't expect as polished an install with the Cinnamon edition of Manjaro as I got with
Linux Mint.  But I was wrong.  Manjaro Cinnamon is highly polished.  Once again, the themes are highly polished and the icons are
unique and even beautiful.  I actually like the default icon theme with Manjaro Cinnamon better than I like default Mint icon theme.
Does Manjaro have more artists on their Cinnamon team? The flat icon theme seems modern and sophisticated. 

Of course, my Mint installations are so old by now that I have not updated them in a good while, and my original choices have been
respected by each of numerous upgrades.  Perhaps if I installed a new verison of Mint from scratch, it would look as fresh and lovely
as a new Manjaro Mint install.  I don't know.  But the nice thing about Manjaro over Mint is that I don't have "upgrades" anymore, so
to speak.  A rolling release gets upgraded in place regularly.  There are no large release cycles per se.  The upgrades are smaller
and are incremental.  

## The Package Manager

Perhaps Mint and Manjaro Cinnamon is a good comparison.  It seems fair.  So I'll compare the package managers: apt vs pacman.  There
are some profound differences.  The largest difference right off the bat is that with Manjaro, you have access to the AUR, or the
Arch User Repository.  Basically, this has user source trees and custom build scripts for about every obscure or specialized piece of
software you can think of.  For example, I deploy web apps to Heroku, and the Heroku-cli tools happily lives inside the AUR.
Likewise Spotify and its custom build script.  There's a custom build script for GKrellM, too, my favorite little PC performance
visualizer.  If you use the Slack desktop workgroups app, there is a custom build script for that, even though it's not officially
supported on the Arch platform--only Fedora and Debian/Ubuntu.  You would think the AUR could add instability to your distro, but I
haven't experience that.  Perhaps my time is coming?  I guess I'll find out in time, but so far, only happiness and productivity.
The tool for the AUR I use is `yaourt`, which I think stands for "Yet AnOther User Repo Tool".  There's support for lots of software
that often doesn't make it into the mainstream repos of large distros.  If you cannot find it in a mainstream repo for Arch or
another distro, you can still probably find it in the AUR.

Pacman is the default package manager.  Yaourt also works on the normal repos too, I think, but I believe Yaourt specializes in the
AUR.  For my daily upgrade checks, I run pacman from the CLI.  It basically does the same thing that `dnf` and `apt` and `zypper` and
`eopkg` do on other distros.  I use it to search for packages and learn about their dependencies and version numbers.  Pacman is
simply what you normally use on Arch-based distros.  There are probably more subtle differences, but I only know that pacman seems to
work for me, just as those other tools I mentioned have worked for me--reliably and with no fanfare.

## Conclusions

Right now, the machine I use the most is running Linux Mint 18.3.  I have not had a problem with this machine or distro, ever.  So
I'm not inclined to make changes right away.  But I think I could change this machine to Manjaro.  I think it would be just as
stable.  But I rather hate to nuke a perfectly good and stable Linux installation for no good reason other than the novelty of trying
something new.  

I have to tell you, I recently ran the upgrade from Mint 18.3 to Mint 19 on another machine, and I was surprised to run into an
error.  The install script did not complete error free.  That was the first time I had ever experienced a hiccup with a Mint major
version upgrade.  The 19 release had been out for perhaps 3-4 weeks when I ran the upgrade.  The machine in question was a laptop
without a lot of custom extras.  When the errors happened, I eventually closed my mouth and got on Google to find what the problem
was.  I eventually solved the problem, or rather, found someone else's solution.  But my conclusion was that even Linux Mint, the
most reliable and stable distro in my personal experience, even *that* distro can have a hiccup during an upgrade.  So, I'm reminded
to keep my backups current, and I'm also reminded that distros like Manjaro are ready and able to replace Stalwarts like Linux Mint
whenever the desire arises.  In fact, last time I looked at Distro Watch, Mint and Manjaro were neck and neck for first and second
place.  I think they swap places on a regular basis.  Manjaro has simply gotten that good!

Also, I must confess that I don't believe in a perfect distro.  If you use Linux long enough, eventually you will have a problem.
That applies to any distro, although some distros are more rock-solid stable than others.  But even Linux Mint is capable of having a
hiccup.  I'm sure Manjaro is capable of that too.  But I tend to regard them as top drawer distros that guarantee stability and
freshness as far as any Linux distro can.



