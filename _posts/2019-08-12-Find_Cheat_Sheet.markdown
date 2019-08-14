---
layout: post
title: Find Cheat Sheet
date: 2019-08-12 11:15:50-04:00
categories: Linux cli_utilities
---

## *Find* Cheat Sheet

Find is one of those under-used powertools in Linux/UNIX that will save you lots of time if you only learn
how to use it.  It's tremendously powerful and helpful.  

# The Main Idea

Find files (everything is a file in UNIX) that meet criteria and then do something with them (or not--just 
looking at them is doing something with them too).

```
find . -type f -iname "*jazz*.mp3" -exec mv "s/ /_/g" {} +
```

The above command will find all mp3 files with 'jazz' in the title and remove spaces from their filenames.  It
will work on 20 files or 2000 files.  If you tried to do this with your file manager, this could take
forever.  But this little one-liner would do it instantly.

# Basic Syntax

```
find _pathspec_ argument . . . command {} + (or / or ;)
```

You start with the find command, then provide a place (pathname) to start searching from, and then specify 
what matches or non-matches you want the returned files to have.  Optionally, you can have each of those
returned files get a command executed on them (more than one way to do this).  The last item is to terminate the
statement with a `+` or a `/` or a `;`.

It's perfectly OK to simply find files meeting criteria without executing any commands on them.  

The pathspec `.` means recursively search the current directory structure, but you can specify `/var` or `/etc`
or whatever you want.  You can use the `-mindepth` and `-maxdepth` arguments to specify how deep you want to
search the filesystem.

You can supply more than one pathspec:  `find /var /etc -mtime 0` -- find all files in both /var and /etc that have been
modified in the last 24 hours.  (-mtime 0 means less than 1 day)

# Arguments for `find`: How can you find files?

* __name__:  `find . -name "*waldo*"` -- find all files with 'waldo' in the filename
* __iname__: (case insensitive): `find . -iname "*bogus*txt"` -- finds BOGUS.txt and bOgUs.TxT
* __type__:  `find . -type d` -- find all directories in the current directory structure
* types (c, d, s, l, p, b): files, directories, sockets, symlinks, named pipes, block file. 
* __permissions__: `find . -type f -perm 775` -- find all files with permissions of 755. _Note_: can also use
the `-perm u=rwx,g=rx,o=rx` type of syntax.
* __access__:  `find /etc -atime -3 -name "*conf*"` -- all files in /etc accessed within last 3 days named "*conf*"
* __access/modification/created times__:  `find /var/log -atime -3 -mtime -3 -ctime -3 ` -- less than 3 days ago
_Note_: Accesstime is the last time the file was read.  Modificationtime is the last time the content of the file was
changed.  Changetime is the last time the file or its metadata (such as permissions or ownership) were changed
* __min/time__:  `find /etc -cmin -10` -- find all files changed in /etc less than 10 min ago.
* __user/uname/uid__ (also nouser, nogroup): `find /opt -not -group root -type f -executable` -- find all executable files (by current user) in /opt not owned by members of root group
* __size__: `find ~/Music -size +100M` -- find all files in ~/Music larger than 100 Megabytes
* __empty__: `find ~/tmp -empty` -- find all empty files in your personal tmp directory
* __regex__: `find ~/Pictures -iregex '*self*' -ctime -100` -- find all selfies newer than 100 days in Pictures
* __readable__ (also -executable, -writeable): `find /etc -readable -type f` -- find all readable files by current user in /etc
* __newer__: `find ~ -newer ~/.bashrc -name ".bash*"` -- find bash-related config files newer than your .bashrc in your
  home directory and below.  _Note_: You can also use `-newer{acm}t` on this.  For example, to find all files modified on
  the July 4th, 2014:  
  ```
  find / -type f -newermt 2014-07-04 ! -newermt 2014-07-05
  ```
* __not__ (!): `find ~ ! -user username` -- find all files and dirs in my home file structure not owned by username. `-not`
  and `!` are the same
* __and/or__: `find / -type d -a -name 'python*'` -- find all directories below root that start with python. (-o means
  'or'). Example: `find / -type d -name 'python*' -o -name 'perl*'`

# Doing Actions on Files Found

* __delete__: `find ~/tmp -name '*.sw?*' -mtime +90 -delete ;` -- delete swap files older than 90 days
* __exec__: `find ~/Music -type f -exec rename -f 'y/A-Z/a-z/' {} +` -- rename all music files to have lowercase names
_Note_: The difference between ending with '+' and ';' is that the '+' adds all the files as arguments at once and ';' adds
each file found and executes the command on _each_ file sequentially.  Example: `find ~ type f -name '*jazz*.mp3' -exec tar -czf
jazz.tar.gz {} +` will add all mp3 jazz files into a jazz tarball, while `;` will overwrite the tarball each time with each
single mp3 file.  Very different results, so you probably mean to do the '+' rather than the ';' here.
* __xargs__: `find . -type f -name "*deleteme*" | xargs rm {} +` -- delete all files with 'deleteme' in name. _Note_: you
  need a pipe ('|') with xargs.
* __execdir__: Executes the command on the directory the file found exists in. Not sure to use this myself
* __ls__: `find / -type f -size +1G -ls` -- Simply lists files largers than 1G so you can view details about the file
* __print__: `find /opt -type f -executable -print` -- Show all executable files beneath /opt.  _Note_: Sometimes special 
characters in filenames could cause the terminal some grief.  If the output is going to a terminal rather than a file, you
may want to choose a formated output, using `-fprint` or `-fprintf`.  If you want to disregard any side effects to the
terminal and print characters regardless of the terminal, you could use `-print0` or `-fprint0`.  Read the manpage for more
information on this.

# Error Messages

You may or may not want to remove them.  For example, if you are not interested in permissions limitations in your output,
you could use `find /var/log -name "*log*" -type f 2>/dev/null`, which will throw away all errors related to files you don't have
permissions to see.

# Creation Dates

Finding files by creation dates is next to impossible to do.  In fact, I would say it's a happy accident when you do.  But
you can check for files that are newer or not newer than a specific file.  For example, if you know the `/etc/mtab` file
has not changed since the OS was installed, then you could use that as a reference for comparison for a creation date.  But
would you actually know that the file has not been altered?  Or should not have been?  This is one of the sticky areas of
find.  I usually just say you can't find files based on creation dates, but only by when it was last changed/modified or
accessed.

# Combining Arguments

I touched on `-a` and `-o` above, but you can get creative on how you group the commands by using '(' and ')'.  Also, you
usually don't have to use `-a` because it's oftentimes implicit.  If you have 
```
find . -user 'joe' -type f
``` 
it is implicit that you want only files owned by joe.  You don't need a `-a` here.  But, let's say you wanted to see all files owned by
'joe' that were modified more than 90 days ago but not more than 100 days ago, or only those files that were modified within the last 4
days?  As the logic becomes a little more complex, the '(' and ')' can come to the rescue: 
```
find / -user 'joe' '(' -mtime +90 -a ! -mtime +100 ')' -o '(' -mtime -4 ')'
```

# Conclusion

There are so many options and so much flexibility with `find` that you can correctly infer that it's a daily staple for
systems admins everywhere.  The more you practice with it, the more indispensible you'll find it in your day to day work at
the command line.
