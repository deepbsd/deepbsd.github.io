---
layout: post
title: Grepping Project Files in Vim
date: 2019-05-16 13:54:04-04:00
categories: Vim
---
## Using Vimgrep To Find Project Files

One of the tasks I never got smooth at with Vim is finding project files that contained
a certain regex match.  I don't seem to have this problem on the command line, but somehow
I never got smooth with it in Vim.  When using Atom or Sublime, Ctl-S searches through the
project easily and finds matches and displays a link to each match in each matching file.
How handy!  But how does one do this in Vim?

I think the challenge for me has been to pick a method.  There are so many approaches to 
solving this problem that I get overwhelmed.  So bearing that in mind (there are many
approaches or solutions) today I'll pick what seems for the moment to be my fallback approach:
`vimgrep`.

# Syntax

The basic syntax is:
```
:vimgrep /pattern/args path_to_files
```
An example that recursively finds all uppercase instances of 'UNIX' in a set of configuration 
files could be:
```
:vimgrep /UNIX/g **/*.conf
```
You could also use this on the current buffer with `:vimgrep /UNIX/g %` because '%' is a reserved
symbol that represents the filepath of the active buffer.  The 'g' argument on the regex means to
include every match on the line, not just the first match in the line.

# The Quickfix List
What we're actually creating behind the scenes is a special list of files we want to fix in Vim.
Vim calls this the "quickfix" list.  This is one of Vim's most powerful tools, and there are many
ways to populate this list.  See `:help quickfix` for lots more information on it.

This is not to be confused with the `arglist`, which is the list of files we want to search in
our project.  That list would be created by the `**/*.conf` argument, which is its own regex,
where `**/` says to recursively search, and `*.conf` says to just search files ending in 'conf'.
To see the arglist at any point in time, simply type `:args` in the command buffer.

Vim is always keeping track of several lists, including the `bufferlist` and probably many more 
I'm not thinking of.  But for the moment, we're just talking quickfix list, the results of your 
recursive project search.  

The default behavior is to start at the top of the list, in the first file with a match to your
regex.  So in your current buffer you would see something like:
```
# Ain't UNIX grand!
```
with the cursor blinking in front of the word UNIX.  You would be in the first 'conf' file in your
quickfix list.  You would be in edit mode.  If you did the following in the command buffer
```
:cnext
```

you would be magically transported to the next file in your quickfix list, at the next match.  Again in edit mode.  If the
current buffer has more than one match, `n` will take you to it or give you `Search hit BOTTOM, continuing from TOP`
warning at the bottom of the screen. `:cprev` will move you to the previous entry in the quickfix list, if it exists.  If
you just want to see the list itself, type `:clist` in the command buffer.  `:cfirst` and `:clast` will take you to the
first and last items in the quickfix list.  

At this point, for me, I like to see the quickfix list first rather than jump to the first 
match in the first file, so I suppress this behavior by using vimgrep with the `/pattern/gj` 
argument:
```
:vimgrep /UNIX/gj **/*.conf
```
The `j` option suppresses the auto jump behavior, and you see the same buffer you had before
the search.  It is not obvious that the quickfix list has been created, that the vimgrep 
command was successful.  So to prove that it was, now you type:
```
:clist
```
and now you can see the quickfix list.  To edit the first file, simply type `:cfirst`.
Then you could keep progressing through each file match in the list with `:cnext`.

# An Example Exercise
Perhaps a simple demonstration is best.  Create the following test directory and file structure
in your home directory:
```
$ mkdir TEST_DIR
$ touch TEST_DIR/{one,two,three,four}.txt
$ echo for f in TEST_DIR/*
> do
> echo "filename: $f" >> $f
> echo "this is a second line in $f" >> $f
> done
```
Now you have some files to work on in Vim. You can play with this however you like, but open Vim 
in your home directory and type
```
:vimgrep /filename/gj **/*.txt
```
and see what happens?  You'll need to type the `:clist` command and then the `:cfirst` command.
You can cycle through files with `:cnext` and `:cprev`.  You could test the accuracy of the 
search with just searching for `:vimgrep /one/g **/*.txt` which might even include other files
not included in the exercise.  In short, you can play with this, and just pay attention to what
you're doing, since you already know that Vim is powerful and will do exactly what you tell it.

# Other Search Tools

Vimgrep is just one option to use for searching your projects.  There are external tools, like 
`Ggrep` from Tim Pope's 'Fugitive', `Ack.vim` and the `:Ack` command and the `:Ag` command from 
`ag.vim`.  These are widely used tools, but I recommend starting with the built-in `:vimgrep`.  
I have not yet outgrown just using `:vimgrep`.

Also, can also use the entire UNIX toolset for populating your arglist as well with 
```
:args find . -type f -name 'pattern'
```
for example, which would probably be too big a list.  You could also simply go 
`:args grep pattern **/*.scss` if you simply wanted
to recursively search all your SASS files for 'pattern'.  

# More Information

This is a large topic. I would start with Vim's `:help quickfix` and `:help :vimgrep` documentation.  Please
remember Drew Niel's _Practical Vim_ and particularly chapters 12, 16 and 17.  With so much information on
Vimgrep available on the web, you can almost search in any direction and find success!






