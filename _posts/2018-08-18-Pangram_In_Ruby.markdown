---
layout: post
title: Pangram In Ruby
date: 2018-08-18 19:59:36-04:00
categories: ruby
---
## Sovling for Pangrams in Ruby

As you probably have discerned, I've been recreationally learning Ruby.  I had a class in it perhaps a couple of years ago, but I never felt very fluent in the language.  There's so much written about what a programmer
friendly language it is, and while I can see some of that being true, I feel I'm missing a lot about why it's more friendly or less friendly than, say Python or Javascript.  So, I think I just need a little more
experience solving problems.

Today's example comes from the Exercism.io Pangram exercise:


> # Pangram
> 
> Determine if a sentence is a pangram. A pangram (Greek: παν γράμμα, pan gramma,
> "every letter") is a sentence using every letter of the alphabet at least once.
> The best known English pangram is:
> > The quick brown fox jumps over the lazy dog.
> 
> The alphabet used consists of ASCII letters `a` to `z`, inclusive, and is case
> insensitive. Input will not contain non-ASCII symbols.
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
>     ruby pangram_test.rb
> 
> To include color from the command line:
> 
>     ruby -r minitest/pride pangram_test.rb
> 
> 
> ## Source
> 
> Wikipedia [https://en.wikipedia.org/wiki/Pangram](https://en.wikipedia.org/wiki/Pangram)
> 
> ## Submitting Incomplete Solutions
> It's possible to submit an incomplete solution so you can see how others have completed the exercise.

# My Approach

The simplest approach it seems to me is to take the set of characters that comes as input, remove duplicates, sort those characters, and see if it's equal to the alphabet.  From what I can see, however, Ruby doesn't
have a Set function in the standard library.  You have to import it.  Is that weird?  I wonder what the think was there?  In Python, you have Sets built-in.  You don't have to import it.  

But maybe there's another way to think about it?  You could just create your own set of characters that equals the alphabet.  And then you could ask whether each character of *that* set is included in the input string.
Essentially, I think that's the same solution, isn't it?  Except that you are not calling Set on anything.  So what would that look like?  What would the steps be?

1. Create a list of lowercase (my choice) characters that equals the alphabet.

2. Take each character in the input string, and check it for being in the alphabet.  No wait.  That's wrong.  It's gotta be the other way around!  Check each letter of the alphabet to make sure it's included in the
   input string!

3. Return true if each character of the alphabet *is* included and false otherwise.

That's it!  So how do you do that in Ruby?  Well, there's the `.all?` method and also the `.includes?` method.  Now, these are programmer friendly methods it seems to me.  Anyway, here's what the code eventually came to
look like.  Notice, there are some differences, for sure, between this and Python and Javascript.

```
   1	class Pangram
   2	
   3	    def self.pangram?(line=' ')
   4	      ('a'..'z').all? { |char| line.downcase.include? (char) }
   5	    end
   6	
   7	end
   8	
```

It turns out this is a pretty standard solution for this early exercise in a language.  Lots of people have come up with something just like this.  Here's what I like about doing this in Ruby:

* I like how adding a '?' to a method name goes with returning a Boolean.  I haven't seen another language do that.

* I like how you can successively chain methods together like a choo choo train, and how it still usually is readable.  

Now, in this case, what I am not sure I like is how I called downcase on 'line' for 26 times.  I could have created a variable called `characters` that was created from the input line that was downcased just once.  But,
that would have been an extra line of code.  How much compute power does it require to change a character from upper case to lower case?  So I figured just keep it on one line and let the computer sweat a little bit
extra.  Save the effort on my brain for a problem that mattered a little more, because I don't think it's going to make that big a difference in this case.

# Conclusion

I conclude that I have a LOT to learn in Ruby.  In lots of other stuff too, but a whole big bunch of stuff to learn in Ruby.  Oh, I think I'm learning that Ruby is pretty friendly!  Maybe I just need to get friendlier
with it!

