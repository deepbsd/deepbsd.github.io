---
layout: post
title: Udemy Vim Masterclass
date: 2018-05-06 16:59:48-04:00
categories: Vim Linux Unix Terminal
---

# Vim Masterclass with Udemy

I recently complated an online class for Vim power users.  That's what it's
supposed to be, and it succeeds for the most part, but there were two areas I
really wanted and expected to learn about: Windows and Tabs.  This course didn't
cover those, but it did cover buffers rather well.

To me, a master class is for someone who uses the tool in question everyday in
their work, and they are comfortable with intermediate concepts.  They are
trying to transition from an intermediate level of competence to an advanced
level of competence.  It seems to me that this course mostly accomplishes that
goal, with the exception of Tabs and Windows.

# The Instructor

Jason Cannon is the instructor, and he appears to have quite a bit of experience
with both Vim and a Linux/UNIX sysadmin career role.  He's definitely qualified
to teach the course, and he does an excellent job.  He provides exercises of
using the motions and methods we need in all of these areas, including visual
mode.  

By the end of the course, you will definitely have exceeded whatever level of
Vim competence you brought to the course.  If you take the time to master all of
the material in this course, you will definitely be an expert Vim user.  

But you will have to learn to use Windows and Tabs on your own.

# Vim Windows and Tabs

If you stop to think about it, Vim windows and tabs are basically buffers that
are displayed differently.  As buffers, they are accessed through things like
`:bn` or `:bp`.  Windows are access through `Ctl-w j` or `Ctl-w k` for example.
And tabs are accessed through `Ctl-PgUp` or `gt` or `gT` and so forth.  In other
words, if you know how to manage buffers, you *basically* know how to manage
windows and tabs.  

The real power of Vim lies, I believe, in expanding your level of comfort to
encompass as much of Vim's potential as possible.  Vim is such a huge tool that
scarcely anyone ever masters it.  Most people use as much of it as they need to
get their work done, and thereafter they stagnate.  They don't push themselves
to learn more.  In order to get really good with Vim, you have to challenge
yourself to expand beyond your current limits.  You need not just one or two
ways of doing some task, but you need to try a handful of different ways.  Then,
with this added competence, you can create even more combinations that you
couldn't before, because now you have grown more breadth.  With more breadth,
you can grow even more depth.  This model of learning applies specifically to
Vim mastery.

For example, if you are already comfortable using `ex` mode and searching and
replacing text through the _ex_ editor, then try using _visual_ mode instead.  
If you become adept at both methods, eventually you can combine the power and
strength of each tool to create new ways to accomplish daily tasks.

For example, let's say you're used to commenting out a block of text with
something like:

```:10,20s/^/^#/g```

to comment out lines 10-20.  If you learn visual mode, now you can do it with:

```Ctl-v10jI#```

It gives you another option.  And there are actually even more ways to do this,
using, say, macros or alternate keybindings or simply other motion/action
combinations.  The more you know, the more you can do.  The more ways you can do
something, the better you can compare the different ways of doing something.
And the more choices you have, the more refined your choices can be for a
specific task.  

On the other hand, if you only know one way to do it, you always have to make
that one do, whether it's the best way of doing it or not.

Windows and Tabs are simply new ways to operate on buffers.  All the tips and
tricks you've learned in the rest of the course can be applied to Windows and
Tabs.

# Where to learn more about Windows and Tabs.

My first stop is usually the Vim wiki, and here's an article about [Vim
Windows](http://vim.wikia.com/wiki/Switch_between_Vim_window_splits_easily).
Likewise, here's an article about [Tabs in Vim](http://vim.wikia.com/wiki/Using_tab_pages).

As always, Google is your friend when it comes to finding resources for learning
anything as ubiquitous as Vim.  There are YouTube videos and many articles and
resources.  This is no surprise, since Vim is one of the greatest, if not _the_
greatest editors in the history of editors.

# Other Topics Missed

There's always more.  Perhaps in a masterclass 2, we could cover topics like
folding, spell check, plugins, tags, markers, more on setting and using
variables, more formatting options and examples, using vim as a stream editor
(not sure if this is doable, but I'm curious!), `ex-cmd-index` and `:smile`, and
whatever else seems like fun, once you've mastered the material in this course.


