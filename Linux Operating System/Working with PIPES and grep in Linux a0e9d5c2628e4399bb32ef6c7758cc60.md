# Working with PIPES and grep in Linux

## What is a pipe and how does it work?

A pipe is a form of redirection (transfer of standard output to some other destination) that is used in Linux and other Unix-like operating systems to send the output of one command/program/process to another command/program/process for further processing. The Unix/Linux systems allow stdout of a command to be connected to stdin of another command. You can make it do so by using the pipe character **‘|’**.

Pipe is used to combine two or more commands, and in this, the output of one command acts as input to another command, and this command’s output may act as input to the next command and so on. 

## Explain how grep works and present an example

Grep is an essential Linux and Unix command. It is used to search text and strings in a given file. In other words, grep command searches the given file for lines containing a match to the given strings or words. It is one of the most useful commands on Linux.

```bash
#Searchin apple word on passwd file
genaroparedes@GenaroParedes-MacBook-Pro /etc % grep "apple" passwd
_appleevents:*:55:55:AppleEvents Daemon:/var/empty:/usr/bin/false
_applepay:*:260:260:applepay Account:/var/db/applepay:/usr/bin/false
#You can search any word on any file that whatever you want
```

## Explain how egrep works and present an example

The egrep command enables usage of extended regexp patterns. This allows use of meta-symbols such as `+`, `?` or `|`. These aren't ordinary characters like we may use in words or filenames but are control commands for the `grep` binary itself. Thus, with `egrep`, the character `|` means logical OR.

```bash
#In this example the command found chains with apple or www words
genaroparedes@GenaroParedes-MacBook-Pro /etc % egrep "apple|www" passwd
_appleevents:*:55:55:AppleEvents Daemon:/var/empty:/usr/bin/false
_www:*:70:70:World Wide Web Server:/Library/WebServer:/usr/bin/false
_wwwproxy:*:252:252:WWW Proxy:/var/empty:/usr/bin/false
_applepay:*:260:260:applepay Account:/var/db/applepay:/usr/bin/false
```

## Present an example where you combine a pipe with grep and other command

```bash
#You can search a specific word in a specific file
#In this example we are lookig into passwd file and searching root word
genaroparedes@GenaroParedes-MacBook-Pro /etc % cat passwd | grep "root"       
root:*:0:0:System Administrator:/var/root:/bin/sh
daemon:*:1:1:System Services:/var/root:/usr/bin/false
_cvmsroot:*:212:212:CVMS Root:/var/empty:/usr/bin/false
```

## Present an example where you combine a pipe with egrep and other command

```bash
#In this case we used cat to show the passwd text file and then
#search root or apple words
genaroparedes@GenaroParedes-MacBook-Pro /etc % cat passwd | egrep "root|apple"  
root:*:0:0:System Administrator:/var/root:/bin/sh
daemon:*:1:1:System Services:/var/root:/usr/bin/false
_appleevents:*:55:55:AppleEvents Daemon:/var/empty:/usr/bin/false
_cvmsroot:*:212:212:CVMS Root:/var/empty:/usr/bin/false
_applepay:*:260:260:applepay Account:/var/db/applepay:
```