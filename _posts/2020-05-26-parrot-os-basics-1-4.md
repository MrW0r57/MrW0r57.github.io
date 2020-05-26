---
layout: post
published: false
title: Parrot OS basics 1.4
---
## Environmental variable in bash

In this blog post we wil discuss linux shell and environmental variables in bash. 

## What is Linux Shell ?

Shell is an environment in which we can run our commands, programs, and shell scripts. There are different flavors of a shell, just as there are different flavors of operating systems. Each flavor of shell has its own set of recognized commands and functions.

**Types of shell**

There are basically two types of shells in linux

1. Bourne Shell

2. C shell


**The Bourne Shell has the following subcategories −**

- 	  Bourne shell (sh)

-     Korn shell (ksh)

-     Bourne Again shell (bash)

-     POSIX shell (sh)

**The  C-Shell Sub cataogories −**

- C shell (csh)

- TENEX/TOPS C shell (tcsh)


In Parrot, we use bash shell usually, you can chheck it using 'echo $SHELL' command.


Now we will talk about Environmental variables, how to list them ?, how set them ?


**Variables have the following format:**


   KEY=value
   
   KEY="Some other value"
   
   KEY=value1:value2


**Environment variables are variables that are available system-wide and are inherited by all spawned child processes and shells.**


Shell variables are variables that apply only to the current shell instance. Each shell such as zsh and bash, has its own set of internal shell variables.

**Commands that allow to set and list environmental variables :**

- env - To run a program in a modified environment without modifying current one. To list all current environment use single 'env'.

- printenv - print all or part of environment.

- set - to set an environmental variable and shell.When used without an argument it will print a list of all variables including environment and shell variables, and shell functions.

- unset - to unset an environmental variable shell.

- export - to set environmental variable.


**To display the value of the HOME environment variable**
~~~
$ printenv HOME
~~~

To display multiple values

~~~
$ printenv LANG PWD
~~~

**Common environmental variables**

- 	  USER - display current logged in user.

-     HOME - display home directory of the current user.

-     EDITOR - display default file editor to be used. This is the editor that will be used when you type edit in your terminal.

-     SHELL - display path of the current user’s shell, such as bash or zsh.

-     LOGNAME - display name of the current user.

-     PATH - display list of directories to be searched when executing commands. When you run a command the system will search those directories in this order and use the first found executable.

-     LANG - display current locales settings.

-     TERM - displau current terminal emulation.

-     MAIL - display location of where the current user’s mail is stored.

**To display all variable values**

~~~
$ echo $USER (or any variable)
~~~
or 
~~~
$printenv USER
~~~
To set variable 

$ export PATH="$HOME/bin:$PATH/"

## Conclusion

_**Try yourself and check the value of variables using echo.**_

