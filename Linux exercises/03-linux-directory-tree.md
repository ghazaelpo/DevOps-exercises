# Learning the Linux structure for the directories

The Filesystem Hierarchy Standard (FHS) defines the directory structure and directory contents in Linux distributions. Every service, process, command, absolutely everything in Linux is a file. This is the main premise for this Operative System based on Unix.

All these files are typically displayed in a hierarchical tree structure.

All the directories belong to primary hierarchy root and root directory of the entire file system hierarchy.

`/`, this is the absolutely path.

***Following we will explain the main and the most important directories:***

**Essentials Programs**

Directories containing files needed to run essential programs

`/bin`, essential command binaries such as cat, cp, ls. This commands are available for all the users.

`/sbin`, essential binaries only available for root user.

`/lib(64)`, libraries needed for essential binaries in /sbin.

**Non-Essentials Programs (Secondary Hierarchy)**

Directories containing files needed to run non-essential programs

`/etc`, system-specific configuration files for programs in /usr and /opt.

`/opt`, additional programs not found in distribution repositories.

`/usr`, portable, read only, non-essential programs and program files.

`/var`, used for storing dynamic program data that may change.

**Mount points**

Directories used for mounting devices and file systems

`/media`, removable media such as CD-ROMs and floppy drives.

`/mnt`, temporary file systems such as USB drives.

**User directories**

Directories containing user-specific files

`/home/(username)`, user files, configuration, and programs.

`/root`, home directory for the root user.

**Kernel/Runtime File Systems**

Directories populated by the kernel to provide information to programs and the user

`/proc`, information about processes, the kernel and system hardware.

`/sys`, information about system hardware and the kernel.

`/run`, information about the system since the last boot.

`/tmp`, directory for temporary files. Usually a tmpfs that is cleared on boot.

 **Other directories**

`/boot`, files essential for booting the system such as initrd, kernel, and bootloader configuration.

`/dev`, device files for physical devices such as HDDs as well as data streams (stdin, stdout...).

`/srv`, files used for services offered by the system such as www, rsync and ftp.

`/var`, variable (changing) files such as lock files, logs, mail, and program files.