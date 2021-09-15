# systemctl in Linux

## Tell us the history about systemD and systemV

**systemD**

The systemd (system daemon) is a service and management mechanism. In RHEL7 or above, it is responsible for initializing and activating system resources and server daemons at the boot time as well as on a running system.

In easy language, the systemd starts and manages all types of processes and services in Linux. In technical language, it is an initializer program that brings the system up to a defined state by activating all services and processes those are enabled in that state. To know which services and processes are enabled in which state, it uses configuration files.

**SystemV**

This initialization process was created for 'UNIX System V' systems in the early 1980s. After a little bit of customization, it was adopted in Linux. This classic initialization program worked well for many years. Till RHEL5, RedHat used this program as the default initialization program.

This process defines six system states known as run-levels and maps all processes and services with these run-levels. It also offers easy to use commands and methods for managing run-levels and their related services.

This program starts all services in a pre-defined sequence. It executes the next script in the sequence only if the current script in the sequence is executed or timed out. If a script stuck during the execution, it had to wait until that script timed out. This unexpected wait makes the entire system initialization process less efficient and ultimately slower.

## What's the difference between enabled and running?

Running refers to an active service, this service can initialize by default every time when your system has rebooted or you can activate manually, there is a specific command to lists the running state or detail on why it is not running, or if a service has been stopped unintentionally.

`systemctl status servicename` - *Show services status, active or inactive*
`systemctl start servicename`- *Start running a service*

On the other hand enable a service refer to initialize a service every time the server/computer is rebooted. So, this option is useful if you need start a service manually again and again.

`systemctl enable servicename` - *Enable a service*


## Enable and start a daemon, document the process

The systemctl utility can also be used to start or stop systemd services using a service unit file, with or without .service suffix

 In this example we are going to start httpd daemon:

```bash
#Firs we need to check if the daemon is active or inactive
apache2.service - The Apache HTTP Server
   Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: 
  Drop-In: /lib/systemd/system/apache2.service.d
           └─apache2-systemd.conf
   Active: inactive (dead) since Wed 2021-09-08 00:05:14 MDT; 3min 31s ago
  Process: 10075 ExecStop=/usr/sbin/apachectl stop (code=exited, status=0/SUCCES
 Main PID: 9823 (code=exited, status=0/SUCCESS)
#We can see above that the daemon is inactive
#So we can proceed to activate the daemon
ecee@embedded-vm:/etc/apt$ systemctl start apache2
ecee@embedded-vm:/etc/apt$ systemctl status apache2
● apache2.service - The Apache HTTP Server
   Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: 
  Drop-In: /lib/systemd/system/apache2.service.d
           └─apache2-systemd.conf
   Active: active (running) since Wed 2021-09-08 00:11:17 MDT; 3s ago
  Process: 10075 ExecStop=/usr/sbin/apachectl stop (code=exited, status=0/SUCCES
  Process: 10109 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCC
 Main PID: 10113 (apache2)
    Tasks: 55 (limit: 4915)
   CGroup: /system.slice/apache2.service
           ├─10113 /usr/sbin/apache2 -k start
           ├─10114 /usr/sbin/apache2 -k start
           └─10115 /usr/sbin/apache2 -k start
```

If you need start daemons every time you rebooted your pc/server the best option is use `systemctl enable` command. Starting them manually is not a convenient method to employ due to the number of services required to run on a server.

```bash
#In this case we rebooted our linux system and we can see that httpd daemon
#is not running
ecee@embedded-vm:~$ systemctl status apache2
● apache2.service - The Apache HTTP Server
   Loaded: loaded (/lib/systemd/system/apache2.service; disabled; vendor preset:
  Drop-In: /lib/systemd/system/apache2.service.d
           └─apache2-systemd.conf
   Active: inactive (dead)
#We will reboot once again but first we are going to use enable command and
#check the result
ecee@embedded-vm:~$ sudo systemctl enable apache2
[sudo] password for ecee: 
Synchronizing state of apache2.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable apache2

#Now our daemon was enable, reboot again the system and then check the httpd status
#I used uptime to check how long my system has turned on
ecee@embedded-vm:~$ uptime
 00:44:06 up 0 min,  1 user,  load average: 3.76, 1.33, 0.47
ecee@embedded-vm:~$ systemctl status apache2
● apache2.service - The Apache HTTP Server
   Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: 
  Drop-In: /lib/systemd/system/apache2.service.d
           └─apache2-systemd.conf
   Active: active (running) since Wed 2021-09-08 00:43:29 MDT; 52s ago
 Main PID: 1051 (apache2)
    Tasks: 55 (limit: 4915)
   CGroup: /system.slice/apache2.service
           ├─1051 /usr/sbin/apache2 -k start
           ├─1054 /usr/sbin/apache2 -k start
           └─1055 /usr/sbin/apache2 -k start

Sep 08 00:43:18 embedded-vm systemd[1]: Starting The Apache HTTP Server...
Sep 08 00:43:29 embedded-vm apachectl[936]: AH00557: apache2: apr_sockaddr_info_
Sep 08 00:43:29 embedded-vm apachectl[936]: AH00558: apache2: Could not reliably
Sep 08 00:43:29 embedded-vm systemd[1]: Started The Apache HTTP Server.
```

## What are the available targets in centos 7? (multi-user, desktop, etc)

Previous versions of CentOS/RHEL Linux use **SysV init run levels**. These run levels provided the ability to use systems for different purposes and only start the services needed for a specific purpose, at a specific run level. In RHEL 7, run levels have been replaced with **systemd target units**. Target units have a **.target** extension and similar to run levels, target units allow you to start a system with only the services that are required for a specific purpose.
>Target units do not offer any additional functionality on top of the generic functionality provided by units. They exist merely to group units via dependencies (useful as boot targets), and to establish standardized names for synchronization points used in dependencies between units. Among other things, target units are a more flexible replacement for SysV runlevels in the classic SysV init system.

# Comparison of SysV runlevels with systemd targets
| Run Level | Target Unit | Description |
| ------- | ------- | ------- |
| 0 | runlevel0.target, poweroff.target | Shut down and power off the system. |
| 1 | runlevel1.target, rescue.target | Set up a rescue shell. |
| 2,3,4 | runlevel[2,3,4].target, multi-user.target | Set up a non-graphical multi-user system. |
| 5 | runlevel5.target, graphical.target | Set up a graphical multi-user system. |
| 6 | runlevel6.target, reboot.target | Shut down and reboot the system. |

To view the currently active target units on your system use below command.

```bash
# systemctl list-units --type target
UNIT                   LOAD   ACTIVE SUB    DESCRIPTION
basic.target           loaded active active Basic System
cryptsetup.target      loaded active active Encrypted Volumes
getty.target           loaded active active Login Prompts
graphical.target       loaded active active Graphical Interface
local-fs-pre.target    loaded active active Local File Systems (Pre)
local-fs.target        loaded active active Local File Systems
multi-user.target      loaded active active Multi-User System
network-online.target  loaded active active Network is Online
network.target         loaded active active Network
nfs-client.target      loaded active active NFS client services
nss-user-lookup.target loaded active active User and Group Name Lookups
paths.target           loaded active active Paths
remote-fs-pre.target   loaded active active Remote File Systems (Pre)
remote-fs.target       loaded active active Remote File Systems
slices.target          loaded active active Slices
sockets.target         loaded active active Sockets
swap.target            loaded active active Swap
sysinit.target         loaded active active System Initialization
timers.target          loaded active active Timers

LOAD   = Reflects whether the unit definition was properly loaded.
ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
SUB    = The low-level unit activation state, values depend on unit type.

19 loaded units listed. Pass --all to see loaded but inactive units, too.
To show all installed unit files use 'systemctl list-unit-files'.
```
Even we can consult an specific level, one by one as per below:

```bash
#Run Level 0
ecee@embedded-vm:~$ systemctl status poweroff.target
● poweroff.target - Power-Off
   Loaded: loaded (/lib/systemd/system/poweroff.target; disabled; vendor preset:
   Active: inactive (dead)
     Docs: man:systemd.special(7)
#Run Level 1
ecee@embedded-vm:~$ systemctl status rescue.target
● rescue.target - Rescue Mode
   Loaded: loaded (/lib/systemd/system/rescue.target; disabled; vendor preset: d
   Active: inactive (dead)
     Docs: man:systemd.special(7)
#Run Level 2,3,4
ecee@embedded-vm:~$ systemctl status multi-user.target
● multi-user.target - Multi-User System
   Loaded: loaded (/lib/systemd/system/multi-user.target; static; vendor preset:
   Active: active since Wed 2021-09-08 09:32:19 MDT; 8min ago
     Docs: man:systemd.special(7)

Sep 08 09:32:19 embedded-vm systemd[1]: Reached target Multi-User System.
#Run Level 5
ecee@embedded-vm:~$ systemctl status graphical.target
● graphical.target - Graphical Interface
   Loaded: loaded (/lib/systemd/system/graphical.target; static; vendor preset: 
   Active: active since Wed 2021-09-08 09:32:19 MDT; 10min ago
     Docs: man:systemd.special(7)

Sep 08 09:32:19 embedded-vm systemd[1]: Reached target Graphical Interface.
#Run Level 6
ecee@embedded-vm:~$ systemctl status reboot.target
● reboot.target - Reboot
   Loaded: loaded (/lib/systemd/system/reboot.target; disabled; vendor preset: e
   Active: inactive (dead)
     Docs: man:systemd.special(7)
```

