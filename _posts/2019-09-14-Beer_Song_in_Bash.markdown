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
#!/usr/bin/env bash

input=("$@")    # snarf the arguments

error(){
    echo "1 or 2 arguments expected" && exit 1
}

error1(){
    echo "Start must be greater than End" && exit 1
}

# throw an error if get too few or too many arguments
[[ ${#input[@]} -gt 0 && ${#input[@]} -lt 3 ]] || error
# check that verses are in right order
[[ ${#input[@]} -gt 1 && $1 -lt $2 ]] && error1

say_verse(){

    count1=$1
    count2=$((count1-1))
    singular="bottle"
    plural="bottles"
    verse2="Take one down and pass it around,"
    verse3="Go to the store and buy some more,"
	verse4="Take it down and pass it around,"
 
   if [[ $count1 -gt 2 ]]; then
        bottles1=${plural}
        bottles2=${plural}
    fi

    if [[ $count1 -eq 2 ]]; then
        bottles1=${plural}
        bottles2=${singular}
    fi
 
    if [[ $count1 -eq 1 ]]; then
        count2="no more"
		verse2=${verse4}
        bottles1=${singular}
        bottles2=${plural}
    fi

    if [[ $count1 -eq 0 ]]; then
        count1="no more"
        count2=99
        bottles1=${plural}
        bottles2=${plural}
        verse2=${verse3}
    fi

    verse="${count1} ${bottles1} of beer on the wall, ${count1} ${bottles1} of beer. \n${verse2} ${count2} ${bottles2} of beer on the wall.\n"

    printf "${verse^}"
}

# If the range is a single verse
[[ ${#input[@]} -eq 1 ]] && say_verse $input && exit 0;

# If the range is more than a single verse
while [[ $input -ge $2 ]]; do
    say_verse $input
    echo
    input=$((input-1))
done

exit 0
```

Basically, I generate the same verse over and over again, but I change several keywords based on the number
of the verse being recited.  I suspect there are much more efficient ways of doing this.  But this was what I
came up with.

By the way, after reading all this code, is anyone feeling thirsty?  First one's on me!


