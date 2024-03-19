# Understanding the Process, Soft Links and Hard Links in Linux

## Describe the different types of processes (daemons, zombies, parent, child, etc.)

### **Zombie Processes**

It is a process whose execution is completed but it still has an entry in the process table. Zombie processes usually occur for child processes, as the parent process still needs to read its child’s exit status. Once this is done using the wait system call, the zombie process is eliminated from the process table. This is known as reaping the zombie process.

### **Orphan Processes**

Orphan processes are those processes that are still running even though their parent process has terminated or finished. A process can be orphaned intentionally or unintentionally.

An intentionally orphaned process runs in the background without any manual support. This is usually done to start an indefinitely running service or to complete a long-running job without user attention.

An unintentionally orphaned process is created when its parent process crashes or terminates. Unintentional orphan processes can be avoided using the process group mechanism.

### **Daemon Process**

A daemon process is a background process that is not under the direct control of the user. This process is usually started when the system is bootstrapped and it terminated with the system shut down.

Usually the parent process of the daemon process is the init process. This is because the init process usually adopts the daemon process after the parent process forks the daemon process and terminates.

### Parent and child process

A child process is a process that is created by another process(parent process), a child process is also known as the subprocess. There are two major ways of creating a child process: fork system call which is preferred in Unix like operating systems, the spawn is the preferred way in modern NT kernel of Microsoft Windows.

### Foreground process

By default, a process started by a user runs in the foreground. It takes input from the command prompt and displays output to the computer screen. If a foreground process is running, the terminal prevents initiating a new process until the existing one does not get finished.

## How can you list the different kind of processes?

- **ps command** — outputs a static view of all processes.
- **top command** — displays the real-time list of all running processes.
- **htop command** — shows the real-time result and is equipped with user-friendly features.

```bash
#ps command
genaro@genaro-VirtualBox:~$ ps 
    PID TTY          TIME CMD
   1859 pts/0    00:00:00 bash
   1895 pts/0    00:00:00 ps
#top command
genaro@genaro-VirtualBox:~$ top

top - 17:39:34 up 3 min,  1 user,  load average: 0.68, 1.07, 0.51
Tasks: 189 total,   1 running, 188 sleeping,   0 stopped,   0 zombie
%Cpu(s):  2.8 us,  2.4 sy,  0.0 ni, 94.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   1560.3 total,    276.9 free,    634.1 used,    649.3 buff/cache
MiB Swap:    448.5 total,    448.5 free,      0.0 used.    773.2 avail Mem

#htop command
```

![Untitled](Understanding%20the%20Process,%20Soft%20Links%20and%20Hard%20Lin%20494361c1dea64dc99a725be70cf8420b/Untitled.png)

## How do you kill a process gracefully? Describe all the steps

**kill Command**

The **`kill`** command is used to kill processes by name. By default, it will send a SIGTERM signal. The **`kill`** command can kill multiple processes with a single command.

```
kill <process>
```

Several options can be used with the **`kill`** command:

- **`e`**. Find an exact match for the process name.
- **`I`**. Ignore case when trying to find the process name.
- **`i`**. Ask for additional confirmation when killing the process.
- **`u`**. Only kill processes owned by a specific user.
- **`v`**. Report back on whether the process has been successfully killed.

### **Linux Signals and Process Management**

Signals are the method that Linux uses to communicate with processes running in the operating system. The three primary signals that the `kill` command uses to terminate processes are:

- 1 (SIGHUP) – Terminates interactive programs and causes daemons (background services) to re-read the configuration files the process uses.
- 9 (SIGKILL) – Forces the process to exit without performing graceful shutdown tasks.
- 15 (SIGTERM) – Allows a process to terminate gracefully, such as closing open files when finished. This is the default signal used when no number is specified when using the kill command.

### **Using the `kill` Command to Terminate a Process**

In this next example, you will use the `kill` command. Pretend for a moment that you are running a PowerShell instance, named `pwsh`, and the PID assigned is 22687. One way to terminate this process is shown below.

1. Use `pgrep pwsh` to determine the PID for the process `pwsh`, used in the `kill` command.
2. Use `kill -s TERM 22687` to terminate the `pwsh` process gracefully. The `TERM` command maps to the 15 (SIGTERM) signal and indicated using the `s` parameter of the `kill` command.
3. Use your choice of `top`, `ps`, or `pgrep` to verify the PID is no longer listed.

Shown below is an example of the above process from an Ubuntu 20.04 LTS bash terminal.

![Untitled-2021-01-26T161208.280.png](Understanding%20the%20Process,%20Soft%20Links%20and%20Hard%20Lin%20494361c1dea64dc99a725be70cf8420b/Untitled-2021-01-26T161208.280.png)

## List all the daemons running and document the steps

```bash
#Using grep to search a key word
genaro@genaro-VirtualBox:~$ systemctl | grep daemon
  accounts-daemon.service                                                                  loaded active running   Accounts Service                                                 
  acpid.service                                                                            loaded active running   ACPI event daemon                                                
  avahi-daemon.service                                                                     loaded active running   Avahi mDNS/DNS-SD Stack                                          
  cron.service                                                                             loaded active running   Regular background program processing daemon                     
  networkd-dispatcher.service                                                              loaded active running   Dispatcher daemon for systemd-networkd                           
  rtkit-daemon.service                                                                     loaded active running   RealtimeKit Scheduling Policy Service                            
  whoopsie.service                                                                         loaded active running   crash report submission daemon                                   
  avahi-daemon.socket                                                                      loaded active running   Avahi mDNS/DNS-SD Stack Activation Socket                        
  snapd.socket                                                                             loaded active running   Socket activation for snappy daemon                              
  uuidd.socket                                                                             loaded active listening UUID daemon activation socket
```

## How can you check if a daemon is enabled?

```bash
#Using systemctl status command
genaro@genaro-VirtualBox:~$ systemctl status avahi-daemon.service
● avahi-daemon.service - Avahi mDNS/DNS-SD Stack
     Loaded: loaded (/lib/systemd/system/avahi-daemon.service; enabled; vendor >
     Active: active (running) since Mon 2021-09-13 22:05:56 CDT; 7min ago
TriggeredBy: ● avahi-daemon.socket
   Main PID: 588 (avahi-daemon)
     Status: "avahi-daemon 0.7 starting up."
      Tasks: 2 (limit: 1802)
     Memory: 1.4M
     CGroup: /system.slice/avahi-daemon.service
             ├─588 avahi-daemon: running [genaro-VirtualBox.local]
             └─646 avahi-daemon: chroot helper

sep 13 22:05:58 genaro-VirtualBox avahi-daemon[588]: New relevant interface enp>
sep 13 22:05:58 genaro-VirtualBox avahi-daemon[588]: Registering new address re>
```

## Mention a few utilities to work with processes (about 4)

- Different users can be running various programs on the system at the same time.
- You can monitoring services in a real-time view using `htop` command.
- You can control directly what happens on the system.
- You can create new processes for your duties.

## Tell us what is a soft link and a hard link, also explain the difference between these two

A **symbolic** or **soft link** is an actual link to the original file, whereas a **hard link** is a mirror copy of the original file. If you delete the original file, the soft link has no value, because it points to a non-existent file.

But in the case of hard link, it is entirely opposite. Even if you delete the original file, the hard link will still has the data of the original file. Because hard link acts as a mirror copy of the original file.

## Create and delete a soft link and document the process

```bash
#Create a directory test
genaro@genaro-VirtualBox:~/Documents$ mkdir test
#Go to test and create a new file
genaro@genaro-VirtualBox:~/Documents$ cd test
genaro@genaro-VirtualBox:~/Documents/test$ echo "Welcome to DOU" > source.file
genaro@genaro-VirtualBox:~/Documents/test$ cat source.file 
Welcome to DOU
#Use ls command and indicate soft link using -s flag
genaro@genaro-VirtualBox:~/Documents/test$ ln -s source.file softlink.file
#Now compare the source file and the softlink created
genaro@genaro-VirtualBox:~/Documents/test$ cat source.file 
Welcome to DOU
genaro@genaro-VirtualBox:~/Documents/test$ cat softlink.file 
Welcome to DOU

#Now we will delete the soft link that we created
genaro@genaro-VirtualBox:~/Documents/test$ ls -l
total 4
lrwxrwxrwx 1 genaro genaro 11 sep 13 22:36 softlink.file -> source.file
-rw-rw-r-- 1 genaro genaro 15 sep 13 22:36 source.file
genaro@genaro-VirtualBox:~/Documents/test$ rm softlink.file 
genaro@genaro-VirtualBox:~/Documents/test$ ls -l
total 4
-rw-rw-r-- 1 genaro genaro 15 sep 13 22:36 source.file

```

## Create and delete a hard link and document the process

```bash
#We will use the same source.file
genaro@genaro-VirtualBox:~/Documents/test$ ln source.file hardlink.file
#Hardlink created, the content is the same as source.file
genaro@genaro-VirtualBox:~/Documents/test$ cat hardlink.file 
Welcome to DOU
#Deleted
genaro@genaro-VirtualBox:~/Documents/test$ rm hardlink.file 
genaro@genaro-VirtualBox:~/Documents/test$ rm hardlink.file 
rm: cannot remove 'hardlink.file': No such file or directory
genaro@genaro-VirtualBox:~/Documents/test$ ls -lia
total 1
24763 drwxrwxr-x 2 genaro genaro 4096 sep 13 22:53 .
24599 drwxr-xr-x 4 genaro genaro 4096 sep 13 22:35 ..
  805 -rw-rw-r-- 1 genaro genaro   15 sep 13 22:36 source.file
```

## What is an inode?

An inode is a data structure that stores various information about a file in Linux, such as the access mode (read, write, execute permissions), ownership, file type, file size, group, number of links, etc. Each inode is identified by an integer number. An inode is assigned to a file when it is created.

```bash
#When you create a hardlink these files share the same inode
#Because hard link acts as a mirror copy of the original file.
genaro@genaro-VirtualBox:~/Documents/test$ ls -lia
total 16
24763 drwxrwxr-x 2 genaro genaro 4096 sep 13 22:51 .
24599 drwxr-xr-x 4 genaro genaro 4096 sep 13 22:35 ..
  805 -rw-rw-r-- 2 genaro genaro   15 sep 13 22:36 hardlink.file
  805 -rw-rw-r-- 2 genaro genaro   15 sep 13 22:36 source.file

#On the other hand, soft link not act as a mirror copy, it is just as pointer
#to a source file
#The source file and the soft link not share the same inode
genaro@genaro-VirtualBox:~/Documents/test$ ls -lia
total 12
24763 drwxrwxr-x 2 genaro genaro 4096 sep 13 23:00 .
24599 drwxr-xr-x 4 genaro genaro 4096 sep 13 22:35 ..
  803 lrwxrwxrwx 1 genaro genaro   11 sep 13 23:00 softlink.file -> source.file
  805 -rw-rw-r-- 1 genaro genaro   15 sep 13 22:36 source.file
```