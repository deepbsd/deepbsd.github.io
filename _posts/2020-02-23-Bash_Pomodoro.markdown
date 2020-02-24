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

Here's the script:

```
     1	#!/usr/bin/env bash
     2	
     3	#################################
     4	#  Easy little pomodoro time mgmt
     5	#  program to help you not waste time.
     6	#  This runs in a terminal, so you can use it 
     7	#  with a tiling window manager if desired.
     8	#  Requires 'play' is installed (from sox)
     9	#################################
    10	
    11	##  Initial variables
    12	short_break=5
    13	long_break=20
    14	pomodoro=25
    15	## Forgot that all terminals are not UTF
    16	#goal="⌚⌚⌚⌚⌚⌚⌚⌚"
    17	goal="********"
    18	completed_pomodoros=""
    19	start_sound=./sounds/Ship_Bell-Mike_Koenig-1911209136.wav
    20	end_sound=./sounds/foghorn-daniel_simon.wav
    21	((durationinmins=${pomodoro}*3600/60))
    22	
    23	## Run the i3bar version or regular version?
    24	[[ "$@" =~ 'b' ]] && runinbar=true || unset runinbar
    25	
    26	##  Set the start time in seconds
    27	start_time=$(date +%s)
    28	
    29	## Play start or end sounds for periods
    30	play_sound(){
    31	    ## make sure 'play' is installed...
    32	    command -v play >/dev/null 2>&1 || { echo >&2 "play (from sox app) is required but not installed. aborting..."; exit 1; } 
    33	    file=${1}
    34	    play -q $file 2>/dev/null
    35	}
    36	
    37	## Play the start sound
    38	play_sound $start_sound
    39	
    40	## Computes seconds elapsed from after 1st argument
    41	## Expects argument in seconds
    42	compute(){
    43	   start_secs=${1}
    44	   now_time=$(date +%s)
    45	   elapsed=$( expr $now_time - $start_secs )
    46	   printf "%d " "${elapsed}"
    47	}
    48	
    49	## Converts seconds to hours, minutes, seconds
    50	## Just displays minutes and seconds
    51	convertsecs(){
    52	    ((h=${1}/3600))
    53	    ((m=(${1}%3600)/60))
    54	    ((s=${1}%60))
    55	    #printf "%02d:%02d:%02d" $h $m $s
    56	    printf "%02d:%02d" $m $s
    57	}
    58	
    59	## Computes minutes and seconds remaining from start time
    60	## and now time,  Expects now_seconds then start_time
    61	remainingsecs(){
    62	    ((m=${2}-1-${1}%3600/60))
    63	    ((s=(60-${1}%60)))
    64	    [ $m -eq -1 ] && m=0
    65	    printf "%02d:%02d" $m $s
    66	}
    67	
    68	## For showing a list of asterisks and completed Pomodoros
    69	completed(){
    70	    echo '⌚' 
    71	}
    72	
    73	##  Runs a break, either a short one or long one
    74	##  Expects an argument in minutes
    75	run_break(){
    76	    play_sound $end_sound
    77	    start=$(date +%s)
    78	    now=$(date +%s)
    79	    length=${1}
    80	    elapsed_secs=$(expr $now - $start)
    81	    minutes=$((elapsed_secs/60))
    82	
    83	
    84	
    85	    while [ $minutes -le $length ]; do
    86	        now=$(date +%s)
    87	        pomo=$(compute $start)
    88	        minutes=$((elapsed_secs/60))
    89	
    90	        ## exit and start a new Pomodoro when break is spent
    91	        if (($minutes >= $length)) ; then 
    92	            return 0
    93	        fi
    94	
    95	        elapsed_secs=$(expr $now - $start)
    96	        remaining=$(remainingsecs $elapsed_secs $length)
    97	        elapsed=$(convertsecs $pomo)
    98	        if [ $length -ne $short_break ]; then
    99	            break_type="Long Break"
   100	        else
   101	            break_type="Short Break"
   102	        fi
   103	
   104	        clear
   105	## Hot pink may not work well on light terminal but it does on dark terminal
   106	cat <<EOBreak
   107	
   108	
   109	        $(echo -e "\033[38;5;205m")
   110	        //////////////////////   BREAK TIME  //////////////////////////////
   111	
   112	        Break: ${break_type}    Elapsed: ${elapsed}   Remaining:  ${remaining}
   113	        $(echo -e "\033[m")
   114	
   115	EOBreak
   116	
   117	        sleep 1
   118	    done
   119	}
   120	
   121	show_bar(){
   122	    count=0
   123	    period=${1}
   124	    length=${2}
   125	    start=$(date +%s)
   126	    spinner=('\' '|' '/' '—' '\' '|' '/' '—')
   127	
   128	
   129	    while true; do
   130	        elapsedsecs=$(compute $start)
   131	        [ ${elapsedsecs} -gt $((length*60)) ] && return
   132	        pomo=$(compute $start)
   133	        elapsed=$(convertsecs $pomo)
   134	        remaining=$(remainingsecs $pomo $length)
   135	        clear
   136	        printf "%s > %s %ss left %d/%d done" ${period} ${spinner[$count]} ${remaining} ${#completed_pomodoros} ${#goal} 
   137	        sleep 1
   138	        if [ $count -lt 7 ]; then
   139	            ((count++))
   140	        else
   141	            count=0
   142	        fi
   143	    done
   144	
   145	}
   146	
   147	##  This is the main pomodoro screen
   148	show_pom(){
   149	    period=${1}
   150	    length=${2}
   151	    start=$(date +%s)
   152	
   153	    while true; do
   154	        pomo=$(compute $start)
   155	        elapsedsecs=$(compute $start)
   156	        [ ${elapsedsecs} -gt $((length*60)) ] && return
   157	        elapsed=$(convertsecs $pomo)
   158	        remaining=$(remainingsecs $pomo $length)
   159	
   160	    clear
   161	
   162	cat <<EOF
   163	
   164	
   165	                    Welcome to MyPomodoro!
   166	
   167	        ///////////////  Work Time  ///////////////////////
   168	
   169	        Short break: ${short_break}     Elapsed: ${elapsed}
   170	
   171	        Long break: ${long_break}     Remaining: ${remaining}
   172	
   173	        Goal: ${goal}     Completed: ${completed_pomodoros}
   174	EOF
   175	    sleep 1
   176	    done
   177	}
   178	    
   179	
   180	##  This is the main loop
   181	while true; do
   182	    [ "$runinbar" ] && show_bar "Work" ${pomodoro} || show_pom "Work" ${pomodoro}
   183	
   184	    completed_pomodoros+=$(completed)
   185	    if  [[  $(( ${#completed_pomodoros} % 4 )) == 0 ]] && [[ ${#completed_pomodoros} -ne 0 ]]; then
   186	        [ "$runinbar" ] && play_sound $end_sound && show_bar "Long_Break" ${long_break} || run_break ${long_break}
   187	    else
   188	        [ "$runinbar" ] && play_sound $end_sound && show_bar "Short_Break" ${short_break} || run_break ${short_break}
   189	    fi
   190	    start_time=$(date +%s)
   191	    play_sound $start_sound
   192	done

```

## Thoughts on Script

I'm not sure this script will stand, but it seems to work for now.  The idea was to
pass a '-b' argument if it should run in the bar, and pass no arguments if it should
just run in the terminal.  So far, it just runs in the terminal, either in a single
line or on multiple lines.
