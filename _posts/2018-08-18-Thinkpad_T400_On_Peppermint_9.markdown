---
layout: post
title: Thinkpad T400 On Peppermint 9
date: 2018-08-18 21:04:44-04:00
categories: Linux Thinkpad RetroPC
---

## My New $25 Thinkpad T400

So earlier this week, my Thinkpad adventures brought me into the
64-bit world when I upgrade my old T60 to an Intel T7600
processor.  That was a fun upgrade.  I'm running LXLE 16.04
Legacy on that machine.  And I love it.

But this machine is a 64-bit machine out of the box.  The T61 was its
predecessor, and that came with a T8100 in its fastest iteration I
think. I'm not sure.  But I think at this point Intel wanted to start
working on using less power in their laptop CPUs, and so their CPUs
didn't get much faster for a while. The T61 was one of these sacrifices
in the speed department.  In a way, the T400 was too, since its CPU was
not much faster than the T60s.  But, there were still quite a few other
changes

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/deepbsd/44072935332/in/dateposted-public/" title="Thinkpad T400 with Peppermint 9"><img src="https://farm2.staticflickr.com/1839/44072935332_2a39a6ee7e_k.jpg" width="1536" height="2048" alt="Thinkpad T400 with Peppermint 9"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

For example this was the first Thinkpad with a widescreen format.  At this point, the 4:3 aspect ratio became a thing of the past.   Also, this machine had an extensive internal roll cage.  I guess people were trying to put Lenovo to the durability to the test.  When you start disassembling this machine, you can see what I mean.

This machine was the first machine that could take 8 Gigs of RAM.  And recognize and address all of it.  The DIMMs didn't come in 8 Gig sticks when this machine came out, but they can be added now.

It's hard for me to say whether this machine is a really fancy T60 or a not-so-impressive T410.  I'll go ahead and call it the former.  It's just that the improvements are incremental here, and they're not so obvious.  Technology doesn't grow exponentially each year.  This year was a year for incremental improvements.  I can't see them that much, except for what I've mentioned.  I'm sure there are lots more improvements that I'm overlooking.  I think Lenovo was trying to be careful and not destroy a very successful product line by changing it very much.  At this point, I think they are flying solo.  No IBM involvement. 

I've heard people criticize the keyboard on this machine.  It's essentially just like the one on my T60.  Perhaps it was another one of those things they did *not* want to change too soon.  And indeed, Lenovo would go on to change the keyboard later on for the worse.  At least in the minds of many fans of the product line, including Yours Truly.  But the next iteration of the product, the T410, I *loved* the change on the keyboard!  They made the `Delete` and the `Escape` keys larger, and they made a few other welcome changes.  But this *perfect* keyboard only lasted for two more product cycles before they introduced the Gawd Awful chiclet keyboard with the T430.  Of course, that's just my opinion. 

However, for me, they keyboard and the display are the essential features of a laptop product.  IBM created the IBM Selectric typewriter.  They created the Keytronics 5150 Keyboard, later named the Model M.  So, they *knew* something about keyboards.  The keyboard was one of the best features of the Thinkpad series.  I believe Lenovo got it perfect on the T410 and the T420.  The T420 was my favorite iteration of Thinkpad.  Its keyboard was the inspiration for the T25 keyboard, the 25th anniversary Thinkpad.  

# Peppermint 9

I have not installed Peppermint on bare metal on one of my machines before.  This was the first time.  I am not unimpressed.  It looks pretty.  I don't notice any lagginess anywhere.  The design and software choices seem reasonable, if eclectic.  And there is a lot of mix and matching.  Take a look at this neofetch grab below:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/deepbsd/43215401785/in/dateposted-public/" title="neoFetch"><img src="https://farm2.staticflickr.com/1816/43215401785_b9e9620c0e_b.jpg" width="709" height="529" alt="neoFetch"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

It uses the Whisker menu system from XFCE.  There are quite a few tools from that desktop.  So they are lightweight and fast.

The file browser is Nemo, from the Cinnamon desktop.  It uses a `blurlock` type lockscreen from i3wm.  There are quite a few Gnome tools.  

And the underlying distribution is Ubuntu 18.04.  So the underlying system will be familiar.  For example, when I pulled down my blog (which you're reading now, thank you) I didn't have to google much to know how to install the `build-essential` toolset for Ubuntu.  (Ruby gems will need it to be installed and run Jekyll.)  

Peppermint makes a pretty big deal out of using Web Apps with ICE to make them Desktop apps.  I'm assuming they are simply using the Electron toolset from Github.  I haven't explored that much.  I guess it's fine.  It strikes me as weird, though, that you would prefer cloud-based Microsoft tools to onboard open source tools, like the Libre Office suite.  Oh well, maybe they're just trying to appeal to a more newbie-ish audience and assume that people won't have used tools outside of Microsoft?  Just guessing.

# Why I Chose Peppermint Here

First, Peppermint has a good reputation for reliability.  And it runs great on older hardware, which a T400 definitely is.  There's also a well-detailed, well-designed user experience installed out of the box.  At least I think so.  The developers certainly have chosen from a broad spectrum of possible choices to get what they want.  I think those choices are at least as reasonable as Cinnamon and Mate, and the choices are also lightweight for ease of running on legacy hardware.  That's not always easy, and appearance was not sacrificed in that choice.

Second, speed on legacy hardware.  This follows from what I've said already.  

Third, it looks spiffy!  And I can find my way around.  These days, there's a fair amount of cross-polination between Mate, Cinnamon, XFWM, and LXDE I think.  They tend to resemble each other.  And a good idea is a good idea, no matter where it is applied.  Desktop environments are one of those common places where good ideas tend to reappear time and again.

My one complaint so far is that the two-fingered scrolling does not seem to work on my touchpad yet.  I'm still researching on why this might be.  Is it possible that this Synaptics TouchPad product was a bit peculiar and the driver was not upgraded as it was for other Thinkpads?  I don't know.  Is it a Peppermint problem?  I doubt it.  It could just as easily be a problem with my particular installation.  Edge scrolling works, at least, and with the touchpad not working exactly right, I get a chance to use the TrackPoint a little bit more.  Small blessings.

All in all, this is a terrific little laptop.  It's got enough compute power to make me happy and do my work.  It doesn't have the dreaded chiclet keyboard yet, at least.  And the screen lets me stream Brit detective shows like I love to do.  The 802.11n wifi is fast enough to let me do that.  And the Peppermint distro lets me do it quickly and also look good doing it.


