---
layout: post
title: Bash Pomodoro
date: 2020-02-23 23:08:53-05:00
categories: bash timekeeping
---
# Creating a Pomodoro in Bash

I originally wanted to create a pomodoro timer that could run in i3status or i3blocks.
I haven't quite made it that far, but it does run in bash.  For those of you who
haven't heard about it, see the Wikipedia article on the [Pomodoro
Technique](https://en.wikipedia.org/Pomodoro_Technique).

I chose to create a work period of 25 minutes, with 5 minute short breaks and 20
minute long breaks.  I decided to measure the time using a date object measured in
seconds.  Then I figured I needed three functions: 1) a compute function that takes an
argument of seconds to start from and prints the number of seconds elapsed from that
date object (measured in seconds), 2) a "convert seconds" function that takes a date
object in seconds and returns the formated string of minutes and seconds that can 
be displayed to the user, and 3) a "seconds remaining" function that takes two
arguments: the number of seconds when the period started and the "now" time in
seconds, and that returns a printed string of remaining minutes and seconds in the
period.

Further, I needed a function to run the breaks between work periods.  This function
would start a period for a certain length, and that length would be this functions
only required parameter.  

Once all this was working, I would need some kind of audible bell or something to tell
the user when the Pomodoro period or break was done, and when to take a break or
return to work.  So that was another function.

Because I not only wanted this to run in a shell terminal, I wrote a function that
would display the work periods (pomodoros) and break periods in a single line that
could be displayed on a status bar like i3status or i3blocks for my favorite tiling
window manager, [i3wm](https://i3wm.org).  This required that I actually have two
functions for showing a pomodoro, one that displays inside a terminal and one that
runs inside a bar.  Well, the "bar" function works such that it displays a line of
text that could run inside a status bar, but I haven't gotten it to actually work
inside either i3bar or i3blocks.  It displays inside a terminal on a single line just
fine.  And the other functions works fine inside a terminal window; it takes up about
5 lines of text, separated by line spaces in-between, for a total of ten line spaces.


