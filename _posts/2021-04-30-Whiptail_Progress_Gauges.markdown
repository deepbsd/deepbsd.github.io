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

First, we'll have to launch the process in the background which means spawning a subshell.  Otherwise, we
couldn't measure the process in the script.  So, remember that!  We need to launch the process and 
capture its PID, then watch for the process to disappear from the PID table.  How on Earth do we make that 
happen?

Well, I would recommend passing the name of the function to execute in the background as a parameter to
the `processgauge` function.  So that would mean something like this:

## The Calculator, The Caller and the Gauge


```
calculate(){                                                    ## The Calculator! 'How many angels on a pidhead?'
    echo `Highly technical, time-consuming process here...`
    sleep 600  # sleep for 10 minutes
}

showprogress(){                                        ## The Gauge:  Produce the number stream
    start=$1; end=$2; shortest=$3; longest=$4

    for n in $(seq $start $end); do
        echo $n
        pause=$(shuf -i ${shortest:=1}-${longest:=3} -n 1)  # random wait between 1 and 3 seconds
        sleep $pause
    done
}

processgauge(){                                         ## The Caller:  Start the gauge and watch the PID
    process_to_measure=$1
    message=$2
    backmessage=$3
    eval $process_to_measure &
    thepid=$!
    num=25
    while true; do
        showprogress 1 $num 1 3
        sleep 2
        while $(ps aux | grep -v 'grep' | grep "$thepid" &>/dev/null); do
            if [[ $num -gt 97 ]] ; then num=$(( num-1 )); fi
            showprogress $num $((num+1))
            num=$((num+1))
        done
        showprogress 99 100 3 3
    done  | whiptail --backtitle "$backmessage" --title "Progress Gauge" --gauge "$message" 6 70 0
}

```

This idea relies on capturing the PID of the process to measure.  Then producing numbers up until
the process drops out of the PID table.  We get a guaranteed number stream up to 25, but you can 
set `num` to whatever you want.  You can also make the sleep period longer by offering larger numbers
for the start and end values.  So one advantage of this approach is that it is flexible.  

This type of approach works for short processes and long processes.  You can set longer sleep times in
process gauge (The Caller) for a longer process or shorter sleep times.  You can make consistent
sleep times if you like.  Unfortunately, `shuf` will not accept decimal arguments.  They must be
integers, even though `sleep` will accept decimal arguments.  You could probably find another way
of managing that problem if you like.  For now, this works for me.  Perhaps in the future I'll 
generate shorter sleep times than one second.

So, from a menu to run `calculate`, you could call 
```
processgauge calculate "Calculating Maximum Beer Intake" "Calculating Max Beers"
```
You'll have to experiment with different calculations to see how you like the progress bar with 
different scenarios.  On shorter processes, the progress bar may jump from 25 to 100 percent
really quickly.  On longer processes, the bar may go back and forth between 97 and 98 percent
for a long time.  I chose this vacilation back and forth because at least you know the process hasn't
gotten hung up.  At least it's still running.  You could put something else in `calculate` that
outputs to a logfile and then `tail -f` that logfile to show any errors encountered or other issues.
For example:
```
calculate(){
    logfile="./logfile"
    length=600
    [[ -f $logfile ]] && rm $logfile
    echo "=== START ===" &>$logfile
    for ((i=0; i<=$length; i+=1)); do
        echo "$i:" &>>$logfile
        date +"%D::%N" &>>$logfile
    done
    echo "=== END ===" &>>$logfile
}

```

Now for longer processes in the background you can watch a logfile to see how it's doing.

## Conclusion

This is only one beginning.  I'm sure there are lots more approaches to creating a progress gauge
with Whiptail.  But this approach got me going for today.  I'm back in business with Whiptail!
