---
layout: post
title: Whiptail Progress Gauges
date: 2021-04-30 11:16:27-04:00
categories: bash
---

# Creating Progress Gauges with Whiptail

Whiptail is a dandy TUI (terminal user interface) toolkit that helps you make bash scripts
for non-technical users.  Or for people who just don't like terminals.  The terminal is
a huge source of information.  Sometimes it's too much information.  When it is, a toolkit
like Whiptail can make your scripts seem more friendly.  In particular, though, progress 
gauges can seem a little problematic, because you must provide the indication of progress
yourself.  The `--gauge` switch doesn't possess any magical qualities that help it to know
how much more a process must operate before it completes.  In fact, it has absolutely no way 
to know the progress of a process toward completion.  You must program that progress 
yourself.  I'm going to talk about that in this article.



