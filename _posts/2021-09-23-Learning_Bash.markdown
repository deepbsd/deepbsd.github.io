---
layout: post
title: Learning Bash
date: 2021-09-23 14:05:27-04:00
categories: linux, bash
---

# How Learning Bash Helps you Learn Linux

When you set out to "Learn Linux" you're actually embarking on a long journey of UNIX
mastery.  You're joining a group of geeks whose ancestry goes back to the 1960's, and
perhaps even before, if you consider that UNIX didn't grow out of nothing.  Learning
the Bourne Again SHell will teach you long-standing principles that have served
programmers, admins, and geeks well from when 64k was a lot of memory up until now,
when 64k is hardly any memory.

By the way, "UNIX" is a copyrighted product, but for many of us, "Unix" is a way of life. So 
I frequently use "Unix" to mean "Unix-like operating system" such as Linux.

## The Terminal (Working In Your Head, Not the Display)

In this modern day and age, most people are used to graphical interfaces or GUIs.
The terminal feels like a foreign planet to most computer users nowadays.  But
graphical layers depend on many other programs and devices working correctly.  If any
of those go wrong, only a console or terminal can be available.  Even very simple
problems can cause a graphical layer to go away.  If you depend on only the graphical
layer, you will experience more downtime and won't be able to fix many
not-so-difficult problems.

The early computers didn't have the horsepower to show graphical layers.  The first
computers didn't even have keyboards or monitors, let alone mice.  Computer programs
used to be stored on perforated paper.  Even large floppy disks were an improvement.
And people got lots of work done in those days by doing mental work in their heads
instead of on the screen.

To make sense of the terminal, you have to understand how computers are built and how
they work.  You won't be seeing pictures of a hard disk or power supply or keyboard.
You have to understand the basic hardware and ideas that make things work.  So this
article assumes you have that.  If you don't know what a network connection or memory
card or disk drive is, you probably are not yet ready for Linux or Bash.  (Even the
term "card" and "disk" is starting to sound rather old.)

## Keep Pieces Small, But Small Pieces Can Form Big Pieces

One of the first principles of Unix is that programs are designed to do small, very
specific things, but that these small programs can be joined together to do large,
sophisticated jobs using Unix plumbing.

UNIX plumbing is a way of talking about redirecting input and output on the terminal.
The notion of data flowing in a direction from one thing to another thing is not new.
But in the terminal we constantly thing of STD\_IN and STD\_OUT and something else
called STD\_ERR.  This is simply data flowing in, data flowing out, and then
something going wrong with the flow of data.  

Mind you, these small programs we're talking about need data to work on.  Let's
create a simple command at the terminal and print the word "Linux" to the display:
`echo 'Linux'` at the terminal will cause the STD\_OUT to be "Linux".  

To see an example of STD\_IN you could take the STD\_OUT of this command and "pipe"
it (UNIX plumbing term) so it becomes the STD\_IN of another term:
`echo 'Linux' | tr a-z A-Z`

The end result of this is 'LINUX' at the prompt.  `echo` produces and STD\_OUT of
'Linux'.  Because of the pipe symbol '|', this output now becomes the input to
another program called _tr_.  This is a terrific little program which I encourage you
to read about.  It simply "translates" or "modifies" some textual input to
some kind of textual output.  It can do different things to characters in a string.
In this case, we're replacing all lowercase characters with uppercase characters.
The STD\_OUT of one program has become the STD\_IN of another program using Unix
plumbing.  This is a very, very useful concept that happens a lot in Linux and Unix.

You can stack up the commands in a sequence:
`echo "Linux" | tr a-z A-Z | sed 's/LINU/UNI/'`
`sed` is a terrific and powerful program that edits streams of text. Here, `tr` translates
the text to uppercase and `sed` substitutes 'LINU' with 'UNI' to output the word
'UNIX' from the original 'Linux'.

We have taken STD\_OUT from one program and piped into STD\_IN of another program,
and then done the same thing again with *that* output so it becomes STD\_IN for yet
another program (sed) to produce yet another example of STD\_OUT: 'UNIX'. 

There are many, many more examples of plumbing with Linux with more operators.  The
pipe symbol is just one.  The point is, we're using very small things to accomplish
large tasks by gluing the small things together.  This idea is fundamental to Bash
and Unix/Linux.

## Reusing Small and Useful Tools

The plumbing examples above show off another very important principle:  reusing
common tools.  

Imagine you had a screwdriver that had an unlimited number of bits for it.  You could
use the same screwdriver on slot head screws as well as phillips head screws as well
as Torx head screw as well as anything else.  These small Unix/Linux tools are very
much like that.  


