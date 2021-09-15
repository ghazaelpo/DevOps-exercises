# Learning SSH

## Tell us a brief history about SSH and why I should learn SSH

The [**Secure Shell protocol**](https://www.ssh.com/ssh/protocol/) was developed by **[Tatu Ylonen](https://ylonen.org/)** in 1995 due to a hacking incident in the Finnish university network. A password sniffer had been installed on a server connected directly to main network, so many passwords and usernames had stolen, even from Ylonen's company.

That incident give motivation to Ylonen to study cryptography and develop a solution for remote login over the internet safely. His friends proposed additional features, and three months later, in July 1995, Ylonen published the first version as open source. That was the born of OpenSSH.

Today, the protocol is very popular and used for managing more than half of world’s web servers and practically every Unix or Linux computer. It is most used by system administrators and Information security specialists to configure, manage, maintain, and operate most firewalls, routers, switches, and servers in the millions of mission-critical networks and environments of our digital world. It is also embedded inside many file transfer and systems management solutions.

There are so many reasons for use this protocol, following I will mention the most important:

- Providing secure access for users and automated processes
- Interactive and automated file transfers
- Issuing remote commands
- Managing network infrastructure and other mission-critical system components
- Allow multiple connections

## Document the steps needed to configure an SSH server

### Step1: Install required packages

Let’s start by opening a terminal window to enter the necessary commands.

Remember to update your Ubuntu system using `sudo apt update` and `sudo apt upgrade` before installing new packages or software with to make sure that you are running the latest versions.

```bash
sudo apt update && sudo apt upgrade
```

The package you need to run SSH Server is provided by openssh-server component from OpenSSH:

```bash
sudo apt install openssh-server
```

### **Step 2: Checking the status of the server**

Once the downloading and installation of the package is done the SSH service should be already running, but to be sure we will check it with:

```bash
sudo systemctl status ssh
#You should see something like this, with the word Active highlighted.
genaro@genaro-VirtualBox:~$ sudo systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: >
     Active: active (running) since Fri 2021-09-10 16:11:40 CDT; 9min ago
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 623 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 656 (sshd)
      Tasks: 1 (limit: 1802)
     Memory: 2.5M
     CGroup: /system.slice/ssh.service
             └─656 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
```

### **Step 3: Allowing SSH through the firewall**

Ubuntu comes with a firewall utility called [UFW](https://itsfoss.com/set-up-firewall-gufw/) (UncomplicatedFirewall) which is an interface for **iptables** that in turn manages the network’s rules. If the firewall is active, it may prevent the connection to your SSH Server.

To configure UFW so that it allows the wanted access, you need to run the following command:

```bash
sudo ufw allow ssh
#Just to be sure and the connection does not fail execute the below commands
genaro@genaro-VirtualBox:~$ sudo ufw status
Status: inactive
genaro@genaro-VirtualBox:~$ sudo ufw enable
Firewall is active and enabled on system startup
genaro@genaro-VirtualBox:~$ sudo ufw status
Status: active
```

The status of UFW can be checked running `sudo ufw status`.

At this time our SSH Server is up and running, just waiting for a connection from a client.

### Connecting to the remote system from your local machine

Your local Linux system should already have SSH client installed. If not, you may always install it using the following command on Ubuntu:

```bash
sudo apt install openssh-client
```

To connect to your Ubuntu system you need to know the IP address of the computer and use the `ssh` command, like this:

```bash
ssh username@address
```

Change username to your actual user in the system and address to the IP address of your Ubuntu machine.

If you don’t know the IP address of your computer you can type ip a in the terminal of the server and check the output. You should have something like this:

```bash
genaro@genaro-VirtualBox:~$ ifconfig
enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet **192.168.100.138**  netmask 255.255.255.0  broadcast 192.168.100.255
        inet6 2806:2f0:5000:f1e3:c094:9be2:659e:471  prefixlen 64  scopeid 0x0<global>
        inet6 2806:2f0:5000:f1e3:1799:b499:43d7:58a6  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::a602:2c86:df42:b8f2  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:e2:36:73  txqueuelen 1000  (Ethernet)
        RX packets 76  bytes 8244 (8.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 143  bytes 16400 (16.4 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 168  bytes 14202 (14.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 168  bytes 14202 (14.2 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

As you can see here my IP address is 192.168.100.138. Let’s try connecting using the username@address format.

```bash
genaroparedes@GenaroParedes-MacBook-Pro ~ % ssh genaro@192.168.100.138
```

The first time you connect to a SSH server, it will ask for permission to add the host. Type yes and hit Enter to continue.

Immediately SSH tells you that the host was permanently added and then asks for the password assigned to the username. Type in the password and hit Enter one more time.

And that's it! You will be logged into your Ubuntu system remotely!

```bash
genaroparedes@GenaroParedes-MacBook-Pro ~ % ssh genaro@192.168.100.138
genaro@192.168.100.138's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.11.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 updates can be applied immediately.

Your Hardware Enablement Stack (HWE) is supported until April 2025.
Last login: Fri Sep 10 16:16:43 2021 from 192.168.100.127
genaro@genaro-VirtualBox:~$
```

## Copy one of the files from the previous practice to one of your coworkers, document all the steps and paste screenshots as proofs

Copy using SSH is not really difficult, there are two cases, **from local to remote** and **from remote to local** but in this case, as per the above requirement we will copy from local to remote and additionally I will mention the other option too.

```bash
#Copying a file local from the previous practice to a someone remote
#Use this form: scp myfile.txt remoteuser@remoteserver:/remote/folder/
genaroparedes@GenaroParedes-MacBook-Pro exercises % scp 10-systemctl.md genaro@192.168.100.138:/home/genaro/Documents/Example
genaro@192.168.100.138's password: 
10-systemctl.md                                   100%   11KB 381.3KB/s   00:00
```

The below image show the results:

![Screen Shot 2021-09-10 at 19.43.38.png](Learning%20SSH%202ff901bfce38445c9808d90a4565a26a/Screen_Shot_2021-09-10_at_19.43.38.png)

If you want copy from remote to local, you just use the below form:

```bash
#This is additionally apart the requirement
scp remoteuser@remoteserver:/remote/folder/remotefile.txt  localfile.txt
```

## Customize the ssh dir using the configuration file at /etc/ssh/sshd_config and apply the following requirements:

- Change the default SSH port

```bash
#Go to the the specified path above /etc/sshd_config
genaro@genaro-VirtualBox:/etc/ssh$ ls
moduli        sshd_config.d           ssh_host_ed25519_key.pub
ssh_config    ssh_host_ecdsa_key      ssh_host_rsa_key
ssh_config.d  ssh_host_ecdsa_key.pub  ssh_host_rsa_key.pub
sshd_config   ssh_host_ed25519_key    ssh_import_id
#Then open the sshd_config file
genaro@genaro-VirtualBox:/etc/ssh$ sudo vim sshd_config
#And you will see the file displayed as per below
#Change the part where my cursor is current located
```

![Untitled](Learning%20SSH%202ff901bfce38445c9808d90a4565a26a/Untitled.png)

Please note that port numbers 0-1023 are reserved for various system services. Hence, I recommend choosing port numbers between 1024 and 65535. It is necessary change the default 22 port to another one available, in this case we will use 2222

![Untitled](Learning%20SSH%202ff901bfce38445c9808d90a4565a26a/Untitled%201.png)

```bash
#It is mandatory allow the port in the firewall
genaro@genaro-VirtualBox:/etc/ssh$ sudo ufw allow 2222/tcp
Rule added
Rule added (v6)
genaro@genaro-VirtualBox:/etc/ssh$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW       Anywhere                  
2222/tcp                   ALLOW       Anywhere                  
22/tcp (v6)                ALLOW       Anywhere (v6)             
2222/tcp (v6)              ALLOW       Anywhere (v6)
```

Then just try the connection:

```bash
#In this case is necessary specefies the port using -p 2222
genaroparedes@GenaroParedes-MacBook-Pro ssh % ssh genaro@192.168.100.138 -p 2222
genaro@192.168.100.138's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.11.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 updates can be applied immediately.

Your Hardware Enablement Stack (HWE) is supported until April 2025.
Last login: Sat Sep 11 13:19:40 2021 from 192.168.100.127
genaro@genaro-VirtualBox:~$
```

- Disable access to root user through ssh

```bash
#As you can see we have root access
genaroparedes@GenaroParedes-MacBook-Pro ~ % ssh root@192.168.100.138 -p 2222  
root@192.168.100.138\'s password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.11.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 updates can be applied immediately.

Your Hardware Enablement Stack (HWE) is supported until April 2025.
Last login: Sun Sep 12 01:19:27 2021 from 192.168.100.127
root@genaro-VirtualBox:~#

#We will disable the root access through sshd_config file
#Go to etc/ssh/sshd_config and use vim to open it
root@genaro-VirtualBox:/etc/ssh# vim sshd_config
#In the below part from the file edit PermitRootLogin
#And set as no

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin prohibit-password
PermitRootLogin no
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

#Try log in again and you will not able to connect as root user
genaroparedes@GenaroParedes-MacBook-Pro ~ % ssh root@192.168.100.138 -p 2222
root@192.168.100.138\'s password: 
Permission denied, please try again.
root@192.168.100.138's password: 
Permission denied, please try again.
root@192.168.100.138\'s password: 
root@192.168.100.138: Permission denied (publickey,password).
```

- Create a group to enhance ssh security using the AllowGroups flag and enable ssh access for a new user called letmein, document the process

```bash
#Creating the user requested
genaro@genaro-VirtualBox:~$ sudo useradd letmein
#Creating a new example group
genaro@genaro-VirtualBox:~$ sudo groupadd example
#Adding new user to example group
genaro@genaro-VirtualBox:~$ sudo usermod -a -G example letmein
#Now you have to edit the sshd_config and add AllowGroups flag
#with the example group
#once you have changed it, restart the ssh service
AllowGroups example

#If you try to log in with different users you will not able because
#you have only log in using a belong user to example group as letmein user
genaroparedes@GenaroParedes-MacBook-Pro ~ % ssh genaro@192.168.100.138 -p 2222
genaro@192.168.100.138\'s password: 
Permission denied, please try again.
genaroparedes@GenaroParedes-MacBook-Pro ~ % ssh root@192.168.100.138 -p 2222
root@192.168.100.138\'s password: 
Permission denied, please try again.

#Log in successfully 
genaroparedes@GenaroParedes-MacBook-Pro ~ % ssh letmein@192.168.100.138 -p 2222
letmein@192.168.100.138's password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.11.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 updates can be applied immediately.

Your Hardware Enablement Stack (HWE) is supported until April 2025.
```

- Create an entry banner that displays the text "Welcome stranger to DigitalOnUs" everytime a user ssh into your VM

```bash
#Create a file that contain the text mentioned above in the path /etc/ssh
genaro@genaro-VirtualBox:/etc/ssh$ sudo vim example
#Then edit the sshd_config file and modify the Banner flag adding your path
#and file name 
Banner etc/ssh/example

#Now try log in to the server and see the results as per below
```

![Screen Shot 2021-09-12 at 3.22.07.png](Learning%20SSH%202ff901bfce38445c9808d90a4565a26a/Screen_Shot_2021-09-12_at_3.22.07.png)

## Config your own ssh using $USER/.ssh/config and make sure when you type server01 it connects to your coworker machine

```bash
#First you need go to path mentioned above
genaroparedes@GenaroParedes-MacBook-Pro ~ % cd ~/.ssh/
#Look at your config file        
genaroparedes@GenaroParedes-MacBook-Pro .ssh % ls
config		id_ed25519	id_ed25519.pub	known_hosts
#And configure as per below
genaroparedes@GenaroParedes-MacBook-Pro .ssh % more config 
Host server01
        Hostname 192.168.100.138
        Port 2222
        ForwardX11 yes
Host *
        User genaro
#In the first section you have to give a name to your host
#For our example the host is called server01
#The hostname flag is the IP address for our computer
#The port flag is the port that defined for us
#And ForwardX11 flag is the secure channel enabled
#Finally you have to add the User flag and put your username

#Once you have complete your configuration just type your host name and that's all
genaroparedes@GenaroParedes-MacBook-Pro .ssh % ssh server01
                                          
                 ,----..                  
    ,---,       /   /   \                 
  .'  .' `\    /   .     :          ,--,  
,---.'     \  .   /   ;.  \       ,'_ /|  
|   |  .`\  |.   ;   /  ` ;  .--. |  | :  
:   : |  '  |;   |  ; \ ; |,'_ /| :  . |  
|   ' '  ;  :|   :  | ; | '|  ' | |  . .  
'   | ;  .  |.   |  ' ' ' :|  | ' |  | |  
|   | :  |  ''   ;  \; /  |:  | | :  ' ;  
'   : | /  ;  \   \  ',  / |  ; ' |  | '  
|   | '` ,/    ;   :    /  :  | : ;  ; |  
;   :  .'       \   \ .'   '  :  `--'   \ 
|   ,.'          `---`     :  ,      .-./ 
'---'                       `--`----'     
                                          
///Welcome stranger to DigitalOnus///

genaro@192.168.100.138\'s password: 
Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.11.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 updates can be applied immediately.

Your Hardware Enablement Stack (HWE) is supported until April 2025.
Last login: Sun Sep 12 04:00:24 2021 from 192.168.100.127
genaro@genaro-VirtualBox:~$
```

## Document how to create an ssh key and how to copy the key into another server

```bash
#Create the ssh key using the below command
# -t flag is for spicifies the type of key, we will use ed25519
genaroparedes@GenaroParedes-MacBook-Pro .ssh % ssh-keygen -t ed25519
Generating public/private ed25519 key pair.
Enter file in which to save the key (/Users/genaroparedes/.ssh/id_ed25519): ./newkey_ed25519
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in ./newkey_ed25519.
Your public key has been saved in ./newkey_ed25519.pub.
The key fingerprint is:
SHA256:7Ui93sh1ZfE14wJIr/9zNUM3uBj3AEpfRQPCr4rLp7Y genaroparedes@GenaroParedes-MacBook-Pro.local
The key\'s randomart image is:
+--[ED25519 256]--+
|         ... .++ |
|        ..oo..  .|
|        ..oo+ .+.|
|         +.o.=.oB|
|        S.o =.=.*|
|       . o.+ ..*.|
|        o +.. . +|
|      .o = +.o . |
|      .E= + ..o  |
+----[SHA256]-----+

#Now if you want to use this ssh key to authentic your identity...
#You must copy this key to our server because above we created for the client...
#That means we created a key in the client and then is necessary to copy...
#To the server and validate our identity for log in.
genaroparedes@GenaroParedes-MacBook-Pro .ssh % ssh-copy-id -i newkey_ed25519.pub genaro@192.168.100.139
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "newkey_ed25519.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
                                          
                 ,----..                  
    ,---,       /   /   \                 
  .'  .' `\    /   .     :          ,--,  
,---.'     \  .   /   ;.  \       ,'_ /|  
|   |  .`\  |.   ;   /  ` ;  .--. |  | :  
:   : |  '  |;   |  ; \ ; |,'_ /| :  . |  
|   ' '  ;  :|   :  | ; | '|  ' | |  . .  
'   | ;  .  |.   |  ' ' ' :|  | ' |  | |  
|   | :  |  ''   ;  \; /  |:  | | :  ' ;  
'   : | /  ;  \   \  ',  / |  ; ' |  | '  
|   | '` ,/    ;   :    /  :  | : ;  ; |  
;   :  .'       \   \ .'   '  :  `--'   \ 
|   ,.'          `---`     :  ,      .-./ 
'---'                       `--`----'     
                                          
///Welcome stranger to DigitalOnus///

Enter passphrase for key '/Users/genaroparedes/.ssh/id_ed25519': 
Enter passphrase for key '/Users/genaroparedes/.ssh/id_ed25519': 
genaro@192.168.100.139's password: 

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'genaro@192.168.100.139'"
and check to make sure that only the key(s) you wanted were added.
#Log in again
genaroparedes@GenaroParedes-MacBook-Pro .ssh % ssh -i newkey_ed25519 genaro@192.168.100.139 
                                          
                 ,----..                  
    ,---,       /   /   \                 
  .'  .' `\    /   .     :          ,--,  
,---.'     \  .   /   ;.  \       ,'_ /|  
|   |  .`\  |.   ;   /  ` ;  .--. |  | :  
:   : |  '  |;   |  ; \ ; |,'_ /| :  . |  
|   ' '  ;  :|   :  | ; | '|  ' | |  . .  
'   | ;  .  |.   |  ' ' ' :|  | ' |  | |  
|   | :  |  ''   ;  \; /  |:  | | :  ' ;  
'   : | /  ;  \   \  ',  / |  ; ' |  | '  
|   | '` ,/    ;   :    /  :  | : ;  ; |  
;   :  .'       \   \ .'   '  :  `--'   \ 
|   ,.'          `---`     :  ,      .-./ 
'---'                       `--`----'     
                                          
///Welcome stranger to DigitalOnus///

Welcome to Ubuntu 20.04.3 LTS (GNU/Linux 5.11.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

0 updates can be applied immediately.

Your Hardware Enablement Stack (HWE) is supported until April 2025.
Last login: Sun Sep 12 19:15:32 2021 from 192.168.100.127
genaro@genaro-VirtualBox:~$ 

```