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
of your color theme is.  But what really needs modifying is the colorscheme file itself.

Here is what mine looks like:

```
{% raw %}
     1	" Vim color file
     2	"
     3	" Name:       xoria256.vim
     4	" Version:    1.6
     5	" Maintainer:	Dmitriy Y. Zotikov (xio) <xio@ungrund.org>
     6	"
     7	" Should work in recent 256 color terminals.  88-color terms like urxvt are
     8	" NOT supported.
     9	"
    10	" Don't forget to install 'ncurses-term' and set TERM to xterm-256color or
    11	" similar value.
    12	"
    13	" Color numbers (0-255) see:
    14	" http://www.calmar.ws/vim/256-xterm-24bit-rgb-color-chart.html
    15	"
    16	" For a specific filetype highlighting rules issue :syntax list when a file of
    17	" that type is opened.
    18	"
    19	" TODO: link colours instead of setting values explicitly
    20	
    21	" Initialization {{{
    22	if &t_Co != 256 && ! has("gui_running")
    23	  echoerr "Please use GUI or a 256-color terminal (which sets t_Co=256)."
    24	  finish
    25	endif
    26	
    27	set background=dark
    28	
    29	hi clear
    30	
    31	if exists("syntax_on")
    32	  syntax reset
    33	endif
    34	
    35	let colors_name = "xoria256"
    36	"}}}
    37	" Colours {{{1
    38	"" General {{{2
    39	hi Normal       ctermfg=252 guifg=#d0d0d0 ctermbg=234 guibg=#1c1c1c cterm=none gui=none
    40	hi Cursor                                 ctermbg=214 guibg=#ffaf00
    41	hi CursorColumn                           ctermbg=238 guibg=#444444
    42	"hi CursorLine                             ctermbg=237 guibg=#3a3a3a cterm=none gui=none 
    43	hi CursorLine                             ctermbg=237 ctermfg=grey guibg=#3a3a3a cterm=none gui=none 
    44	hi CursorLineNr                             ctermfg=white ctermbg=magenta guibg=#3a3a3a cterm=none gui=none 
    45	hi Error        ctermfg=15  guifg=#ffffff ctermbg=1   guibg=#800000
    46	hi ErrorMsg     ctermfg=15  guifg=#ffffff ctermbg=1   guibg=#800000
    47	hi FoldColumn   ctermfg=247 guifg=#9e9e9e ctermbg=233 guibg=#121212
    48	hi Folded       ctermfg=255 guifg=#eeeeee ctermbg=60  guibg=#5f5f87
    49	hi IncSearch    ctermfg=0   guifg=#000000 ctermbg=223 guibg=#ffdfaf cterm=none gui=none
    50	hi LineNr       ctermfg=247 guifg=#9e9e9e ctermbg=233 guibg=#121212
    51	hi MatchParen   ctermfg=188 guifg=#dfdfdf ctermbg=68  guibg=#5f87df cterm=bold gui=bold
    52	" TODO
    53	" hi MoreMsg
    54	hi NonText      ctermfg=247 guifg=#9e9e9e ctermbg=233 guibg=#121212 cterm=bold gui=bold
    55	hi Pmenu        ctermfg=0   guifg=#000000 ctermbg=250 guibg=#bcbcbc
    56	hi PmenuSel     ctermfg=255 guifg=#eeeeee ctermbg=243 guibg=#767676
    57	hi PmenuSbar                              ctermbg=252 guibg=#d0d0d0
    58	hi PmenuThumb   ctermfg=243 guifg=#767676
    59	hi Search       ctermfg=0   guifg=#000000 ctermbg=149 guibg=#afdf5f
    60	hi SignColumn   ctermfg=248 guifg=#a8a8a8
    61	hi SpecialKey   ctermfg=77  guifg=#5fdf5f
    62	" hi SpellBad     ctermfg=160 guifg=fg      ctermbg=bg                cterm=underline               guisp=#df0000
    63	hi SpellBad                               ctermbg=238                                               guisp=#df0000
    64	hi SpellCap     ctermfg=189 guifg=#dfdfff ctermbg=bg  guibg=bg      cterm=underline gui=underline
    65	hi SpellRare    ctermfg=168 guifg=#df5f87 ctermbg=bg  guibg=bg      cterm=underline gui=underline
    66	hi SpellLocal   ctermfg=98  guifg=#875fdf ctermbg=bg  guibg=bg      cterm=underline gui=underline
    67	hi StatusLine   ctermfg=15  guifg=#ffffff ctermbg=239 guibg=#4e4e4e cterm=bold gui=bold
    68	hi StatusLineNC ctermfg=249 guifg=#b2b2b2 ctermbg=237 guibg=#3a3a3a cterm=none gui=none
    69	hi TabLine      ctermfg=fg  guifg=fg      ctermbg=242 guibg=#666666 cterm=none gui=none
    70	hi TabLineFill  ctermfg=fg  guifg=fg      ctermbg=237 guibg=#3a3a3a cterm=none gui=none
    71	" FIXME
    72	hi Title        ctermfg=225 guifg=#ffdfff
    73	hi Todo         ctermfg=0   guifg=#000000 ctermbg=184 guibg=#dfdf00
    74	hi Underlined   ctermfg=39  guifg=#00afff                           cterm=underline gui=underline
    75	hi VertSplit    ctermfg=237 guifg=#3a3a3a ctermbg=237 guibg=#3a3a3a cterm=none gui=none
    76	" hi VIsualNOS    ctermfg=24  guifg=#005f87 ctermbg=153 guibg=#afdfff cterm=none gui=none
    77	" hi Visual       ctermfg=24  guifg=#005f87 ctermbg=153 guibg=#afdfff
    78	hi Visual       ctermfg=255 guifg=#eeeeee ctermbg=96  guibg=#875f87
    79	" hi Visual       ctermfg=255 guifg=#eeeeee ctermbg=24  guibg=#005f87
    80	hi VisualNOS    ctermfg=255 guifg=#eeeeee ctermbg=60  guibg=#5f5f87
    81	hi WildMenu     ctermfg=0   guifg=#000000 ctermbg=150 guibg=#afdf87 cterm=bold gui=bold
    82	
    83	"" Syntax highlighting {{{2
    84	hi Comment      ctermfg=244 guifg=#808080
    85	hi Constant     ctermfg=229 guifg=#ffffaf
    86	hi Identifier   ctermfg=182 guifg=#dfafdf                           cterm=none
    87	hi Ignore       ctermfg=238 guifg=#444444
    88	hi Number       ctermfg=180 guifg=#dfaf87
    89	hi PreProc      ctermfg=150 guifg=#afdf87
    90	hi Special      ctermfg=174 guifg=#df8787
    91	hi Statement    ctermfg=110 guifg=#87afdf                           cterm=none gui=none
    92	hi Type         ctermfg=146 guifg=#afafdf                           cterm=none gui=none
    93	
    94	"" Special {{{2
    95	""" .diff {{{3
    96	hi diffAdded    ctermfg=150 guifg=#afdf87
    97	hi diffRemoved  ctermfg=174 guifg=#df8787
    98	""" vimdiff {{{3
    99	hi diffAdd      ctermfg=bg  guifg=bg      ctermbg=151 guibg=#afdfaf
   100	"hi diffDelete   ctermfg=bg  guifg=bg      ctermbg=186 guibg=#dfdf87 cterm=none gui=none
   101	hi diffDelete   ctermfg=bg  guifg=bg      ctermbg=246 guibg=#949494 cterm=none gui=none
   102	hi diffChange   ctermfg=bg  guifg=bg      ctermbg=181 guibg=#dfafaf
   103	hi diffText     ctermfg=bg  guifg=bg      ctermbg=174 guibg=#df8787 cterm=none gui=none
   104	""" HTML {{{3
   105	" hi htmlTag      ctermfg=146  guifg=#afafdf
   106	" hi htmlEndTag   ctermfg=146  guifg=#afafdf
   107	hi htmlTag      ctermfg=244
   108	hi htmlEndTag   ctermfg=244
   109	hi htmlArg	ctermfg=182  guifg=#dfafdf
   110	hi htmlValue	ctermfg=187  guifg=#dfdfaf
   111	hi htmlTitle	ctermfg=254  ctermbg=95
   112	" hi htmlArg	ctermfg=146
   113	" hi htmlTagName	ctermfg=146
   114	" hi htmlString	ctermfg=187
   115	""" XML {{{3
   116	hi link xmlTagName	Statement
   117	" hi link xmlTag		Comment
   118	" hi link xmlEndTag	Statement
   119	hi link xmlTag		xmlTagName
   120	hi link xmlEndTag	xmlTag
   121	hi link xmlAttrib	Identifier
   122	""" django {{{3
   123	hi djangoVarBlock ctermfg=180  guifg=#dfaf87
   124	hi djangoTagBlock ctermfg=150  guifg=#afdf87
   125	hi djangoStatement ctermfg=146  guifg=#afafdf
   126	hi djangoFilter ctermfg=174  guifg=#df8787
   127	""" python {{{3
   128	hi pythonExceptions ctermfg=174
   129	""" NERDTree {{{3
   130	hi Directory      ctermfg=110  guifg=#87afdf
   131	hi treeCWD        ctermfg=180  guifg=#dfaf87
   132	hi treeClosable   ctermfg=174  guifg=#df8787
   133	hi treeOpenable   ctermfg=150  guifg=#afdf87
   134	hi treePart       ctermfg=244  guifg=#808080
   135	hi treeDirSlash   ctermfg=244  guifg=#808080
   136	hi treeLink       ctermfg=182  guifg=#dfafdf
   137	""" rst #{{{3
   138	hi link rstEmphasis Number
   139	
   140	""" VimDebug {{{3
   141	" FIXME
   142	" you may want to set SignColumn highlight in your .vimrc
   143	" :help sign
   144	" :help SignColumn
   145	
   146	" hi currentLine term=reverse cterm=reverse gui=reverse
   147	" hi breakPoint  term=NONE    cterm=NONE    gui=NONE
   148	" hi empty       term=NONE    cterm=NONE    gui=NONE
   149	
   150	" sign define currentLine linehl=currentLine
   151	" sign define breakPoint  linehl=breakPoint  text=>>
   152	" sign define both        linehl=currentLine text=>>
   153	" sign define empty       linehl=empty
   154	""" vimHelp {{{3
   155	hi link helpExample Number
   156	hi link helpNumber String
   157	hi helpURL ctermfg=110 guifg=#87afdf                           cterm=underline gui=underline
   158	hi link helpHyperTextEntry helpURL
{% endraw %}
```

You can see on lines 42-44 above, I have replaced the `hi CursorLineNr` command.  In Vim script double quotes 
are comments.  So I commented out the old command and copied the same command with a new argument.  When
you try to go back in time and see what you changed, this might help you.  In the `CursorLine` value I set 
the foreground color to grey.  This shows up nicely against the dark grey of xoria256 without being distracting.
To remove the underline from the line number, I need to define a background and foreground color for the 
`CursorLineNr` value.  I chose a background of magenta with a foreground of white.  It looks pretty good.  
The important thing is that it doesn't distract me, either with too much color or too little, and I can find
my cusor on a large display without going hunting.  

Note that the color choices must be from the normal 8-bit color choices you have available in your terminal.

## Conclusion

Find your color theme file from your callout in your `.vimrc`.  Edit that file (the color file) to define your `hi CursorLine` 
and `hi CursorLineNr` values.  Define your `cterm` values for `CursorLine` and your `ctermfg` and `ctermbg` 
values for your `hi CursorLineNr` lines.  Then close and reopen vim.  That should do it!  Voila!  Annoying
underline is now removed and replaced with a nice color combo of your chosing.
