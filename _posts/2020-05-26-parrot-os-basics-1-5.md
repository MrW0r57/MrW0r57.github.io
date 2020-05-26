---
layout: post
published: false
title: Parrot OS Basics 1.5
---
## Some Tricks and Tips

In this blog post we will learn the tricky usage of some commands and utilities.

**cat command**

To add text and make a file


$ cat  > filname.py or filename.txt or filename.c 


To append text in a file


$ cat >> filename.java or filename.sh .


To number line in output


$ cat -n filename.txt


**alias command**

~~~
$ alias (to list all alias)
~~~

To set alias

$ alias hi='echo "hi hacker" '


Now write hi on terminal and press enter, it will show

~~~
$ hi
hi hacker
~~~

Now another command


$ alias scanme='nmap -sS -p- localhost'


Run scanme and you will nmap scan result for your system

$ scanme

$ alias scanmehard='nmap -A -p- localhost'

you can set multiple alias like this

To permanently add them in to your profile, you just need to append above commands in .bashrc, like below.

$ nano ~/.bashrc

append above line at the end of the file and relaunch terminal.


Use shopt -s cdspell to autmatically correct your typos

$ shopt -s cdspell
$ cd /hme            
try this it will cd to home

**grep command**

print lines that match patterns


example :

 $ grep root /etc/passwd


Option -v, will display all the lines except the match

$ grep -v root /etc/passwd

count lines match

$ grep -c root /etc/passwd

count lines doesn't match

$ grep -cv root /etc/passwd

search ignoring case

$ grep -i root /etc/passwd

**find command**


Search for files in a directory hierarchy

Syntax: find [pathnames] [conditions]

find files containing a specific word in its name

 find /home -name "*hacker*"

find all the files greater than certain size

 find / -type f -size +500M

**sort, uniq, diff, fmt commands**


sort - sort lines of text files
~~~
$ sort filename.txt
~~~
fmt - format unformated file
~~~
$ fmt hacker.txt
~~~
uniq - omit repeated lines

~~~
$ uniq hackerrepeat.txt
~~~

diff - compare files line by line and report the difference
~~~
$ diff [options] file1 file2
~~~
awk command

Awk is a programming language which allows easy manipulation of structured data and the generation of formatted reports.
 
 Basic Syntax
 
$ awk '/search pattern1/ {Actions}
/search pattern2/ {Actions}' file


Print the lines which matches with the pattern.

$ awk '/hacker/
> /hactivist/' badactors.txt


Initialization and Final Action
Awk has two important patterns which are specified by the keyword called BEGIN and END.


$ awk 'BEGIN {print
"Name\tcrime\tplace\tmoney";}
> {print $2,"\t",$3,"\t",$4,"\t",$NF;}
> END{print "Report Generated\n--------------";
> }' badactors.txt

wget and curl commands
----------------------------------
you can download files using wget and curl from internet

example

$ wget https://github.io/tools.git
# curl https://github.io/tools.git

I/O Redirection
--------------------------------------

Input and output in the Linux environment is distributed across three streams

    stdin (0)

    stdout (1)

    stderr (2)

Commands with a single bracket overwrite the destination’s existing contents.

Overwrite

    > - standard output

    < - standard input

    2> - standard error

Commands with a double bracket do not overwrite the destination’s existing contents.

Append

    >> - standard output

    << - standard input

    2>> - standard error

PIPE '|'
Pipes are used to redirect a stream from one program to another

example

$ ls /home/desktop | grep user.txt               // it will send first command input to second and display the result


filters used by pipe



    find - Find returns files with filenames that match the argument passed to find.

    grep - Grep returns text that matches the string pattern passed to grep.

    tee - Tee redirects standard input to both standard output and one or more files.

    tr - tr finds-and-replaces one string with another.

    wc - wc counts characters, lines, and words.


These are very useful command tricks of linux, use them.


