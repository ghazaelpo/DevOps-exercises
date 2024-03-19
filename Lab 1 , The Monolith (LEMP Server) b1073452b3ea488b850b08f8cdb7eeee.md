# Lab 1 , The Monolith (LEMP Server)

### Instructions

- By any means of infrastructure (VMs, AWS, GCP, DigitalOcean), you will create an ubuntu server and deploy "ghost blog" using mysql (not MariaDB) and nginx, as database and reverse proxy, respectively

Ghost is an open-source blogging software coded in Node.js, allowing you to create modern, beautiful blogs. Compared to WordPress, Ghost is lightweight and much faster because it’s built specifically for blogging and isn’t a comprehensive content management system like WordPress.

**Prerequisites of Installing Ghost on Ubuntu Server.**

First we will create a new user as per the tutorial

```bash
adminuser@Genaro-vm:~$ sudo adduser ghost
```

Once the user was created, we will update Ubuntu and the install Node.js

```bash
ghost@Genaro-vm:~$ sudo apt update;sudo apt upgrade
ghost@Genaro-vm:~$ curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
ghost@Genaro-vm:~$ sudo apt install nodejs
```

Check the installed version of Node.js and npm

```bash
ghost@Genaro-vm:~$ node -v
v10.24.1
ghost@Genaro-vm:~$ npm -v
6.14.12
```

In my case I will use ghost username created before

![Screen Shot 2021-10-21 at 14.13.20.png](Lab%201%20,%20The%20Monolith%20(LEMP%20Server)%20b1073452b3ea488b850b08f8cdb7eeee/Screen_Shot_2021-10-21_at_14.13.20.png)

and I will use mytestdb database created before too

![Screen Shot 2021-10-21 at 14.12.15.png](Lab%201%20,%20The%20Monolith%20(LEMP%20Server)%20b1073452b3ea488b850b08f8cdb7eeee/Screen_Shot_2021-10-21_at_14.12.15.png)

Showing privileges for our username

![Screen Shot 2021-10-21 at 14.16.30.png](Lab%201%20,%20The%20Monolith%20(LEMP%20Server)%20b1073452b3ea488b850b08f8cdb7eeee/Screen_Shot_2021-10-21_at_14.16.30.png)

Output from ghost install

![Screen Shot 2021-10-21 at 14.18.51.png](Lab%201%20,%20The%20Monolith%20(LEMP%20Server)%20b1073452b3ea488b850b08f8cdb7eeee/Screen_Shot_2021-10-21_at_14.18.51.png)

Resource deployed 

![Screen Shot 2021-10-21 at 14.08.25.png](Lab%201%20,%20The%20Monolith%20(LEMP%20Server)%20b1073452b3ea488b850b08f8cdb7eeee/Screen_Shot_2021-10-21_at_14.08.25.png)

![Screen Shot 2021-10-22 at 0.53.27.png](Lab%201%20,%20The%20Monolith%20(LEMP%20Server)%20b1073452b3ea488b850b08f8cdb7eeee/Screen_Shot_2021-10-22_at_0.53.27.png)

[Lab 2, the microservice approach, DockerCompose](Lab%201%20,%20The%20Monolith%20(LEMP%20Server)%20b1073452b3ea488b850b08f8cdb7eeee/Lab%202,%20the%20microservice%20approach,%20DockerCompose%200e8cad5f9d7444eb8dafa651cbf1a366.md)