---
layout: post
title: Lambdas in Javascript?
date: 2018-11-12 12:19:31-05:00
categories: programming
---

## Does Javascript Have Lambdas like Python?

I came across this not long ago.  In fact, I was helping to teach an introductory course on Javascript, and there happened to be a veteran programmer in attendance, and we wound up sitting together while my partner
taught the class.  He (the veteran programmer) had been programming in Java for 20 some years and mentioned to me that he had been using lambdas in Javascript.  Well, I had used them in Python, but never Javascript, at
least to my knowledge.  I asked if I had heard correctly, and he said, yes, they were lambdas he had been using.  He had come to the Javascript class because he really didn't know much about using it, despite having
worked in Java for so long, so I thought maybe he had misheard or misunderstood--or maybe I had.

Now, let me say right off that I haven't been programming in Python for as long as he has been programming in Java.  It's been maybe three years for me, and two of those years have been focused on javascript.  But I was
pretty intense about Python for most of 2014 and 2015, and I did quite a bit of programming in Python in 2016.  So I give myself 3 years experience.  And more like two years in Javascript.  And Lambda expressios were
always one of those things in Python that I figured I'll get around to understanding better _one day soon_!  But the gist is that a lambda is a way of creating a function expression without a `def` statement,
so you can reuse a function in simple one-line or so expressions.  They are intended to be handy little tools, as I understand it.  They were not intended to be used to replace `def` statements.  You don't use a lambda
expression where you should declare a function using `def`.  It's more like a tweezers than a crowbar or refrigerator dolly.

## So How Do You Use a Lambda Expression in Python?

Once again [W3 Schools](https://www.w3schools.com/python/python_lambda.asp) has a good explanation.

A lambda expression doesn't have to be anonymous:  
`name = lambda arguments : expression`
or
``` 
Robin = lambda str : 'Holy ' + str + " Batman!" 
```

So now you could say `Robin("television addiction")` and you would get back, `Holy television addiction, Batman!`  So in this case, the lambda expression is a simple string concatenation.  But you could do math or
substitution or plenty of other things too.  But this is the basic idea.  It's a function one-liner that can also be anonymous.

If you wanted to sum the numbers passed to a function:  
```
l = lambda *args : sum(args)
``` 
and now you could say `l(1,2,3,4)` and you'd get `10` back.  `sum` is a handy Array method in Python.  We would have to use `reduce` in Javascript.

Mind you, there are many more ways than this to use lambda expressions in Python.  But I'll stop here for now.

## So How Do You Do This in Javascript?

I'm using a terminal with Node running in it for these examples just like I was running python3 in a terminal for the previous examples.  Typing the following in a Node terminal:
```
let robin = str =>  "Holy "+str+", Batman!" 
```
You'll get the above mentioned effect in Node.  If you enter `robin('television addiction')` you will also get `Holy television addiction, Batman!` just as in Python.  Officially, I think you could call this a lambda
expression in Javascript.

You could go:
```
const sumit = (total, num) => total + num 
```
and then you could say:
```
[1,2,3,4].reduce(sumit)
```

But I don't see that as the same thing.  First of all, we don't have list comprehensions in Javascript. But wait, JS has an `arguments` variable and the 'rest' variable `(...args)`, so I wonder what we could do with that?

```
const sumit = (...args) => args.reduce((x,y) => x+y ) 
```

Now, if we call `sumit(1,2,3,4)` we get the right answer.  

So, is this a lambda function in JS?  Hmmm...  I think maybe it is!  


## Conclusion: JS Lambda Expressions Like Python

Well, I'm just beginning my exploration of lambda expressions in JS, so I'm not concluding anything.  But I now feel like there's more to this than I thought at the beginning of this article.  It's taken me a couple of
hours of struggling at the command line and the input of smarter people than I in my Slack channels to get to this point.  

But I think I can say that we _do_ have lambda expressions in Javascript.  At least sorta.  I'm confident that I can at least say at least we sorta do!  Maybe even we _really do_, but that will require more research!
