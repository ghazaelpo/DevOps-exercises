# Linux Operating System

---

# Learning some basic commands in Linux 👨🏻‍💻

### Following we have some of the most common and basic commands to use

### Working with files and directories 📁

```bash
# echo command
echo - display a line of text
	#Description. Echo the STRING(s) to standard output.
	#It is common use this command to print on terminal.
# Just type echo followed by some text between "here"
root@8f7ef6252884:/# echo "My name is Genaro Hazael Ovalle"
My name is Genaro Hazael Ovalle

# pwd command
pwd - print name of current/working directory
	#Description. Print the full filename of the current working directory.
# If you want to know your current directory just type pwd as per below
root@8f7ef6252884:/# pwd
/

# mkdir command
mkdir - create directories
	#Description. Create the DIRECTORY(ies), if they do not already exist.
# We create a directory called example
root@8f7ef6252884:/# mkdir example

# touch command
touch - create files
	#Description. It is used to create a file without any content. 
	#The file created using touch command is empty. 
	#This command can be used when the user doesn’t have data 
	#to store at the time of file creation.
# We created two files, you can create the files one by one, in this case
# the files have been created at the same line
root@8f7ef6252884:/# touch file1 file2
# One by one
root@8f7ef6252884:/# touch file1
root@8f7ef6252884:/# touch file2

# mv command
mv - move (rename) files
	#Description. Rename SOURCE to DEST, or move SOURCE(s) to DIRECTORY.
# Move the file1 to the new directory called example
root@8f7ef6252884:/# mv file1 example/
# Rename
root@8f7ef6252884:/# mv file1 file12345

# cd command
cd - change the shell working directory
	#Description. Change the current directory to DIR. 
	#The default DIR is the value of the
  #HOME shell variable.
# If you type cd followed by a directory name, you can go into it.
# Go to example directory
root@8f7ef6252884:/# cd example/

# ls command
ls - list directory contents
	#Description. List information about the FILEs 
	#(the current directory by default).
# We need validate if file1 was move to example directory
root@8f7ef6252884:/example# ls
file1

# date command
date - print or set the system date and time
	#Description. Display the current time in the given FORMAT, 
	#or set the system date.
# We able to print the date using just the command.
root@8f7ef6252884:/# date 
Fri Sep  3 01:10:04 UTC 2021
# Even we can add this date to a file2 used previously.
root@8f7ef6252884:/# date >> file2

# cat command
cat - concatenate files and print on the standard output
	#Description. Concatenate FILE(s) to standard output.
# Use this command to bring the text from inside the file and show on the terminal.
# We will take the previous example to show you how it works and print 
# the content from file2.
root@8f7ef6252884:/# cat file2
Fri Sep  3 01:29:36 UTC 2021

# rm command 
rm - remove files or directories
	#Description. rm removes each specified file.  By default, it
  #does not remove directories.
# We are going to remove all files and directories that we created.
root@8f7ef6252884:/# cd example
root@8f7ef6252884:/example# ls
file1
# We already eliminated the file1 inside the directory.
root@8f7ef6252884:/example# rm file1 
root@8f7ef6252884:/example# ls
root@8f7ef6252884:/example#
# But if you want to delete a complete directory, I mean, even with their content
# you can use the option recursive -r
root@8f7ef6252884:/example# cd ..
root@8f7ef6252884:/# rm -r example/
	#If you want to delete a complete directory you have 
	#to do this from outside the directory. As per above.
```

### Handling text files 🗒️

```bash
#For execute this commands we will open alternatives.log file

# more command
more - file perusal filter for crt viewing
	#Description. more is a filter for paging through text one screenful at a time.
  #This version is especially primitive.  Users  should  realize  that  less(1)
  #provides more emulation plus extensive enhancements.
# If you look at the end of this log, you can see 30%, that is mean the document
# has 70% more to show. You can advance clicking enter.
root@6714b99a4bd5:/var/log# more alternatives.log
update-alternatives 2021-08-27 07:17:01: run with --install /usr/bin/w w /usr/bi
n/w.procps 50 --slave /usr/share/man/man1/w.1.gz w.1.gz /usr/share/man/man1/w.pr
ocps.1.gz
update-alternatives 2021-08-27 07:17:01: link group w updated to point to /usr/b
in/w.procps
update-alternatives 2021-08-27 07:17:02: run with --install /usr/bin/pager pager
 /bin/more 50 --slave /usr/share/man/man1/pager.1.gz pager.1.gz /usr/share/man/m
an1/more.1.gz
update-alternatives 2021-08-27 07:17:02: link group pager updated to point to /b
in/more
--More--(30%)

# less command
less - opposite of more
	#Description. Less is a program similar to more, 
	#but it has many  more  features.
  #Less  does  not  have to read the entire input file before starting, so
  #with large input files it starts up faster than text  editors  like  vi.
# Allows you to navigate both forward and backward through the file.
root@6714b99a4bd5:/var/log# less alternatives.log
update-alternatives 2021-08-27 07:16:56: 
run with --quiet --install /usr/bin/awk awk /usr/bin/mawk 5 
--slave /usr/share/man/man1/awk.1.gz awk.1.gz /usr/share/man/man1/mawk.1.gz 
--slave /usr/bin/nawk nawk /usr/bin/mawk --slave /usr/share/man/man1/nawk.1
.gz nawk.1.gz /usr/share/man/man1/mawk.1.gz
update-alternatives 2021-08-27 07:16:56: 
link group awk updated to point to /usr/bin/mawk
update-alternatives 2021-08-27 07:17:00: 
run with --quiet --install /usr/bin/awk awk /usr/bin/mawk 5 --slave 
/usr/share/man/man1/awk.1.gz awk.1.gz /usr/share/man/man1/mawk.1.gz 
--slave /usr/bin/nawk nawk /usr/bin/mawk --slave 
run with --install /usr/bin/w w /usr/bin/w.procps 50 
--slave /usr/share/man/man1/w.1.gz w.1.gz /usr/share/man/man1/w.procps.1.gz
update-alternatives 2021-08-27 07:17:01: link group w updated to 
point to /usr/balternatives.log

# tail command
tail - output the last part of files
	#Description. Print  the  last  10  lines of each FILE to standard output.  
	#With more than one FILE, precede each with a header giving the file name.
# Just show you the last part of the file 
root@6714b99a4bd5:/var/log# tail alternatives.log 
update-alternatives 2021-09-03 03:46:54: run with --remove pager /usr/bin/pg
update-alternatives 2021-09-03 03:46:57: run with --install /usr/bin/w w /usr/bin/w.procps 50 --slave /usr/share/man/man1/w.1.gz w.1.gz /usr/share/man/man1/w.procps.1.gz
update-alternatives 2021-09-03 03:46:57: auto-repair link group w
update-alternatives 2021-09-03 03:51:22: run with --install /usr/bin/write write /usr/bin/bsd-write 100 --slave /usr/share/man/man1/write.1.gz write.1.gz /usr/share/man/man1/bsd-write.1.gz
update-alternatives 2021-09-03 03:51:22: link group write updated to point to /usr/bin/bsd-write
update-alternatives 2021-09-03 03:51:22: run with --install /usr/bin/from from /usr/bin/bsd-from 10 --slave /usr/share/man/man1/from.1.gz from.1.gz /usr/share/man/man1/bsd-from.1.gz
update-alternatives 2021-09-03 03:51:22: link group from updated to point to /usr/bin/bsd-from
update-alternatives 2021-09-03 05:12:37: run with --quiet --install /usr/bin/pager pager /usr/bin/less 77 --slave /usr/share/man/man1/pager.1.gz pager.1.gz /usr/share/man/man1/less.1.gz
update-alternatives 2021-09-03 05:12:37: link group pager updated to point to /usr/bin/less
update-alternatives 2021-09-03 05:12:37: run with --quiet --remove pager /bin/less

# head command
head - output the first part of files
	#Description. Print  the  first  10 lines of each FILE to standard output.  
	#With more than one FILE, precede each with a header giving the file name.
# Just show the first part of files
root@6714b99a4bd5:/var/log# man head
root@6714b99a4bd5:/var/log# head alternatives.log 
update-alternatives 2021-08-27 07:16:56: run with --quiet --install /usr/bin/awk awk /usr/bin/mawk 5 --slave /usr/share/man/man1/awk.1.gz awk.1.gz /usr/share/man/man1/mawk.1.gz --slave /usr/bin/nawk nawk /usr/bin/mawk --slave /usr/share/man/man1/nawk.1.gz nawk.1.gz /usr/share/man/man1/mawk.1.gz
update-alternatives 2021-08-27 07:16:56: link group awk updated to point to /usr/bin/mawk
update-alternatives 2021-08-27 07:17:00: run with --quiet --install /usr/bin/awk awk /usr/bin/mawk 5 --slave /usr/share/man/man1/awk.1.gz awk.1.gz /usr/share/man/man1/mawk.1.gz --slave /usr/bin/nawk nawk /usr/bin/mawk --slave /usr/share/man/man1/nawk.1.gz nawk.1.gz /usr/share/man/man1/mawk.1.gz
update-alternatives 2021-08-27 07:17:01: run with --install /usr/share/man/man7/builtins.7.gz builtins.7.gz /usr/share/man/man7/bash-builtins.7.gz 10
update-alternatives 2021-08-27 07:17:01: link group builtins.7.gz updated to point to /usr/share/man/man7/bash-builtins.7.gz
update-alternatives 2021-08-27 07:17:01: run with --install /usr/sbin/rmt rmt /usr/sbin/rmt-tar 50 --slave /usr/share/man/man8/rmt.8.gz rmt.8.gz /usr/share/man/man8/rmt-tar.8.gz
update-alternatives 2021-08-27 07:17:01: link group rmt updated to point to /usr/sbin/rmt-tar
update-alternatives 2021-08-27 07:17:01: run with --install /usr/bin/w w /usr/bin/w.procps 50 --slave /usr/share/man/man1/w.1.gz w.1.gz /usr/share/man/man1/w.procps.1.gz
update-alternatives 2021-08-27 07:17:01: link group w updated to point to /usr/bin/w.procps
update-alternatives 2021-08-27 07:17:02: run with --install /usr/bin/pager pager /bin/more 50 --slave /usr/share/man/man1/pager.1.gz pager.1.gz /usr/share/man/man1/more.1.gz
```

### Useful commands 🤯 🔥

If you want to know the disk space usage you can use `df` command and for human readable `df -h`

```bash
# df command
df - report file system disk space usage
root@8f7ef6252884:/# df -h
Filesystem      Size  Used Avail Use% Mounted on
overlay          59G  2.6G   53G   5% /
tmpfs            64M     0   64M   0% /dev
tmpfs           993M     0  993M   0% /sys/fs/cgroup
shm              64M     0   64M   0% /dev/shm
/dev/vda1        59G  2.6G   53G   5% /etc/hosts
tmpfs           993M     0  993M   0% /proc/acpi
tmpfs           993M     0  993M   0% /sys/firmware
```

---

`exit` command allow you to quit the terminal and close it. In the below example we can see how the linux username change to mac username, this mean that we are logged out from linux image. 

```bash
root@de5544c7154d:/usr/games# exit
exit
genaroparedes@GenaroParedes-MacBook-Pro ~ %
```

---

`clear` command is use to clean up all the text and characters from the terminal.

```bash
root@72201615da76:/# ls
bin   dev  home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  etc  lib   lib64  media   opt  root  sbin  sys  usr
root@72201615da76:/# clear
root@72201615da76:/#
```

---

`man` command is the system's manual pager. You can get the description for an specific command.

```bash
NAME
       man - an interface to the system reference manuals

SYNOPSIS
       man [man options] [[section] page ...] ...
       man -k [apropos options] regexp ...
       man -K [man options] [section] term ...
       man -f [whatis options] page ...
       man -l [man options] file ...
       man -w|-W [man options] page ...

DESCRIPTION
       man  is  the system's manual pager.  Each page argument given to man is
       normally the name of a program, utility or function.
```

---

`uname` print system information. With no OPTION, same as -s.

```bash
root@6714b99a4bd5:/# uname 
Linux
root@6714b99a4bd5:/# uname -s
Linux
# Print the Kernel release.
root@6714b99a4bd5:/# uname -r
5.10.47-linuxkit
# output version information and exit.
root@6714b99a4bd5:/# uname --version
uname (GNU coreutils) 8.30
Copyright (C) 2018 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Written by David MacKenzie.
```

---

`uptime` tell how long the system has been running. 

```bash
root@6714b99a4bd5:/# uptime
 04:30:53 up  9:23,  0 users,  load average: 0.00, 0.00, 0.00
```

---

`last login` show a listing of last logged in users.

```bash
root@6714b99a4bd5:/# last login

wtmp begins Thu Sep  2 18:25:21 2021
```

---

`history` display or manipulate the history list.

```bash
root@6714b99a4bd5:/# history  
    1  uname
    2  man uname 
    3  unminimize
    4  apt install man-db
    5  name less
    6  man less
    7  man uname
    8  uname 
    9  uname -s
   10  uname -r
   11  uname --version
   12  clock
   13  hwclock
   14  hwclock --verbose
   15  apt install clock
   16  uptime
   17  man uptime
   18  uptime
   19  last login
   20  man last login
   21  last
   22  last login
   23  man last login
   24  lastb
   25  last login
   26  man last 
   27  last login
   28  man history
   29  history --help
   30  history 
```

---

```bash
# Adding -h option to enable human readable.
root@6714b99a4bd5:/var/log# du -h
84K	./apt
400K	.
# Write counts for all files, not just directories.
root@6714b99a4bd5:/var/log# du -a
204	./dpkg.log
8	./alternatives.log
24	./apt/history.log
8	./apt/eipp.log.xz
44	./apt/term.log
84	./apt
32	./lastlog
60	./bootstrap.log
0	./btmp
0	./wtmp
4	./faillog
400	.
```

---

`lspci` list all PCI devices. It is a utility for displaying information about PCI buses in the system and devices connected to them.

```bash
ecee@embedded-vm:~$ lspci
00:00.0 Host bridge: Intel Corporation 440FX - 82441FX PMC [Natoma] (rev 02)
00:01.0 ISA bridge: Intel Corporation 82371SB PIIX3 ISA [Natoma/Triton II]
00:01.1 IDE interface: Intel Corporation 82371AB/EB/MB PIIX4 IDE (rev 01)
00:02.0 VGA compatible controller: VMware SVGA II Adapter
00:03.0 Ethernet controller: Intel Corporation 82540EM Gigabit Ethernet Controller (rev 02)
00:04.0 System peripheral: InnoTek Systemberatung GmbH VirtualBox Guest Service
00:05.0 Multimedia audio controller: Intel Corporation 82801AA AC'97 
Audio Controller (rev 01)
00:06.0 USB controller: Apple Inc. KeyLargo/Intrepid USB
00:07.0 Bridge: Intel Corporation 82371AB/EB/MB PIIX4 ACPI (rev 08)
00:0d.0 SATA controller: Intel Corporation 82801HM/HEM (ICH8M/ICH8M-E) 
SATA Controller [AHCI mode] (rev 02)
```

---

`file` determine the file type

```bash
ecee@embedded-vm:~$ file new2.txt 
new2.txt: ASCII text
```

---

`reboot` or `poweroff` may be used to power-off or reboot the machine

`blkid` locate/print block device attributes

`eject` eject removable media

---