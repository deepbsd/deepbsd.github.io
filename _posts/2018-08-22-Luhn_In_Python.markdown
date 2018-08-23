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
