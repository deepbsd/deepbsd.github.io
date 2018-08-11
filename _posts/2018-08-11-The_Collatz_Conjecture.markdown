---
layout: post
title: The Collatz Conjecture
date: 2018-08-11 13:46:40-04:00
categories: bash
---

## The Collatz Conjecture

Okay, I have no idea if there was a guy named Collatz, or whether he ever conjectured anything.  However, there's a little math problem also known as the `3x + 1` problem, or the `Collatz Conjecture`.
I found this as I was working through the bash problems at [https://exercism.io](https://exercism.io).  It goes like this:


> # Collatz Conjecture
> 
> The Collatz Conjecture or 3x+1 problem can be summarized as follows:
> 
> Take any positive integer n. If n is even, divide n by 2 to get n / 2. If n is
> odd, multiply n by 3 and add 1 to get 3n + 1. Repeat the process indefinitely.
> The conjecture states that no matter which number you start with, you will
> always reach 1 eventually.
> 
> Given a number n, return the number of steps required to reach 1.
> 
> # Examples
> 
> Starting with n = 12, the steps would be as follows:
> 
> 0. 12
> 1. 6
> 2. 3
> 3. 10
> 4. 5
> 5. 16
> 6. 8
> 7. 4
> 8. 2
> 9. 1
> 
> Resulting in 9 steps. So for input n = 12, the return value would be 9.
> 
> 
> Run the tests with:
> 
> ```bash
> bats collatz_conjecture_test.sh
> ```
> 
> After the first test(s) pass, continue by commenting out or removing the `skip` annotations prepending other tests.
> 
> ## Source
> 
> An unsolved problem in mathematics named after mathematician Lothar Collatz [https://en.wikipedia.org/wiki/3x_%2B_1_problem](https://en.wikipedia.org/wiki/3x_%2B_1_problem)
> 
> 
> # External utilities
> `Bash` is a language to write scripts that works closely with various system utilities,
> like [`sed`](https://www.gnu.org/software/sed/), [`awk`](https://www.gnu.org/software/gawk/), [`date`](https://www.gnu.org/software/coreutils/manual/html_node/date-invocation.html) and even other programming languages, like [`Python`](https://www.python.org/).
> This track does not restrict the usage of these utilities, and as long as your solution is portable
> between systems and does not require installing third party applications, feel free to use them to solve the exercise.
> 
> For an extra challenge, if you would like to have a better understanding of the language,
> try to re-implement the solution in pure `Bash`, without using any external tools.
> 
> # Submitting Incomplete Solutions
> It's possible to submit an incomplete solution so you can see how others have completed the exercise.


This is the README.md lifted from the exercism site on the problem.  It's kind of like one of those little math tricks that a grade school teachers might show to a class in order to rev up some enthusiasm and curiosity
for math.  I'm not sure if it works on the kids, but it worked on me!  

# My Solution

```
   1	#!/usr/bin/env bash
   2	
   3	input=${1}
   4	
   5	error(){
   6	  echo "Error: Only positive numbers are allowed"
   7	  exit 1
   8	}
   9	
  10	validate(){
  11	    [[ ${1} =~ ^[0-9]+$ ]] && [[ ${1} -gt 0 ]] || error
  12	}
  13	
  14	validate ${input} 
  15	
  16	posnum=${input}   # input has now been sanitized
  17	
  18	count=0   # count iterations...
  19	
  20	# must validate input or loop is infinite
  21	while [[ ${posnum} -ne 1 ]]; do
  22	  if [ $((posnum % 2)) -eq 0 ]; then
  23	    ((posnum=posnum/2))
  24	  else 
  25	    ((posnum=1+posnum*3))
  26	  fi
  27	  ((count+=1))
  28	done
  29	
  30	echo $count

```

This was actually my second refactoring, and while I was looking at some other people's solutions, I think I may have to refactor again.  

My first refactor was to abstract out the validation process, and let the function name describe what was happening.  I'm validating input.  The `error` function is called to error out of the program if it gets bad
input. I decided to change the name of the variable from `input` to `posnum` after validation to reflect that the input had now been sanitized.  This is important, because the while loop will be infinite unless the
number is a positive integer.  

Lines 21-28 could be handled with a ternary operator, though.  This would reduce the line count, but I'm not sure if the resulting code would be as easy to read.  I'm going to try it.

```
   1	#!/usr/bin/env bash
   2	
   3	input=${1}
   4	
   5	error(){
   6	  echo "Error: Only positive numbers are allowed"
   7	  exit 1
   8	}
   9	
  10	validate(){
  11	    [[ ${1} =~ ^[0-9]+$ ]] && [[ ${1} -gt 0 ]] || error
  12	}
  13	
  14	validate ${input} 
  15	
  16	posnum=${input}   # input has now been sanitized
  17	
  18	count=0   # count iterations...
  19	
  20	# must validate input or loop is infinite
  21	while [[ ${posnum} -ne 1 ]]; do
  22	  [ $((posnum % 2)) -eq 0 ] && ((posnum=posnum/2)) || ((posnum=1+posnum*3))
  23	  ((count+=1))
  24	done
  25	
  26	echo $count
```

So I'm not sure.  What do you think?  Does that help?  I guess it's not really a ternary operator after all; it's just bash conditional logic on one line, which I love anyway. I think it works, and this is consistent
with the earlier lines, which also use this same sort of logic.  So I believe this is a good refactoring.  I basically gained 4 lines.  That's not a lot, but I think it reinforces my chosen style.

By the way, line 22 immediately above would have been written as a ternary after all: 

```
posnum=`posnum%2 == 0 ? posnum/2 : posnum*3+1`
```  

Actually, I just tried something like this on my command line, and it didn't work.  I'm going to have to experiment for a minute on that.  Probably has to do with integers and `let` I'm guessing.  I'll figure it out!

# My Conclusion 

The Collatz Conjecture is a terrific student for a slightly experienced to more-advanced student of bash, because: it requires some arithmatic skills at the commandline; it requires ability with conditional logic; and
it's not too crazy on math ability, as many other problems are.

The newer versions of bash are capable of so much more than the older versions.  It's almost like bash has grown into a full-scale scripting language!  Well, it's not on a par with Python or Ruby yet.  But it's getting
closer.  And it still possesses all of the direct ability to communicate directly with the operating system that other scripting languages use external libraries for.  So Bash is still a terrific choice for many of your
scripting needs.



