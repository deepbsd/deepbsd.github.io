---
layout: post
title: Overclocking On Linux
date: 2019-11-15 09:25:10-05:00
categories: Linux Overclocking
---

## Linux as an Overclocking Platform

I've recently gotten into overclocking some of my computers.  I've always been weary to
do this, because it seemed like a great way to ruin perfectly good hardware and throw
money down the drain.  So, no overclocking for me.  Until now.

I looked around and saw that I simply had too much hardware.  And it has finally begun
to dawn on me that there is quite a bit of headroom built into CPU these days.  No one
can predict the performance potential of a randomly binned CPU.  So there is a sort of
CPU lottery.  Maybe you win, or maybe you don't.  But there is going to be at least some
potential performance your CPU in your computer will have beyond what it's currently
doing if you are willing to push it a little bit.  And, frankly, I got curious.  That's
how these things always start for me.  I get curious.

There is one more aspect to all this.  I made a promise to myself to not buy anymore
computers.  I probably have about 20 or more towers at my house, mostly all running
linux.  I figured if I'm not buying any more new CPUs, I've got to stay busy with what
I've got, and my attention turned to performance.  If I can get some of these boards and
CPUs to wear out or something, then I might buy new stuff???  

# What is Overclocking Anyway?

There's really nothing special about overclocking.  It's simply pushing your CPU a
little harder for greater speed, and that usually requires more voltage.  Since CPUs and
the chips on your motherboard are so small, they are vulnerable to heat, so small
increases in voltage can place your motherboard and CPU at some risk if you don't think
about what you're doing.  After all, you could have paid many hundreds of dollars for
those components, so why would you want to cook them inside of your tower case?

Well depending on your specific CPU and motherboard, you could get a 10-20% performance
bump in your system.  For free, basically.  I've finally had some systems that are 10
plus years old die on me.  Either a drive controller or mobo component dies or
something, but this has been long *after* that system has been a highly useful system
for me.  My point is, why not get more use out of that hardware since you're going to
upgrade it long before it physically dies anyway?  Overclocking is one way to do that.

Specifically, to overclock, you must have an unlocked CPU (one that allows you to change
speeds and voltages) and a motherboard that supports overclocking.  Likewise, you're
going to need a good power supply with at least a Bronze level rating, and also a good
cooling solution, probably an after market cooler, to handle the increased heat.

An example of an overclock is taking an i5-4790K cpu on an ASRock Z97 Extreme6 board (a
little more expensive motherboard that is good at overclocking) and changing the default
multiplier in the BIOS so that the CPU speed goes from 3.5GHz to 4.5GHz.  Core voltage
could need to go up an extra 0.125 volts or so to keep this clock stable.  So instead of
an idle temperature of, say, 30 degrees Centigrade, perhaps you're now running closer to
40 degrees at idle.  You haven't spent a dime, unless you've upgraded some of your
components.  

This boost from 3.5GHz to 4.5GHz is almost a 30% increase in CPU speed.  And it's
costing you perhaps an extra few pennies in your monthly energy bill.  Can you begin to
see why the idea might be attractive to people?

# But is it Practical?

That depends.  If all you do is surf the web and read email, then probably not.  If you
just want to watch YouTube videos on your machine, then overclocking probably won't be
of interest to you.  But, if you use your CPU cycles on things, such as playing
intensive computer games or rendering videos or compling source trees or something, then
overclocking your CPU might be something of interest to you.  

For me, sometimes I write computer programs that require compute power.  For example, if
I'm searching for prime numbers, I can easily bring a system to its knees.  These are
just intensive calculations, and some operations can take a very long time.  In fact,
there's a "Great Search for Mersenne Primes" on the internet, and it requires so much
compute power that there are thousands (or more?) volunteers sharing their computers'
extra CPU cycles in the search.  The software you download is great for stress testing
your system for stability.  If you can run the stress test and keep your system stable
at higher clocks and voltages, searching for prime numbers is a great way to test your
experimental settings.  This software is called [Prime95](https://mersenne.org/download).

First and foremost, it's fun.  Overclocking is like hot rodding your computer.  You may
or may not notice the performance gains you'll realize.

# Is It Safe?

I believe that depends on you.  Are you safe?  Can you experiment safely?  If you can
trust yourself to be careful and pay attention and be patient, then yes, overclocking is
safe.  If you tend to do things like run around with sharp knives or drive too fast or
hit live ammunition with hammers just for fun, then overclocking your computer may not
be for you.  However, if you can do research and learn the meanings of BIOS/UEFI
settings for your motherboard, then you can safely realize these performance gains from
overclocking.  

Basically, you'll *need* the things I mentioned earlier:

1. An unlocked CPU
2. A motherboard that supports overclocking
3. A good power supply (80 plus Bronze or better)
4. A good cooling solution

# Is Water Cooling Necessary?

Water cooling is not necessary but it can be more efficient than air cooling.  Water can
dissipate thermal energy more efficiently than air, or so I hear.  But if you're
comparing a small 120mm water cooler to a huge heat sink with multiple fans moving air
through the heat sink, then the air cooler will be better.  

TDP or "thermal design profile" is a measurement of the maximum heat a CPU or a Cooler
can handle.  It can be a basic indicator for how much cooling capability a cooler has.
If your air cooler can handle 150W TDP and your 120mm AIO can handle 130W TDP, then your
air cooler is a better solution.  But is it so big that it doesn't fit into your box?
Maybe the biggest heat sink that fits into your box has a TDP of 120W.  

This brings up an interesting point:  there are a LOT of great cooling solutions these
days in either water or liquid coolers.  In general, air coolers must sit on top of the
CPU, which limits the size of the heat sink that can be used.  Water coolers can use
tubes to move the hot water through radiators that can be placed anywhere in the
computer.  You can even use multiple radiators if you so desire.  So liquid coolers have
more potential in terms of how much heat they can dissipate in your system.  But all
this depends on your use case.  Do you just want to run a massive overclock and build a
custom loop cooling solution just so you can show off your high clocks to your friends?
You'll probably want to build a custom loop with multiple radiators, and perhaps you can
even overclock your GPU (graphics card) also and include that in your custom loop?

But if all your after is a 10-15% increase in clock speed, there are lots of air coolers
that will keep your system simple and do the cooling job reliably.  There are also
exceptional air coolers with smaller form factors.  And there are AIOs for nearly every
case.  But, size will be a factor in your solution.

# Why Linux?

Well for me, I use Linux.  Linux is as familiar to me as Mac and Windows are to many
people.  But most people who post on overclocking forums seem to be using Windows.  I'm
not aware of anyone who overclocks on Mac, unless we're talking about Hackintoshes.  And
I'm not sure Apple hardware even has a BIOS that you can change settings on.  So that
would prevent overclocking on Apple hardware I think.  But since most people who
overclock do it on Windows, you just need the Linux equivalents of those software
choices for your Linux machine:

1. Prime95
2. CPU-Z for linux
3. HWMonitor for Linux

Slight problem.  CPU-Z and HWMonitor (available for Windows at cpuid.com) are not
available for Linux.  However, there are alternatives for these options on Linux.  It's
not worth it for me to run Windows just so I can run these pieces of software.

Prime95 is available as a CLI program on Linux.  I can monitor fan speeds, temperatures,
clock cycles and load percentages also with CLI programs or scripts.  If you're willing
to do that, then you can get about the same information on Linux as you can on Windows.
You can google "CPU-Z for Linux" or "HWMonitor for Linux" and find lots of alternatives.

If you're running Ubuntu you may have a few graphical options available that haven't
been packaged to other distros.

# First Steps

It's going to start with your particular hardware.  Are you using hardware that is
capable of overclocking?  If not, you're done.

Is the payoff worth the risk in your case?  If you're already a tinkerer and have
hardware you can afford to experiment with, then great.  If you don't want to risk your
hardware, then stop now.

If you're good to go, start with Google.  I googled "Overclocking on Linux" and came up with LOTS of very
interesting links worth reading.  Lots of opinions out there.  

Watch YouTubes about overclocking on Windows too.  Overclocking happens really more at
the BIOS level, so the OS is really more of a window to whatever is happening at that
lower level of the machine.  You can learn a lot from Windows TechTubers, such as
JayzTwoCents, Pauls Hardware, Bitwit, LinusTechTips, and many, many others.  There are
tons of people out there doing this, so you are joining a huge group of people who have
been overclocking for a long time.

# Conclusion

If you're the type of person who likes building computers or building things with
software, you might also be the type of person who enjoys hot rodding their computer.

There's some risk.  But you could also drop a $500 CPU on the hardwood floor while
you're building a computer.  Or you could accidentally spill your milkshake on your
motherboard.  If you have been willing to handle those risks, then overclocking might
not be much more of a risk for you.

If you've ever run benchmarks on your system to see "how did I do?" then you might be a
candidate for overclocking.  Overclocking your computer is a great way to get higher
scores on various benchmarks.  It's also a great way to measure your performance gains
from overclocking.  There are lots of benchmarks out there, and Google is your friend
here.

Linux has tended to be a production type of platform, especially for servers and getting
work done in the background.  But if you've been using Linux as a desktop solution
instead of Windows or Mac, then why change to Windows just for overclocking?  

Finally, I have not mentioned specific software solutions for CPU-Z and HWMontor.
That's because your choices would probably not be my choices.  Desktop Linux is full of
different environments and window managers and toolkits and technology stacks.  There
isn't one solution that fits everybody.  If you're already using Linux then you probably
already know this.  CPU-X may or may not work as a substitute for CPU-Z on Windows.  You
may well find that writing your own script that monitors `/proc/cpuinfo` works better
than anything else.  Sometimes Conky or GKrellM is enough for me to watch while I
overclock.  Your mileage may vary!

One thing I can tell you, I have been having lots of fun overclocking on Linux.






