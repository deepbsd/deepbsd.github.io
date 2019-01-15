---
layout: post
title: Roman Numerals and Square of Sums
date: 2018-08-14 12:54:02-04:00
categories: bash ruby
---

Today I'm actually going to talk about two problems.  I thought the first was interesting because I had to get primitive to solve it in bash.  I don't really know how to use hashes yet in Bash, so I just use two arrays.
The second problem is in Ruby.  I'm just learning Ruby, so I'm figuring out a lot of things as I go.  The Ruby problem is about finding the difference between the difference between the sum of squares of numbers in a
series versus the square of the sums in that series.

## Roman Numerals in Bash

So I was working on another bash program for Exercism.io, and this one took an arabic number as input and returned the equivalent Roman numeral.  The test was inputting a series of numbers and expecting a corresponding
set of roman numerals.  Here's the assignment as it is on Exercism:


> # Roman Numerals
> 
> Write a function to convert from normal numbers to Roman Numerals.
> 
> The Romans were a clever bunch. They conquered most of Europe and ruled
> it for hundreds of years. They invented concrete and straight roads and
> even bikinis. One thing they never discovered though was the number
> zero. This made writing and dating extensive histories of their exploits
> slightly more challenging, but the system of numbers they came up with
> is still in use today. For example the BBC uses Roman numerals to date
> their programmes.
> 
> The Romans wrote numbers using letters - I, V, X, L, C, D, M. (notice
> these letters have lots of straight lines and are hence easy to hack
> into stone tablets).
> 
> ```text
>  1  => I
> 10  => X
>  7  => VII
> ```
> 
> There is no need to be able to convert numbers larger than about 3000.
> (The Romans themselves didn't tend to go any higher)
> 
> Wikipedia says: Modern Roman numerals ... are written by expressing each
> digit separately starting with the left most digit and skipping any
> digit with a value of zero.
> 
> To see this in practice, consider the example of 1990.
> 
> In Roman numerals 1990 is MCMXC:
> 
> 1000=M
> 900=CM
> 90=XC
> 
> 2008 is written as MMVIII:
> 
> 2000=MM
> 8=VIII
> 
> See also: http://www.novaroma.org/via_romana/numbers.html
> 
> 
> Run the tests with:
> 
> ```bash
> bats roman_numerals_test.sh
> ```
> 
> After the first test(s) pass, continue by commenting out or removing the `skip` annotations prepending other tests.
> 
> ## Source
> 
> The Roman Numeral Kata [http://codingdojo.org/cgi-bin/index.pl?KataRomanNumerals](http://codingdojo.org/cgi-bin/index.pl?KataRomanNumerals)
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

# The Process

Fortunately, I've done this problem before in Python.  So I have a basic strategy.  I wanted to use a hash or associative array to handle it, and fortunately, bash can do those now.  However, I am not sure how to use
those yet in bash.  So, I used two arrays instead and let the index number of one (the Arabic numeral array) act as a key to the other (the Roman numeral) array.  The trick is to count from the right starting with the
largest numbers and see what's left over.  Along the way, I'm building a string of Roman numerals that stops when I run out of values.

One of the tricks here is to have a counter that prints a Roman numeral more than once where appropriate.  For example, the number 30 requires three X's, and so on.  I cannot just multiply a character by a count as I
might in some other languages.  Bash is not a language where you can do that.  On line 16 I have to use the `printf` command with a format string followed by a range.  It's a little strange, but hey, that's programming.

The biggest weirdness here is that you have to count in Roman.  That means you have to check for multiples of 9 and 4 especially.  Those symbols will be unique.  

The overall requirement is to start with your input number and divide the biggest number into that you can from the Roman system, as many times as possible, then add those symbols to your resulting string.  Then,
sumbtract that value from the number.  Next, take the next largest value from the Roman system and divide that in as many times as possible and add the Roman symbols to your result. Remove the values from the number as
required.  Then repeat this process until you have zero.

Small example:  You start with the number 8.  The largest value from the Roman system that will divide into this is `V`.  It only goes once.  So your result string now gets a `V`.  Subtract 5 from 8 and you have 3.  The
largest value that now goes in is `I`.  It goes in 3 times, so your result now is `VIII`.  Once you subtract 3 from the number, you now have zero, so you're done.  `VIII` is your result.  That's the basic process.

```
   1	#!/usr/bin/env bash
   2	
   3	num=${1}
   4	
   5	romans=( 'M' 'CM' 'D' 'CD' 'C' 'XC' 'L' 'XL' 'X' 'IX' 'V' 'IV' 'I')
   6	integers=( 1000 900 500 400 100 90 50 40 10 9 5 4 1 )
   7	
   8	result=''
   9	
  10	for n in $(seq 0 $((${#integers[@]}-1)));
  11	do
  12	  count=$((num/integers[n]))
  13	  if [ ${count} -ge 1 ]; then
  14	      for ((i=1; i<=${count}; i++))
  15	      do
  16	          result+=$(printf "${romans[n]}%.0s" {1..${count}} )
  17	      done
  18	  else 
  19	      result+=''
  20	  fi
  21	  ((num-=(integers[n]*count)))
  22	done
  23	
  24	echo ${result}
```

## Ruby: Square of Sums vs The Sum of Squares

Once again, this problem is from Exercism.io.  Here's the README.md for the problem:


> # Difference Of Squares
> 
> Find the difference between the square of the sum and the sum of the squares of the first N natural numbers.
> 
> The square of the sum of the first ten natural numbers is
> (1 + 2 + ... + 10)² = 55² = 3025.
> 
> The sum of the squares of the first ten natural numbers is
> 1² + 2² + ... + 10² = 385.
> 
> Hence the difference between the square of the sum of the first
> ten natural numbers and the sum of the squares of the first ten
> natural numbers is 3025 - 385 = 2640.
> 
> * * * *
> 
> For installation and learning resources, refer to the
> [exercism help page](http://exercism.io/languages/ruby).
> 
> For running the tests provided, you will need the Minitest gem. Open a
> terminal window and run the following command to install minitest:
> 
>     gem install minitest
> 
> If you would like color output, you can `require 'minitest/pride'` in
> the test file, or note the alternative instruction, below, for running
> the test file.
> 
> Run the tests from the exercise directory using the following command:
> 
>     ruby difference_of_squares_test.rb
> 
> To include color from the command line:
> 
>     ruby -r minitest/pride difference_of_squares_test.rb
> 
> 
> ## Source
> 
> Problem 6 at Project Euler [http://projecteuler.net/problem=6](http://projecteuler.net/problem=6)
> 
> ## Submitting Incomplete Solutions
> It's possible to submit an incomplete solution so you can see how others have completed the exercise.

# My Approach

With Ruby being a heavily object oriented language, lots of problems are solved by creating a class module.  That class gets instantiated as a new instance in the test file, and then the class methods are run to see if
they work as expected to produce the required results in the test.  This solution basically took three lines of Ruby code.  The other 10-15 lines were all setup for the class.  Here's my code:

```
   1	class Squares
   2	
   3	    def initialize(number)
   4	      @number = number
   5	    end
   6	
   7	    def square_of_sum()
   8	      (1..@number).reduce(:+)**2
   9	    end
  10	
  11	    def sum_of_squares()
  12	      (1..@number).inject { |sum, num| sum + num**2 }
  13	    end
  14	
  15	    def difference()
  16	      square_of_sum() - sum_of_squares()
  17	    end
  18	
  19	end
  20	
  21	module Bookkeeping
  22		VERSION = 4 # Where the version number matches the one in the test
  23	end
```

This little bit of code took a lot of research actually, and what you see is at least the second refactoring.  I consolidated 2 lines into 1 line for `square_of_sum` and also `sum_of_squares`.  I haven't done much ruby
code, and most of what I have done has strictly been in Rails.  So I just haven't used the power of basic Ruby very much.

The range with `reduce` is actually sort of *Javascriptish* for me.  I actually don't use that idea very much, since I started with Python, and Guido depricated it because it seemed less *Pythonic* and he wanted
programmers to get away from using it.  It's still a part of the `itertools` library in Python.  But, consequently, I don't use `map` or `reduce` very much in other languages when I probably should.  It may not be
*Pythonic*, but it is definitely *Rubyistic* and also *Javascriptish*!!

`inject` is something I've never heard of before this exercise.  I'm not sure what the difference is yet between `reduce` and `inject`.  They seem to be much alike to me.  But I'm just learning, so nevermind.  Still,
this seems to work, and it's apparently very *Rubyistic*.  

The `VERSION` thing at the bottom is simply part of the Exercism Ruby track; apparently, they like to keep track of test versions.

# Closing

I've been working on both of these problems recently. The two languages couldn't be more different.  However, solving problems is similar in almost any language.  You just have to *think* in that language.  Fortunately,
these are simple problems, but simple problems are best when you're dealing with new languages.  Or even new ways of using languages!
