# Working with Users and Groups and the root user in Linux

## Describe the process to:

- Create a user in Linux

```bash
#Use the useradd command following by the username of your choice
genaro@genaro-VirtualBox:~$ sudo useradd haza
```

- Delete a user in Linux

```bash
#Use the userdel command following by the username of your choice
genaro@genaro-VirtualBox:~$ sudo userdel haza
```

- Modify a user in Linux

```bash
#We can use usermod to make changes to an existing use
#There are so many options, we are going to discuss the most typicals:

#ADDING INFORMATION TO USER ACCOUNT
genaro@genaro-VirtualBox:~$ sudo usermod -c "This is Haza" haza
#Validating the added information
genaro@genaro-VirtualBox:~$ grep -E --color 'This is' /etc/passwd
haza:x:1001:1001:This is Haza:/home/haza:/bin/sh

#SET USER ACCOUNT EXPIRY DATE
#The option ‘-e‘ is used to set expiry date on a user account with the date... 
#format YYYY-MM-DD. Before, setting up an expiry date on a user, let’s first...
#check the current account expiry status using the...
#‘chage‘ (change user password expiry information) command.genaro@genaro-VirtualBox:~$ sudo chage -l haza
Last password change					: sep 13, 2021
Password expires					: never
Password inactive					: never
Account expires						: never
Minimum number of days between password change		: 0
Maximum number of days between password change		: 99999
Number of days of warning before password expires	: 7

#The expiry status of a "haza" user is NEVER, let’s change it...
#to Sep 14 2021 using "usermod -e" option and confirm the expiry date with "chage" command.
genaro@genaro-VirtualBox:~$ sudo chage -l haza
Last password change					: sep 13, 2021
Password expires					: never
Password inactive					: never
Account expires						: sep 14, 2021
Minimum number of days between password change		: 0
Maximum number of days between password change		: 99999
Number of days of warning before password expires	: 7
#VERY USEFUL!!!!
```

- Change user password

```bash
#It is a pretty easy and powerful command, you use as per below:
genaro@genaro-VirtualBox:~$ sudo passwd haza
#Type your new password
New password: 
#Type again
Retype new password:
#Completed 
passwd: password updated successfully
```

- Describe the different methods to list users in Linux (/etc/passwd, id, w, who, finger)

```bash
#/etc/passwd
	#The /etc/passwd file stores essential information, which required during login. 
	#In other words, it stores user account information.
	#The /etc/passwd is a plain text file.
	#You can use cat command to display this text file
genaro@genaro-VirtualBox:/etc$ cat passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
	#You can find a specific user using grep and the username
genaro@genaro-VirtualBox:/etc$ grep genaro passwd
genaro:x:1000:1000:Genaro Paredes,,,:/home/genaro:/bin/bash
	#The general form for this format is the below
username:password:userID:groupID:userIDInfo:homedirectory:command/shell

#id - print real and effective user and group IDs
genaro@genaro-VirtualBox:/etc$ id
uid=1000(genaro) gid=1000(genaro) groups=1000(genaro),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),120(lpadmin),132(lxd),133(sambashare)

#w - Show who is logged on and what they are doing.
genaro@genaro-VirtualBox:/etc$ w
 01:49:11 up 43 min,  1 user,  load average: 0.03, 0.10, 0.08
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
genaro   :0       :0               01:06   ?xdm?   1:18   0.01s /usr/lib/gdm3/g

#who - show who is logged on
genaro@genaro-VirtualBox:/etc$ who
genaro   :0           2021-09-13 01:06 (:0)

#finger — user information lookup program 
genaro@genaro-VirtualBox:/etc$ finger
Login     Name             Tty      Idle  Login Time   Office     Office Phone
genaro    Genaro Paredes  *:0             Sep 13 01:06 (:0)
```

- Create a group in Linux called dou-devops

```bash
genaro@genaro-VirtualBox:/etc$ sudo groupadd dou-devops
```

- Add the users dou-YOUR_NAME to the previous group

```bash
genaro@genaro-VirtualBox:/etc$ sudo useradd dou-genaro
genaro@genaro-VirtualBox:/etc$ sudo usermod -a -G dou-devops dou-genaro
```

- Delete the user dou-YOUR_NAME users from the dou-devops group

```bash
genaro@genaro-VirtualBox:/etc$ sudo deluser dou-genaro dou-devops
Removing user `dou-genaro' from group `dou-devops' ...
Done.
```

- Describe the different methods to consult groups in Linux

```bash
#The most memorable command to list all groups a user is a member of is...
#the groups command. When executed without an argument the command will print...
#a list of all groups the currently logged in user belongs to:
genaro@genaro-VirtualBox:~$ groups
genaro adm cdrom sudo dip plugdev lpadmin lxd sambashare
#To get a list of all groups a specific user belongs to...
#provide the username to the groups command as an argument:
genaro@genaro-VirtualBox:~$ groups dou-genaro
dou-genaro : dou-genaro

#Using the id command
#The id command prints information about the specified user and its groups. 
#If the username is omitted it shows information for the current user.
	#For example to get information about the user dou-genaro you would type:
	#The command will show the user ID (uid), the user’s primary group (gid), 
	#and the user’s secondary groups (groups)
genaro@genaro-VirtualBox:~$ id dou-genaro 
uid=1002(dou-genaro) gid=1003(dou-genaro) groups=1003(dou-genaro)
	#To print only the names instead of the numbers use the -n option. 
	#Option -g will print only the primary group and -G all groups.
genaro@genaro-VirtualBox:~$ id -nG dou-genaro 
dou-genaro

#Using etc/passwd file 
#You can search the user group in this file using the below format
username:password:userID:groupID:userIDInfo:homedirectory:command/shell
dou-genaro:x:1002:1003::/home/dou-genaro:/bin/sh

```

- How can you delete groups in Linux?

```bash
#Using groupdel
genaro@genaro-VirtualBox:~$ sudo groupdel dou-devops
#We can validate that the group is already deleted using the command again
genaro@genaro-VirtualBox:~$ sudo groupdel dou-devops 
groupdel: group 'dou-devops' does not exist
```

- Tell us the different method to use root privileges

```bash
#Using the word sudo before to write a command
sudo deluser dou-genaro dou-devops

#Or using the sudo command with -s or -i flag
#-i, --login                   run login shell as the target user; a command
                               #may also be specified
#-s, --shell                   run shell as the target user; a command may
                               #also be specified
genaro@genaro-VirtualBox:~$ sudo -s
root@genaro-VirtualBox:/home/genaro#
genaro@genaro-VirtualBox:~$ sudo -i
root@genaro-VirtualBox:~#

#Using su -
genaro@genaro-VirtualBox:~$ su -
Password:
root@genaro-VirtualBox:~#
```