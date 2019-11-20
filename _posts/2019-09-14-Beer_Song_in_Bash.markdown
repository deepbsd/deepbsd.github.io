---
layout: post
title: Beer Song in Bash
date: 2019-09-14 22:34:41-04:00
categories: bash
---

## Beer Song in Bash

This was a fun little project, just to try and stay fluent in Bash.  I've been working enough in 
Javascript that I tend to get forgetful in other languages.  Fortunately, Exercism comes to the rescue.
It's not that I'm a great whiz in Bash, but I feel it's a language I want to try and stay conversant in.

# Basic Problem

You're supposed to programatically generate all 100 versus of the beer song and pass a suite of tests where
your script is asked to generate the song at a verse number and continue to another verse number.  You're
supposed to be able to generate the song from start to finish, including the parts that change depending on
singular or plural values, such as "bottle" vs "bottles" and "no more bottles of beer on the wall" for the
last bottle, followed by "Go to the store and buy some more, " and so forth.

So, if your script is called with `beer_song.sh 99 0` then the entire song should be reproduced verbatim.
if your script is called with `beer_song.sh 99` then just the first verse should be reproduced.  But you must
also be able to produce verse 3 if called with the number 3 or verses 0 - 3 if called as `beer_song.sh 3 0`
for example.  The first parameter will always be greater than the second, and you must throw an error if that
is not the case.

# Other Solutions

Well the best part about exercism is being able to look at other people's solutions.  There were a few that
were longer than mine.  But a lot of the solutions were shorter.  But not many of those shorter solutions
were easier to follow than mine.  But they were easier for me to follow, because I had grown accustomed to
thinking about the problem as I had.  So I don't know whether my solution was any better or not.  But I did
put in some comments, so hopefully you can follow my thinking:


# My Solution:

```
 1	#!/usr/bin/env bash
 2	
 3	input=("$@")    # snarf the arguments
 4	
 5	error(){
 6	    echo "1 or 2 arguments expected" && exit 1
 7	}
 8	
 9	error1(){
10	    echo "Start must be greater than End" && exit 1
11	}
12	
13	# throw an error if get too few or too many arguments
14	[[ ${#input[@]} -gt 0 && ${#input[@]} -lt 3 ]] || error
15	# check that verses are in right order
16	[[ ${#input[@]} -gt 1 && $1 -lt $2 ]] && error1
17	
18	say_verse(){
19	
20	    count1=$1
21	    count2=$((count1-1))
22	    singular="bottle"
23	    plural="bottles"
24	    verse2="Take one down and pass it around,"
25	    verse3="Go to the store and buy some more,"
26		verse4="Take it down and pass it around,"
27	 
28	   if [[ $count1 -gt 2 ]]; then
29	        bottles1=${plural}
30	        bottles2=${plural}
31	    fi
32	
33	    if [[ $count1 -eq 2 ]]; then
34	        bottles1=${plural}
35	        bottles2=${singular}
36	    fi
37	 
38	    if [[ $count1 -eq 1 ]]; then
39	        count2="no more"
40			verse2=${verse4}
41	        bottles1=${singular}
42	        bottles2=${plural}
43	    fi
44	
45	    if [[ $count1 -eq 0 ]]; then
46	        count1="no more"
47	        count2=99
48	        bottles1=${plural}
49	        bottles2=${plural}
50	        verse2=${verse3}
51	    fi
52	
53	    verse="${count1} ${bottles1} of beer on the wall, ${count1} ${bottles1} of beer. \n${verse2} ${count2} ${bottles2} of beer on the wall.\n"
54	
55	    printf "${verse^}"
56	}
57	
58	# If the range is a single verse
59	[[ ${#input[@]} -eq 1 ]] && say_verse $input && exit 0;
60	
61	# If the range is more than a single verse
62	while [[ $input -ge $2 ]]; do
63	    say_verse $input
64	    echo
65	    input=$((input-1))
66	done
67	
68	exit 0
```

Basically, I generate the same verse over and over again, but I change several keywords based on the number
of the verse being recited.  I suspect there are much more efficient ways of doing this.  But this was what I
came up with.

By the way, after reading all this code, is anyone feeling thirsty?  First one's on me!


