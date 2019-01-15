---
layout: post
title: Math With Bash
date: 2018-08-07 14:33:56-04:00
categories: bash programming
---

## Doing Math in Bash

Bash wasn't really created for doing heavy duty math.  There are lots of limitations in that department.  However,
there are also some workarounds.  I won't get to too many of those today, but I will share a couple of projects I did
recently for the website `exercism.io`.


# Luhn

> Given a number determine whether or not it is valid per the Luhn formula.
> 
> The [Luhn algorithm](https://en.wikipedia.org/wiki/Luhn_algorithm) is
> a simple checksum formula used to validate a variety of identification
> numbers, such as credit card numbers and Canadian Social Insurance
> Numbers.
> 
> The task is to check if a given string is valid.
> 
> Validating a Number
> ------
> 
> Strings of length 1 or less are not valid. Spaces are allowed in the input,
> but they should be stripped before checking. All other non-digit characters
> are disallowed.
> 
> ## Example 1: valid credit card number
> 
> ```text
> 4539 1488 0343 6467
> ```
> 
> The first step of the Luhn algorithm is to double every second digit,
> starting from the right. We will be doubling
> 
> ```text
> 4_3_ 1_8_ 0_4_ 6_6_
> ```
> 
> If doubling the number results in a number greater than 9 then subtract 9
> from the product. The results of our doubling:
> 
> ```text
> 8569 2478 0383 3437
> ```
> 
> Then sum all of the digits:
> 
> ```text
> 8+5+6+9+2+4+7+8+0+3+8+3+3+4+3+7 = 80
> ```
> 
> If the sum is evenly divisible by 10, then the number is valid. This number is valid!
> 
> ## Example 2: invalid credit card number
> 
> ```text
> 8273 1232 7352 0569
> ```
> 
> Double the second digits, starting from the right
> 
> ```text
> 7253 2262 5312 0539
> ```
> 
> Sum the digits
> 
> ```text
> 7+2+5+3+2+2+6+2+5+3+1+2+0+5+3+9 = 57
> ```
> 
> 57 is not evenly divisible by 10, so this number is not valid.
> 
> 
> Run the tests with:
> 
> ```bash
> bats luhn_test.sh
> ```
> 
> After the first test(s) pass, continue by commenting out or removing the `skip` annotations prepending other tests.
> 
> ## Source
> 
> The Luhn Algorithm on Wikipedia [http://en.wikipedia.org/wiki/Luhn_algorithm](http://en.wikipedia.org/wiki/Luhn_algorithm)
> 
> 
> ## External utilities
> `Bash` is a language to write scripts that works closely with various system utilities,
> like [`sed`](https://www.gnu.org/software/sed/), [`awk`](https://www.gnu.org/software/gawk/), [`date`](https://www.gnu.org/software/coreutils/manual/html_node/date-invocation.html) and even other programming languages, like [`Python`](https://www.python.org/).
> This track does not restrict the usage of these utilities, and as long as your solution is portable
> between systems and does not require installing third party applications, feel free to use them to solve the exercise.
> 
> For an extra challenge, if you would like to have a better understanding of the language,
> try to re-implement the solution in pure `Bash`, without using any external tools.
> 
> ## Submitting Incomplete Solutions
> It's possible to submit an incomplete solution so you can see how others have completed the exercise.
> 
> So, that's the assignment.  Using that recipe described, write a program that will return the number of steps
> required (each step uses the recipe once) to reduced the number passed into the program down to the number 1.  That's
> it!

# How To Solve It (my approach, anyway)

Now, shell scripts can become very long, be what I like about Exercism is that the assignments can be challenging but
generally only require a couple dozen lines or so.  Sometimes far less.  So, for this problem, I tried to break the
recipe down into steps:

1. Take in a number as an argument.

2. Validate the number; it can have hyphens and spaces, but those must be filtered out.

3. Reverse the numbers so we can proceed from right to left (my preference; it could be done another way).

4. Put this reversed list of numbers into an array.

5. Iterate over the list and double each second number (from the left now.)

6. On each second number that has been doubled, if the number is greater than 9, subtract 9 from that number.
   Otherwise, the number remains doubled from the original.

7. While iterating over the list of numbers, ensure that a sum of each number in the array is calculated

8. When all numbers in the list have been processed, determine if 10 can be divided evenly into that sum.  If so,
   return a 'true' (it *is* a valid Luhn number) or a 'false' if not.

9. Return a 0 exit status if the number *is* a Luhn number and a non-zero exit status if it isn't.
   Oops!  Nope, whoever wrote the test for this exercise did not follow this convention.  So, always return 0.


Here's my final draft that passed all the tests:

```
#!/usr/bin/env bash

# needs gnu rev to reverse string
input=$( echo ${1} | rev | tr -d ' ')

# DRY (don't repeat yourself...)
error(){
    # why does test look for 0 return status on failure????
    echo "false" && exit 0
}

# validate input
( [[ ${input} =~ ^[0-9]+$ ]] && [ ${#input} -gt 1 ] ) || error

# create an iterator
arr=($(echo $input | grep -o .))

sum=0
n=0   # index number for arr

# iterate through the list of numbers
for num in ${arr[@]};
do
  if [ $((n%2)) -ne 0 ]; then  # each uneven index number; even index numbers are unchanged
    ((arr[n]=2*num))
    if [ ${arr[n]} -gt 9 ]; then  # still on uneven index numbers
      ((arr[n]=arr[n]-9))
    fi
  fi
  ((sum+=arr[n]))   # sum both even and odd index numbered elements of the list
  ((n++))           # increment the index number
done

# Finally, return "true" or "false"
( [ $((sum%10)) -eq 0 ] && echo "true" ) || error
```

# Notes on Solution

Another nice thing about Exercism.io is that you can look at other people's solutions.  Most of the other solutions I
looked at were some variation on this one.  People still have semantic preferences.  I have mine.  You can probably
notice several of them.

1. If I can avoid three lines for an entire `if` statement, I'll often use an '||' statement instead.  Logically it
   usually works out to the same thing.  In this case, however, brace expansion happens after square bracket
   evaluation, so I had to break out this solution into an `if` statement to ensure the arithmatic turned out
   correctly.

2. I often use an error function to exit with a non-zero exit status.  Otherwise, the program completes with 0
   status.

3. I try to use more than enough comments so it's impossible to not see what I was thinking.  Hopefully it's
   possible to make that impossible!

4. I prefer to say an expression on one line if it's not that complicated.  Otherwise, I'll break it out into more
   than one line.  Clarity first.

5. I generally will write `${name}` instead of `$name`.  I think it's a good habit, usually.

At the very beginning, I mention in the note you need to have gnu `rev` installed.  If you're on a Mac, I'm not sure
how to make this happen.  Perhaps you can load it in through `homebrew`?  Not sure.  It was already on my Mint box.
But lots of Bashers use Macs these days.  The environments can be quite different.

Also, Bash has loads of useful symbols: `@?` `#!` '#?' `!^` and so on.  I only know a small subset of them, and I
assume others don't know them all either.  So I use them somewhat sparingly.

Otherwise, I think I'm rather mainstream, nothing too special.  Hopefully, when someone looks at my code, it's pretty
straightforward what the hell I'm talking about.  That's what I strive for, anyway.


# More Complexity

When it comes to more complicated math, there are other tools.  You can use tools like `awk` or better yet, `bc`.
At your command line now, try this: `echo '0.5*88.4' | bc`.  If you have `bc` installed, you should see the answer
`44.2` coming back to you.  So another option is to use `bc` in your scripts where you need more precision than with
simple integers that I've used in this Luhn example above.
