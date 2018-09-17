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

#### file

To see a file's format, use `file file`

Ex : 
```
$ file ReadMe.md 
ReadMe.md: UTF-8 Unicode text
```

#### find and locate

Find a file in a folder : `find dir -name file -print`

Ex : find all Java files in the current directory : ```find . -name *.java -print```

Most systems also have a _locate_ command for finding files. Rather than searching for a file in real time, _locate_ searches an index that the system builds periodically. Searching with locate is much faster than _find_, but if the file you’re looking for is newer than the index, _locate_ won’t find it.

#### head and tail

- _head_ : first 10 lines (can be changed with _-n_ option)
- _tail_ : last 10 lines (can be changed with _-n_ option)

#### dot files

dot files can be shown by `ls -a` command.

### Shell input and output

To send the output of _command_ to a file instead of the terminal, use the *>* redirection character :

```
$ echo "this is a text from shell prompt" > text.txt
```
It creates the file if it does not exist or erase the old content otherwise.
To append to an existing file , use `>>`


#### Standard Error 

```
ls /fffffff > f
```

f will be empty file and error message is printed on the shell.

Redirect the standard error : `ls /fffffff > f 2> e`

Standard output to *f*, and standard error to *e*

You can also send the standard error to the same place as stdout with the `>&` notation. 
For example, to send both stdout and standard error to _f_ , try this command :
```
ls /ffffff > f 2>&1
``` 

#### Listing and manipulating processes

 command  | explanation
 -----|----------------
 ps x | show all of your running processes
 ps ax| show all processes on the system, not just the ones you own.
 ps u | include more detailed information on processes.

To inspect the current shell process, use :
```
ps aux $$
```
because $$ is a shell variable that evaluates to the current shell's PID.


#### Killing processes

```
$ kill pid
```
When you run _kill_, you are asking the kernel to send a signal to another process.
The default signal is TERM or terminate.

To freeze a process instead of terminating it, use the STOP signal : `$ kill -STOP pid`

Use the CONT signal to continue running the process again : `$ kill -CONT pid`

The most brutal way to terminate a process is with the KILL signal. Other signals give the process a chance to clean up after itself, but KILL does not.

Users may enter numbers instead of name with _kill_ : `kill -9` instead of `kill -KILL` because the kernel uses numbers to denote the different signals.

#### Modifying permissions

`chmod 755 filename` permissions are usually translated into textual representation of `rwxr-xr-x`. So we have the bit sequence for permission is read-write-execute -> 7 = 111 -> rwx, 5 : 101 -> r-x
(This is called an absolute change because it sets all permission bits at once.)

Directories also have permissions. You can list the contents of a directory if it’s readable, but you can only access a file in a directory if the directory is executable. 

You can specify a set of default permissions with the _umask_ shell command, which applies a predefined set of permissions to any new file you create.

#### Symbolic links 

```
$ ln -s target linkname
```

### Archiving and Compressing Files

#### gzip
gzip (GNU Zip) is one of the current standard Unix compression programs. A file that ends with .gz is a GNU Zip archive.
Use gunzip file.gz to uncompress &lt;file&gt;.gz

#### tar
Unlike the zip programs for other operating systems, _gzip_ does not create archives of files: it does not pack multiple files and directories into one files. To create an archive, use _tar_ instead : 
```
$ tar cvf archive.tar file1 file2 ...
```

Unpacking tar file :

```
$ tar xvf archive.tar
```
### Compressed Archives (.tar.gz)

To unpack a compressed archive file, work from the right side to the left; get rid of the _.gz_ first and then worry about the _.tar_

```
gunzip file.tar.gz
tar xvf file.tar
```

#### zcat
This command pipeline unpacks _file.tar.gz_ :

```
$ zcat file.tar.gz | tar xvf -
```

In `tar` you can use z as an option to automatically invoke gzip on the archive; this works both for extracting an archive (with the _x_ or _t_ modes in _tar_) and creating one (with _c_).

```
$ tar ztvf file.tar.gz
``` 

- _bzip2_ , another compression program in Unix, create compressed files ending with _.bz2_ 
- _bzip2_ is slightly slower than _gzip_ but compacts text files a little more, so it is increasingly popular in the distribution of source code. The decompressing program to use is _bunzip2_ and the options of both components are close enough to those of _gzip_


### Linux directory hierarchy 

The most important subdirectories in root :

- **/bin** contains ready-to-run programs (such as: _ls_ and _cp_ )
- **/dev** contains device files
- **/etc** is the core system configuration directory containing the user password, boot, device, networking, and other setup files.
- **/home** holds personal directories for regular users.
- **/lib** abbr for library, holding library files containing code that executables can use. There are 2 types of libraries : static and shared. The _/lib_ dir should contain only shared libraries, but other lib directories, such as _/usr/lib_ contains both varieties as well as other files.
- **/proc** provides system statistics
- **/sbin** place for system executables. Programs in _/sbin_ directories relate to system management, so regular user usually do not have _/sbin_ components in their command path.
- **/tmp** a storage area for smaller, temporary files you don't care much about. Many programs use this directory as a workspace. Most distributions clear _/tmp_ when the machine boots and some even remove its old files periodically.
- **/usr** this subdirectory has no user files. Instead, it contains a large directory hierarchy, including the bulk of the Linux system.
- **/var** the variable subdirectory, where programs record runtime information. System logging, user tracking, caches and other files that system programs create and manage are here.

#### Other root subdirs

- **/boot** : kernel boot loader files. These files pertain only to the very first stage of the Linux startup procedure.
- **/opt** : may contain additional third-party software.

### Running commands as the Superuser

#### sudo
```
$ sudo vipw
```
#### /etc/sudoers

this file gives user1 and user2 the power to run any command as root without having to enter a password:

```
User_Alias ADMINS = user1, user2

ADMINS  ALL = NOPASSWD: ALL

root    ALL=(ALL) ALL
```
Use the **visudo** command to edit _/etc/sudoers_. This command checks for file syntax errors after you save the file.








































































































