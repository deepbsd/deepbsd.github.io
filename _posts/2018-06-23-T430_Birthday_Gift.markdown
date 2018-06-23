---
layout: post
title: T430 Birthday Gift
date: 2018-06-23 01:02:31-04:00
categories: pc laptops thinkpad
---

## It's My Birthday!

Okay, I really didn't need another computer.  I think I must have about 20 or so right now.  But
I enjoy building them, and I cannot seem to let the old ones die.  I take it as a challenge to
get them running again!

Behold my new T430!

<a data-flickr-embed="true" href="https://www.flickr.com/photos/deepbsd/28092808547/in/dateposted-public/" title="New (?) T430"><img src="https://farm1.staticflickr.com/892/28092808547_3e45632633_k.jpg" width="2048" height="1536" alt="New (?) T430"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

My T420 is doing so well as a desktop computer (it's plugged into a KVM and outputting to a
lovely 1080p 27in monitor!), that I didn't have the heart to disconnect it.  And I have a W530
that also disconnects quite easily that I could use for on-the-go computing, but I wanted to
experiment with Manjaro's i3 distro some more.  And even though I'm running i3 as my window
manager on the W530, the underlying distro is Linux Mint.  And it's behaved flawlessly.  I didn't
want to mess with that distro.  So, new computer time!

But, I didn't want to go overboard.  So I found this used T430 for about $300.  It came with some
el cheapo "refurbished" components.  I replaced those.  I added a 500G SSD and a 16G Crucial RAM
kit.  The RAM timings were rather slow (DDR3), so I didn't overpay for the kit.  The SSD is now a
500G Samsung 850 Pro.  

The unit already came with a dual-core i7-3520M CPU and a 1600x900dpi display.  I'm not sure
which display adapter it is, but I'm pretty sure it's an Nvidia card of some kind.  

# Manjaro i3 To The Rescue

When I first booted up the computer, Cortana started yakking at me and told me to wait so she
could get me "set up".  When it comes to Microsoft, I already know they would like to "set me
up"!  No thank you.  

I stopped Cortana in her tracks and replaced the drive.  Then I booted from a DVD copy of Manjaro
from the i3 community.  It's a lovely distro.  It comes very well-themed out of the box.  Unlike
a normal copy of i3, I didn't need to tweak it very much.  The default keybindings were very
well though-out.  

# The Mission for This Laptop

I mainly expect to use this for programming.  It also works for watching YouTube videos and
browsing websites like Pinterest or Linked-In.  In other words, my typical daily work and/or
play.  I don't think I'll spend much time watching movies on this--I'm spoiled on larger
displays.  But *this* laptop will help me to actually show up at Starbucks or wherever to do my
work away from the house.  Getting me *out of the house* is the primary mission for this laptop.

# Computing Power

As I write this, the Lenovo T480 is the current T-series laptop from Lenovo.  The T-series comes
in an "S" (for slim) version and sometimes a "P" version.  (Not sure what the P stands for.)  The
first number after the letter stands for the size (T4xx means 14-inch, T5xx means 15-inch and so
on).  The P70, which replaced my W series ("W" is for workstation), is a 17-inch laptop.  

Basically, Thinkpads come in a lighter-weight "X" series, a middle-weight "T" series, and a
workstation replacement series called "W" or now "P".  Each of these models can have several
choices for CPU and other loadout options.  The options include a nice display, faster CPU and
larger RAM kit onboard.

> How does this laptop compare with the latest and greatest from Lenovo?  I have no idea.  I actually don't care.  It's fast enough for what I need and use.

I'm sure it's behind on the various benchmarks.  Those benchmarks are all well and fine.  But
they don't particularly matter to me, because I wasn't ever going to use this laptop for video
editing or gaming.  For what I want to use this laptop for, the newest from Lenovo has very
little advantage over this laptop.  That's simply because writing code in vim simply doesn't
require many resources.  I might need a bunch of browser tabs open.  I might need to run some
servers.  I might need a VM or two.  This can do all of that.  I really don't see myself needing
more than one VM at a time.  

For my T430, I got a pretty nice selection of components.  The trick is to get with your laptop
what is harder to replace (CPU, display, video adapter) and to get the cheaper version of what is
easy to replace (CPU, disk drive).  A replacement display and CPU would probably have been half
or more of the cost of the entire laptop.  I already had a 500G SSD left over from a previous
build.  So I only had to pay for the 16G RAM kit.

# More Birthday Fun

Tomorrow I plan on doing 70 kettle bell swings.  I'll take my time doing them all.  I'm thinking
maybe three or more sets.  I'm also getting dinner with my daughter.  I'd also like to see the
new _Incredibles_ movie.  That sounds like fun.

> All in all, I hope my 64th year is as productive and growth-filled as my 63rd year was!

Additionally for my birthday, I bought myself the _Simon and Simon_ TV series on DVD.  I used to
enjoy that old series.  

BTW, I felt inspired, so here's some Node Poetry!  I wrote it while noodling on this new laptop!
I was thinking about putting it on a tee shirt!

```
#!/usr/bin/env node

//personal motto
const mood = (feelingGreat=false) => {
	const makeShift = () => {
      let nowMoment = true
      return mood(nowMoment)
    }
  let behavior = feelingGreat ? "Feeling and Acting Awesome!" : makeShift()
  return behavior
}

var iFeelGood = [true,false]

var myFeeling = iFeelGood[Math.round(Math.random())]

console.log( mood(myFeeling) )
```

