---
layout: post
title: Remove Underline From Vim hi CursorLineNr
date: 2020-11-21 16:18:37-05:00
categories: vim
---
# Removing Underline from Vim Hilighted CursorLineNr

If you're like me, you work hard to get your editor to look and act just as you like it.  
When something changes without your permission, and now your editor has started looking like
it's gone rogue, that's bad.  I'm not sure what drove this change, but some time ago my 
`hi CursorLineNr` value in my color theme started displaying an underline in my editor.
It kinda drove me nuts.  Even now, when I log into a new system where my syntax coloring files
have not been updated, I have to make the change to de-gunk my line number on the cursor line.
Here'r are some notes.

## What files to change

In your `.vimrc`, you normally refer to a syntax color file.  Mine is `xoria256.vim`.  It's 
located in `$HOME/.vim/colors/xoria256.vim`.  (Your installation may vary.)  In your `.vimrc` 
there should be a line that goes something like `colorscheme xoria256` or whatever the name
of your color theme is.  
