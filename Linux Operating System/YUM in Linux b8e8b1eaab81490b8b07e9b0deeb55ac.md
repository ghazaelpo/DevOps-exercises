# YUM in Linux

---

## Tell us the history of yum

The original package manager, Yellowdog UPdater (YUP) was developed in 1999-2001 by Dan Burcaw, Bryan Stillwell, Stephen Edie, and Troy Bengegerdes at Terra Soft Solutions (under the leadership of then CEO Kai Staats) as a back-end engine for a graphical installer of Yellow Dog Linux.

As a full rewrite of YUP, YUM evolved primarily to update and manage Red Hat Linux systems used at the Duke University Department of Physics by Seth Vidal and Michael Stenner. Vidal continued to contribute to YUM until his death in a Durham, North Carolina bicycle accident on 8 July 2013.

In 2003 Robert G. Brown at Duke published documentation for YUM. Subsequent adopters included Fedora, CentOS, and many other RPM-based Linux distributions, including Yellow Dog Linux itself, where YUM replaced the original YUP utility — last updated on SourceForge in 2001. By 2005, it was estimated to be in use on over half of the Linux market, and by 2007 YUM was considered the "tool of choice" for RPM-based Linux distributions.

## Mention the config files that yum uses

The configuration file for `yum` and related utilities is located at `/etc/yum.conf`. This file contains one mandatory `[main]` section, which allows you to set Yum options that have global effect, and can also contain one or more `[*repository*]` sections, which allow you to set repository-specific options. However, it is recommended to define individual repositories in new or existing `.repo` files in the `/etc/yum.repos.d/` directory. The values you define in individual `[*repository*]` sections of the `/etc/yum.conf` file override values set in the `[main]` section.

This section shows you how to:

- set global Yum options by editing the [main] section of the /etc/yum.conf configuration file
- set options for individual repositories by editing the [repository] sections in /etc/yum.conf and .repo files in the /etc/yum.repos.d/ directory;
- use Yum variables in /etc/yum.conf and files in the /etc/yum.repos.d/ directory so that dynamic version and architecture values are handled correctly;
- add, enable, and disable Yum repositories on the command line; and,
- set up your own custom Yum repository.

## What is the difference between yum and yum group

The `groupinstall` command installs a bundle of packages that are designated as a group so that you don't need to install a bunch of individual packages yourself to have all of the features.

```bash
[root@6ee502dc6f34 /]# yum grouplist
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.

Red Hat Universal Base Image 8 (RPMs) - BaseOS                1.4 MB/s | 787 kB     00:00    
Red Hat Universal Base Image 8 (RPMs) - AppStream             827 kB/s | 2.4 MB     00:02    
Red Hat Universal Base Image 8 (RPMs) - CodeReady Builder      30 kB/s |  15 kB     00:00    
Last metadata expiration check: 0:00:01 ago on Fri Sep  3 07:48:24 2021.
Error: No group data available for configured repositories.
```

And if you want to install a only package, you have to specify it.

```bash
yum install wget.x86_64
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.

Last metadata expiration check: 0:10:10 ago on Fri Sep  3 07:48:24 2021.
Dependencies resolved.
==============================================================================================
 Package         Architecture      Version                   Repository                  Size
==============================================================================================
Installing:
 wget            x86_64            1.19.5-10.el8             ubi-8-appstream            734 k

Transaction Summary
==============================================================================================
Install  1 Package

Total download size: 734 k
Installed size: 2.8 M
Is this ok [y/N]: y
Downloading Packages:
wget-1.19.5-10.el8.x86_64.rpm                                 1.7 MB/s | 734 kB     00:00    
----------------------------------------------------------------------------------------------
Total                                                         1.7 MB/s | 734 kB     00:00     
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                      1/1 
  Installing       : wget-1.19.5-10.el8.x86_64                                            1/1 
  Running scriptlet: wget-1.19.5-10.el8.x86_64                                            1/1 
  Verifying        : wget-1.19.5-10.el8.x86_64                                            1/1 
Installed products updated.

Installed:
  wget-1.19.5-10.el8.x86_64                                                                   

Complete!
```

## How can you list all the installed packages using yum?

```bash
Using the yum list installed command
# Below we can find just some installed packages
yum list installed
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.

Installed Packages
acl.x86_64                                        2.2.53-1.el8                         @System
audit-libs.x86_64                                 3.0-0.17.20191104git1c2f876.el8      @System
basesystem.noarch                                 11-5.el8                             @System
bash.x86_64                                       4.4.20-1.el8_4                       @System
brotli.x86_64                                     1.0.6-3.el8                          @System
bzip2-libs.x86_64                                 1.0.6-26.el8                         @System
ca-certificates.noarch                            2020.2.41-80.0.el8_2                 @System
chkconfig.x86_64                                  1.13-2.el8                           @System
coreutils-single.x86_64                           8.30-8.el8                           @System
cracklib.x86_64                                   2.9.6-15.el8                         @System
cracklib-dicts.x86_64                             2.9.6-15.el8                         @System
crypto-policies.noarch                            20210209-1.gitbfb6bed.el8_3          @System
crypto-policies-scripts.noarch                    20210209-1.gitbfb6bed.el8_3          @System
cryptsetup-libs.x86_64                            2.3.3-4.el8                          @System

```