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

## The Basic Syntax

It's worth reading the man page for all the switches for Whiptail.  But the switches you'll use
a lot are `--title`, `--infobox`, `--msgbox`, `--yesno`, `--radiolist`, `--inputbox`, `--textbox`,
`--passwordbox`, `--menu`, `--checklist`, and `--gauge`.  Followed by the dimensions of the
box itself in lines and columns.  Example:  
```
name=$(whiptail --title "Sample input" --inputbox "What is your name?" 8 60 3&>1 1>&2 2&>3)

```
Some of the switches need to redirect STDIN and STDOUT, so we need to redirect it back so that
everything works. Here we capture user input into a variable that we can use later.  You'll have 
to read up more on that redirection elsewhere, because I'm going to focus on the `--gauge` switch.

## The Problem with Progress Gauges

As I mentioned, you need to solve the problem of displaying a stream of numbers between 1 and 100
that meaningfully show the progress a UNIX process is making.  The `--gauge` switch has no built-in
way of doing that.  That means that whatever process you're measuring, you need to find a way of
providing `--gauge` a way of doing that.  

In most tutorials for whiptail I see something like the following:

```
{
    for ((i=0; i<=100; i+=1)); do
        sleep 0.1
        echo $i
    done
} | whiptail --backtitle "PROGRESS GAUGE" --title "Calculating Result" --gauge "Please wait for calculation" 8 50 0
```

This will work.  It will display a progress bar while some process has been executed, but there will
probably  be no correlation between the processes progress and the gauge.  What are some other
possibilities?


