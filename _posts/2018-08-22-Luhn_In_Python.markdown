---
layout: post
title: Luhn In Python
date: 2018-08-22 14:47:33-04:00
categories: python exercism
---

## How to Solve Luhn in Python

It occurred to me I don't have a recent Python solution of an exercism problem in my blog.  Actually, I'm currently working on Yacht, which will be fun, but since I not long ago solved the Luhn problem using Bash, I was
curious to see what I had come up with for the Python solution.  Once again, here's the problem from the Exercism Python track (and in most of the language tracks):


> # Luhn
> 
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
> ```
> 4539 1488 0343 6467
> ```
> 
> The first step of the Luhn algorithm is to double every second digit,
> starting from the right. We will be doubling
> 
> ```
> 4_3_ 1_8_ 0_4_ 6_6_
> ```
> 
> If doubling the number results in a number greater than 9 then subtract 9
> from the product. The results of our doubling:
> 
> ```
> 8569 2478 0383 3437
> ```
> 
> Then sum all of the digits:
> 
> ```
> 8+5+6+9+2+4+7+8+0+3+8+3+3+4+3+7 = 80
> ```
> 
> If the sum is evenly divisible by 10, then the number is valid. This number is valid!
> 
> ## Example 2: invalid credit card number
> 
> ```
> 8273 1232 7352 0569
> ```
> 
> Double the second digits, starting from the right
> 
> ```
> 7253 2262 5312 0539
> ```
> 
> Sum the digits
> 
> ```
> 7+2+5+3+2+2+6+2+5+3+1+2+0+5+3+9 = 57
> ```
> 
> 57 is not evenly divisible by 10, so this number is not valid.
> 
> ### Submitting Exercises
> 
> Note that, when trying to submit an exercise, make sure the solution is in the `exercism/python/<exerciseName>` directory.
> 
> For example, if you're submitting `bob.py` for the Bob exercise, the submit command would be something like `exercism submit <path_to_exercism_dir>/python/bob/bob.py`.
> 
> 
> For more detailed information about running tests, code style and linting,
> please see the [help page](http://exercism.io/languages/python).
> 
> ## Source
> 
> The Luhn Algorithm on Wikipedia [http://en.wikipedia.org/wiki/Luhn_algorithm](http://en.wikipedia.org/wiki/Luhn_algorithm)
> 
> ## Submitting Incomplete Solutions
> It's possible to submit an incomplete solution so you can see how others have completed the exercise.

As you can see, the test will submit a number and based on calculations from a new instance of your module, the test passes or not.  Your module has to return the correct value when the appropriate methods are called on
it with the number used to initialize the instance.  The test called the `is_valid` method.  So a single test might look something like this:

```
    def test_a_single_zero_is_invalid(self):
        self.assertIs(Luhn("0").is_valid(), False)
```

If your method returns `False`, the test passes.  As it turns out, there were quite a few tests, fourteen of them, and my solution passed all of them.  Yay! Here was what I came up with:


```
   1	import re
   2	
   3	class Luhn(object):
   4	    '''Peforms number validation for credit cards, etc.'''
   5	    def __init__(self, string):
   6	        self.number = string
   7	        self.total = self.get_sum(string)
   8	
   9	    def get_sum(self, string):
  10	        '''returns the sum of adjusted digits in number string'''
  11	        num = int(re.sub('[^0-9]', '', string))
  12	        numlist = [ int(n) for n in reversed(str(num)) ]
  13	        for n in range(1,len(numlist),2):
  14	            if (numlist[n]*2) > 9:
  15	                numlist[n] = (numlist[n] * 2) - 9
  16	            else:
  17	                numlist[n] = numlist[n] * 2
  18	        return sum(numlist)
  19	
  20	    def is_valid(self):
  21	        '''returns true if valid number and evenly divisible by 10'''
  22	        if len(self.number) <= 1:
  23	            return False
  24	        if not self.number.replace(" ","").isdigit():
  25	            return False
  26	        else:
  27	            return self.total % 10 == 0
```

I don't get to work with Python very much these days, so Exercism is about the only excuse I have to write anything in it, currently.  Yet, I love the language.  I think it's my favorite.  I enjoy it more than Ruby or
Javascript (Node), for example.  Maybe I just have fond associations with Python, but I would love for Python to be my daily driver.  Javascript is terrific, and so is Ruby, but if I had to pick a favorite language, it
would have to be Python.

That said, all this seems rather verbose.  I think if I went back to refactor this, I could clean it up quite a bit.  I'm suspecting this was one of my early attempts on Exercism.  But at least it works.

Where would I refactor?  I'm not sure.  The `get_sum` method seems a little wordy.  But there're tradeoffs using a list comprehension.  It can be compact and terse, yet it can reduce legibility.  It can become a *list
incomprehension* instead of a list comprehension.  

Sometimes if there are too many lines to read, I think a module becomes hard to read.  It's best if there are a very few methods and a very few lines per method, so that when you look at them, they pop right into your
head as solved problems.  This doesn't quite do that yet, but I'm not prepared to refactor this right now.  But I most likely will at some point in the future.

Perhaps I should have chosen another example!!??

Here's another example from Exercism regarding a problem that validates an ISBN number:


> # ISBN Verifier
> 
> The [ISBN-10 verification process](https://en.wikipedia.org/wiki/International_Standard_Book_Number) is used to validate book identification
> numbers. These normally contain dashes and look like: `3-598-21508-8`
> 
> ## ISBN
> 
> The ISBN-10 format is 9 digits (0 to 9) plus one check character (either a digit or an X only). In the case the check character is an X, this represents the value '10'. These may be communicated with or without hyphens, and can be checked for their validity by the following formula:
> 
> ```
> (x1 * 10 + x2 * 9 + x3 * 8 + x4 * 7 + x5 * 6 + x6 * 5 + x7 * 4 + x8 * 3 + x9 * 2 + x10 * 1) mod 11 == 0
> ```
> 
> If the result is 0, then it is a valid ISBN-10, otherwise it is invalid.
> 
> ## Example
> 
> Let's take the ISBN-10 `3-598-21508-8`. We plug it in to the formula, and get:
> ```
> (3 * 10 + 5 * 9 + 9 * 8 + 8 * 7 + 2 * 6 + 1 * 5 + 5 * 4 + 0 * 3 + 8 * 2 + 8 * 1) mod 11 == 0
> ```
> 
> Since the result is 0, this proves that our ISBN is valid.
> 
> ## Task
> 
> Given a string the program should check if the provided string is a valid ISBN-10.
> Putting this into place requires some thinking about preprocessing/parsing of the string prior to calculating the check digit for the ISBN.
> 
> The program should be able to verify ISBN-10 both with and without separating dashes.
> 
> 
> ## Caveats
> 
> Converting from strings to numbers can be tricky in certain languages.
> Now, it's even trickier since the check digit of an ISBN-10 may be 'X' (representing '10'). For instance `3-598-21507-X` is a valid ISBN-10.
> 
> ## Bonus tasks
> 
> * Generate a valid ISBN-13 from the input ISBN-10 (and maybe verify it again with a derived verifier).
> 
> * Generate valid ISBN, maybe even from a given starting ISBN.
> ## Exception messages
> 
> Sometimes it is necessary to raise an exception. When you do this, you should include a meaningful error message to
> indicate what the source of the error is. This makes your code more readable and helps significantly with debugging. Not
> every exercise will require you to raise an exception, but for those that do, the tests will only pass if you include
> a message.
> 
> To raise a message with an exception, just write it as an argument to the exception type. For example, instead of
> `raise Exception`, you should write:
> 
> ```python
> raise Exception("Meaningful message indicating the source of the error")
> ```
> 
> ## Running the tests
> 
> To run the tests, run the appropriate command below ([why they are different](https://github.com/pytest-dev/pytest/issues/1629#issue-161422224)):
> 
> - Python 2.7: `py.test isbn_verifier_test.py`
> - Python 3.4+: `pytest isbn_verifier_test.py`
> 
> Alternatively, you can tell Python to run the pytest module (allowing the same command to be used regardless of Python version):
> `python -m pytest isbn_verifier_test.py`
> 
> ### Common `pytest` options
> 
> - `-v` : enable verbose output
> - `-x` : stop running tests on first failure
> - `--ff` : run failures from previous test before running other test cases
> 
> For other options, see `python -m pytest -h`
> 
> ## Submitting Exercises
> 
> Note that, when trying to submit an exercise, make sure the solution is in the `$EXERCISM_WORKSPACE/python/isbn-verifier` directory.
> 
> You can find your Exercism workspace by running `exercism debug` and looking for the line that starts with `Workspace`.
> 
> For more detailed information about running tests, code style and linting,
> please see [Running the Tests](http://exercism.io/tracks/python/tests).
> 
> ## Source
> 
> Converting a string into a number and some basic processing utilizing a relatable real world example. [https://en.wikipedia.org/wiki/International_Standard_Book_Number#ISBN-10_check_digit_calculation](https://en.wikipedia.org/wiki/International_Standard_Book_Number#ISBN-10_check_digit_calculation)
> 
> ## Submitting Incomplete Solutions
> 
> It's possible to submit an incomplete solution so you can see how others have completed the exercise.

# My approach

One thing I love about Python is its facility with regular expressions.  You have a lot of flexibility with Python and regex.  
This reminds me of one of my favorite sayings about Python:

> Python is at least the 2nd best language for any task you want to do.

This particular problem had rather simple Math to it, thank goodness.  Sometimes, the problems hurt my brain, but not this one.  This kind of problem was perfect for a list comprehension.  The problem would be making it
legible.  Sometimes, a comment is necessary in the function to clarify the list comprehension.  Anyway, here was my solution:

```
  1	def verify(isbn):
  2	    string = isbn.replace('-', '')
  3	    if string == '' or len(string) != 10:
  4	        return False
  5	    num_arr = list(string)
  6	
  7	    if num_arr[-1] == 'X':
  8	        num_arr[-1] = '10'
  9	    for val in num_arr:
 10	        try:
 11	            if int(val) not in range(0,11):
 12	                return False
 13	        except ValueError:
 14	            return False
 15	
 16	    return sum([int(num_arr[n])*(10-n) for n in range(0,9+1)]) % 11 == 0
```

Basically, the heavy lifting is being done by line 16 in the list comprehension.  The rest is mostly sanitizing input.  Ya just gotta love Python!
