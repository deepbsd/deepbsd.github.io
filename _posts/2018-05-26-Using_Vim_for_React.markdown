---
layout: post
title: Using Vim for React
date: 2018-05-26 15:09:05-04:00
categories: development vim terminal
---

## Using Vim on React Projects

I've switched from Atom and Sublime back to Vim, now, even for larger projects like React.js
projects.  If I was actually getting work done in Editors like Sublime or Atom, or even IDE's
like Eclipse, why on earth would I want to switch to a CLI editor like Vim?

The answer is power and comfort.

The only people who ever ask me this question are people who never understood the power of the
terminal or the CLI.  The old joke among UNIX admins is "Emacs is a terrific operating system,
but I use Vim as my editor."  Obviously, this is what Vim afficiados would say.  And you have to
understand that many of today's geeks have never gotten acquainted with a terminal interface.
They grown up with a graphical environment, so they think that's all there must be.

I wonder if people who grew up before there were CRTs thought the same about hardware switches?
Perhaps they couldn't trust these new fangled terminals and their klunky keyboards?

# Using Vim on Small Projects

A small project could be something as simple as a single config file.  Something like an
`/etc/hosts` file even.  Or even a TODO list.  But I was thinking of a small application, really.
Perhaps a handfull of files.  And I asked myself

> What's the difference between using vim on a small project with a handful of files versus
> using vim on a larger project, with perhaps hundreds of files?

> I think the difference is your facility with buffers, tabs, windows, and folds and perhaps with
> marks.

When a person starts using vim, the first thing they do is learn how to get around.  Then they
start cutting, pasting, searching/replacing--all the things you learn to do with a simple editor
on a single file.  With a graphical editor, you use your mouse heavily for selecting, scrolling,
even cutting and pasting.  

Using a mouse to cut and paste is quite universal.  Using a mouse is also a waste of time.  It
takes your hands off the keyboard and forces you to change gears in your brain as well as in your
hands.  Terminal editors let you keep your hands on the keyboard and keep the gear-changing to a
minimum.  You don't loose momentum by switching over to the mouse.  You can keep from getting
distracted, at least by your workflow.

# Using Vim on larger projects.

So after having used Vim on React for a few weeks now, here's what I can tell you.  

1. I've learned to use windows and tabs.

2. I've learned to use plugins like NERDTree, Surround, Fugitive, syntastic, auto-pairs,
   supertab, and others.  Or at least I'm learning how to use them.

3. I've learned to get really comfortable with the onboard help system.  I have to use it on all
   these new plugins too! I'm not sure one ever outgrows the need for this system.

4. I don't turn on `set mouse=a` at all. I keep my reliance on the keyboard.

5. I keep looking for and finding new sources of Vim wisdom.  There are so many of these.

As a developer, I need to see various pieces of code side by side that are not in the same
buffer.  At least, I find that useful.  For example, if I'm writing a method to dispatch an
action, I need to see both the React component and the action I'm updating, and perhaps also the
reducer method, if one is applicable.  Tabs or window panes is an easy way to see those.  You can
see this in the picture in this article.

<a data-flickr-embed="true" href="https://www.flickr.com/photos/deepbsd/41467875545/in/dateposted-public/" title="vim_screenshot"><img src="https://farm2.staticflickr.com/1725/41467875545_ac73bd535c_k.jpg" width="2048" height="1152" alt="vim_screenshot"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>

As you can see, NERDTree is on the left, and there's some Fugitive output in the status bar, and
I guess you'll just have to trust me with the other goodies.

You can see that `i3wm` is my window manager, and this is on Linux Mint.  I run about 10 or 15
distros currently on my various machines, but Mint is one of the most reliable and consistent
distros.

These plugins really expand how I think about Vim.  It's not hard to think of it as an IDE at
this point.  There are lots of people who use Vim on projects of all sizes.  But a lot of how one
uses an editor depends upon how he/she thinks about the project.

# Encapsulating a project

This means breaking a project down into pieces that are easy to maintain and debug or refactor.
Just as it is on a larger project, project managers need to encapsulate a project into
maintainable parts that they can task people with being responsible for.

Likewise, our success also depends upon how we break our workflow down into maintainable pieces.
In reality, you can only work on one file at a time.  However, we often focus upon one idea at a
time, or one task at a time, or one user trying to get what he/she wants from the app we're
working on.  So as a developer, we need to not only edit the one file at a time we must edit, we
need to access the several files at a time we need for making the feature work that we're working
on.  This might mean looking at a single file or at a handful of files.  

> The editor has to be capable of adjusting to our focus, whether it's focusing on a single line
> of code or upon a single feature that spans several files of code.  The editor must be capable
> of reflecting the nimbleness of our thinking right back at us, and doing it while staying out
> of the way. 

In summary, Vim is a godsend.  And it makes its followers feel goodlike in their editing power.
This editor is very small and nimble and can assume the stature of a very simple terminal editor
or of an IDE powerhouse for enormous projects.  Vim is capable following any line of thinking you
need it to do.  All while staying out of your way and just letting you get your work done.

