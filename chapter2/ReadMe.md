#### The Bourne Shell : /bin/sh
A _shell_ is a program that runs commands, like the ones that users enter.

_shell scripts_ : text files that contain a sequence of shell commands, just as powerful as .BAT files in MS-DOS.

There are many different Unix shells, but all derive several of their features from the Bourne shell (_/bin/sh_),
a standard shell developed at Bell Labs for early versions of Unix. Every Unix system needs the Bourne shell in order to function correctly.

Linux uses and enhanced version of the Bourne shell called _bash_ or the "Bourne-again" shell.

The *bash* shell is the default shell on most Linux distributions, and _/bin/sh_ is normally a link to *bash* on a Linux system.

### Using the shell

#### cat

```
$ cat file1 file2 ...
```
The command is called `cat` because it performs concatenation when it prints the contents of more than one file.

#### cp

copy multiple files into a folder 
```
$ cp file1 ... fileN dir
```

#### touch

The _touch_ command creates a file. If the file already exists, touch does not change it, but it does update the file’s modification time stamp printed with the `ls -l` command. 

#### rmdir

```
$ rmdir dir
```
If `dir` isn’t empty, this command fails.

```
rm -rf dir
```
does the work but please be careful.

#### Shell globbing

The shell can match simple patterns to file and directory names, a process known as _globbing_.

The shell matches arguments containing globs to filenames, substitutes the filenames for those arguments, and then runs the revised command line. The substitution is called expansion because the shell substitutes all matching filenames. 

If you don’t want the shell to expand a glob in a command, enclose the glob in single quotes (''). For example, the command `echo '*'` prints a star. 


### Intermediate commands 

#### grep
prints the line from a file or input stream that match an expression.
```
$ grep root /etc/passwd
```
prints the lines in the `/etc/passwd` file that contain the text *root*

Two of the most important grep options are -i (for case-insensitive matches) and -v (which inverts the search, that is, prints all lines that don’t match). 

to check every file in `/etc` that contains the word *root*, you could use this command: `$ grep root /etc/*`

#### less
The less command comes in handy when a file is really big or when a command’s output is long and scrolls off the top of the screen.

The _less_ command is an enhanced version of an older program named more. Most Linux desktops and servers have _less_, but it’s not standard on many embedded systems and other Unix systems. So if you ever run into a situation when you can’t use _less_, try _more_.

You can also search for text inside _less_. For example, to search forward for a word, type `/word`, and to search backward, use _?word_. When you find a match, press _n_ to continue searching.

Send output of nearly any program directly to another program's standard input:
```
$ grep ie /usr/share/dict/words | less
```

























