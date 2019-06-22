---
layout: post
title: Run Length Encoding in Javascript
date: 2019-06-22 12:33:23-04:00
categories: JS,programming
---
# Run Length Encoding in Javascript

I've been a fan of Python for several years now, and I've loved it for its 
succinctness and expressiveness.  Likewise, I've lamented that Javascript
is not as succinct or expressive.  But I'm starting to believe I've been
laboring under a misconception.  I simply don't know Javascript as well as
I thought I did, and, also, that ES6 in many cases is as succinct as Python.
I now believe that JS can be the equal of Python in succinct and elegant
solutions, if only I can use the power of the language by understanding its
subtleties.

## What is Run Length Encoding?  Here's the README...

Implement run-length encoding and decoding.

Run-length encoding (RLE) is a simple form of data compression, where runs
(consecutive data elements) are replaced by just one data value and count.

For example we can represent the original 53 characters with only 13.

```text
"WWWWWWWWWWWWBWWWWWWWWWWWWBBBWWWWWWWWWWWWWWWWWWWWWWWWB"  ->  "12WB12W3B24WB"
```

RLE allows the original data to be perfectly reconstructed from
the compressed data, which makes it a lossless data compression.

```text
"AABCCCDEEEE"  ->  "2AB3CD4E"  ->  "AABCCCDEEEE"
```

For simplicity, you can assume that the unencoded string will only contain
the letters A through Z (either lower or upper case) and whitespace. This way
data to be encoded will never contain any numbers and numbers inside data to
be decoded always represent the count for the following character.

## Setup

Go through the setup instructions for Javascript to install the necessary
dependencies:

[https://exercism.io/tracks/javascript/installation](https://exercism.io/tracks/javascript/installation)

## Requirements

Install assignment dependencies:

```bash
$ npm install
```

## Making the test suite pass

Execute the tests with:

```bash
$ npm test
```

In the test suites all tests but the first have been skipped.

Once you get a test passing, you can enable the next one by changing `xtest` to
`test`.

## Source

Wikipedia [https://en.wikipedia.org/wiki/Run-length_encoding](https://en.wikipedia.org/wiki/Run-length_encoding)

## Submitting Incomplete Solutions

It's possible to submit an incomplete solution so you can see how others have
completed the exercise.


## My First Solution

I was delighted when my tests finally passed, even if my solution was less than succinct and elegant:

```javascript
export const decode = (text) => {

    if (text === '') return '';
    let input = text;
    let regex = /((\d+)?(\D))/g;
    let result = '';
    let match = regex.exec(input);
    do {
        result += match[3].repeat(+match[2]) || match[3];
        match = regex.exec(input);
    } while (match);

    return result;
};

export const encode = (text) => {
    if (text === '') return '';
    let input = text;
    let regex = /(.)\1*/g;
    let result = '';
    let match = regex.exec(input);
    do {
        match[0].length > 1 ? result += match[0].length + match[1] : result += match[1];
        match = regex.exec(input);
    } while (match);

    return result;
};
```

As you can see, I'm struggling to say what I mean.  My solution in Python was much more succinct:

## My Solution in Python

I maintain that Python is the Cadillac of scripting languages.  It's easy to say what you mean:

```python
from re import sub

def decode(text):

    return sub(r'(\d+)(\D)', lambda m: m.group(2) * int(m.group(1)),
               text)


def encode(text):

    return sub(r'(.)\1*', lambda m: str(len(m.group(0))) + m.group(1) if len(m.group(0)) > 1 else str(m.group(1)),
               text)
```
## Final Solution in Javascript

It turns out you can get pretty succinct and expressive simply by using ES6 syntax and picking the right JS method:

```javascript
export const decode = (text) => {
    return text.replace(/(\d+)([ \w])/g, (_, count, chr) => chr.repeat(count));
};

export const encode = (text) => {
   return text.replace(/([ \w])\1+/g, (group, chr) => group.length + chr );
};
```

Now, looking at this code, the problem is essentially solved in two lines. I didn't need to import the re module as I did 
in Python.  Once I passed a callback function to the `replace` method, I was in business.  Beforehand, I thought I had to 
run a while loop and iterate through the matches in the regex.exec() method.  Turns out, passing a callback to the replace
method was as expressive and succinct as Python's lambda expression was!  

I guess you might even say that arrow functions are the equivalent of Python's lambda functions!  Probably someone thinks
I've just blasphemed, but whatever.  I mean it as a compliment to Javascript!  

I'm not really a language zealot, but I am feeling more comfortable with Javascript.  Not as comfortable as with Python,
but still pretty comfortable.  It makes me happy that I found a way to be as expressive and concise in Javascript as I was
in Python.
