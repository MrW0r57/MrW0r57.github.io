---
layout: post
published: true
title: Windows Basics 3.1
tags:
  - PWP
  - Beginner
  - Windows Basics
comments: true
---
## Windows directory, Registry and basic commands

## Introductiom

_**In this blog post we will learn windows system and basic commands and how to navigate and interact with them using windows command terminal.**_

I hope everyone is familiar with windiows and how to use it using GUI, now we will also learn its command line usage.

Windows highest directory or root directory is specified as drive:\ but usualy its c:\, '\' is the directory seperator in windows link '/' in linux but we can use both in windowa command line

_**Following are the useful directories of windows root directory:**_

- **\perflogs:** May hold Windows performance logs, but on a default configuration, it is empty.

- **\Program Files:** All programs are installed in this folder based on system architecture(x86\x64).

- **\Program Files (x86):** In 64 bit architecture all 32 bit program are installed in this folder.

- **\Users:** This folder contains one subfolder for each user that has logged onto the system at least once

- **\Public:** This folder serves as a buffer for users of a computer to share files. By default this folder is accessible to all users that can log on to the computer.
   
- **\System, \System32, \SysWOW64:** These folders store dynamic-link library (DLL) files that implement the core features of Windows and Windows API. Any time a program asks Windows to load a DLL file and do not specify a path, these folders are searched after program's own folder is searched.



## Windows Registry

The Registry is a database sed to store settings and options for the windows systems.
It contains information and settings for all the hardware, software, users, and preferences of the PC. Whenever a user makes changes to a Control Panel settings, or File Associations, System Policies, or installed software, the changes are reflected and stored in the Registry.

[click here to know more about registry](https://www.akadia.com/services/windows_registry_tutorial.html)

## Windows basic navigation commands

**cd/chdir:** change directory.

**copy:** This command copies a specified file to a given location.

**del/erase:** deletes a file or number of files.

**dir:** this displays the current files and folder directly accessible from either the current directory, or the directory specified after the command.

**find:** searches a specific file for a given string. ex find “hacker” hacker.txt

**md/mkdir:** This command creates a new directory.

**move:** Move is basically a copy/paste command that move a file from one location to another.

**popd/pushd:** Allows the user to quickly switch between file paths.

**ren/rename:** This command is used to rename directories. 

**rd/rmdir:** This allows the user to remove a directory.

**start:** Allows the user to start a program (so long as the program is an executable, batch or command file).

**tree:** Displays a graphical file tree of the the specified file path, or the current drive if no path is specified.

**more/type:** To view file as a text in commandline, we can also use it to edit or append text like cat. ex. more > hacker.txt, more >> hacker.txt, type > hacker.txt, type >> hacker.txt.


For more windows commands (click me)[https://ss64.com/nt/]

## Conclusion

_**We should learn some windows basic commands, in future we have to interact with windows command line also.**_
