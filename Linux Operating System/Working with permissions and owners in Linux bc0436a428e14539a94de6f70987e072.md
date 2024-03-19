# Working with permissions and owners in Linux

# Tell us what you learned about Linux permissions

Linux permissions is one of the security features built into Linux-based systems. We can use it for allow or deny access in a specific file so this feature reduce vulnerabilities.

This feature allow give permissions for a specific category such as owner, group and others.

Let me explain each category below:

- Owner

The Owner permissions apply only the owner of the file or directory, they will not impact the actions of other users.

- Group

The Group permissions apply only to the group that has been assigned to the file or directory, they will not effect the actions of other users.

- Other

The Other permissions apply to all other users on the system, this is the permission group that you want to watch the most.

**Each category has three basic permission types:**

- Read

The Read permission refers to a user’s capability to read the contents of the file.

- Write

The Write permissions refer to a user’s capability to write or modify a file or directory.

- Execute

The Execute permission affects a user’s capability to execute a file or view the contents of a directory.

If we are working constantly with files and we want allow or deny a specific action first is necessary to learn how to check this permissions and for which category is applied.

**Viewing the Permissions**

You can view the permissions by reviewing the output of the `ls -l` command while in the terminal and while working in the directory which contains the file or folder.

Example:

```bash
genaroparedes@GenaroParedes-MacBook-Pro exercises % ls -l
total 304
-rw-rw-r--@ 1 genaroparedes  staff  118401 Sep  3 17:20 08-Red Hat Package Manager.md

#General format
_rwxrwxrwx 1 owner:group
```

- User rights/Permissions
    1. The first character that I marked with an underscore is the special permission flag that can vary. 
        1. "-" indicates a file
        2. "d" indicates a directory 
        3. "l" indicates a link
    2. The following set of three characters (rwx) is for the Owner or permissions.
    3. The second set of three characters (rwx) is for the Group permissions.
    4. The third set of three characters (rwx) is for the Others permissions.
- Following that grouping since the integer/number displays the number of hardlinks to the file.
- The last piece is the Owner and Group assignment formatted as Owner:Group.

**Explicitly Defining Permissions**

To explicitly define permissions you will need to reference the Permission Group and Permission Types.

The Permission Groups used are:

- **u** – Owner
- **g** – Group
- **o** – Others
- **a** – All users

The potential Assignment Operators are + (plus) and – (minus); these are used to tell the system whether to add or remove the specific permissions.

The Permission Types that are used are:

- **r** – Read
- **w** – Write
- **x** – Execute

So for an example, lets say I have a file named file1 that currently has the permissions set to:

 -**rw-rw-rw**

Which means that the owner, group and other have read and write permission. Now we want to remove the read and write permissions from the all users group.

To make this modification you would invoke the command: ***chmod a-rw file1*** to add the permissions above you would invoke the command: ***chmod a+rw file1***

As you can see, if you want to grant those permissions you would change the minus character to a plus to add those permissions.

With all this information we can proceed to work on the below questions and situations.

## Create a file called January with the specific permissions to files and directories in Linux

- **January - read/write for user and only read for groups and for the others only execution**

```bash
#First we create the required file
genaroparedes@GenaroParedes-MacBook-Pro devops % touch January.txt

#Now is time for apply the previous knowledge discussed in the first question

#Viewing the permissions of January file
genaroparedes@GenaroParedes-MacBook-Pro devops % ls -l
total 0
-rw-r--r--  1 genaroparedes  staff  0 Sep  8 17:28 January.txt
#In this case the file has already read/write permissions for the Owner and just
#read permission for Group and All users(Others)
#So we need change the permissions as per requested above even if the Owner part
#has already set we will apply the changes

#read/write for user(owner)
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod u+rw January.txt
#read for groups
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod g+r January.txt
#execution for others
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod o-r January.txt
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod o+x January.txt

#Result
genaroparedes@GenaroParedes-MacBook-Pro devops % ls -l
total 0
-rw-r----x  1 genaroparedes  staff  0 Sep  8 17:28 January.txt
```

- **February - read/write/exec for user and read/write for groups and for the others no permissions at all**

```bash
#read/write/exec for user 
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod u+rwx February.txt
#read/write for groups
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod g+rw February.txt
#no permissions at all for others
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod o-rwx February.txt

#Result
-rwxrw----  1 genaroparedes  staff  0 Sep  8 18:26 February.txt
```

## Explain in detail the different methods to change file/directory permissions in Linux (numbers/ugo)

We discussed the **ugo** method in the first part of this document and we use it to changed some permissions in the previous exercises, so that is covered.

Therefore I will a quick mention about it.

UGO refer to the permission groups as per below:

- **u** – Owner
- **g** – Group
- **o** – Others
- a – All users

And you have to use this groups in addition with **permission types**:

- **r** – Read
- **w** – Write
- **x** – Execute

Using both, types and groups, we can build a command to change permissions as in the previous exercises.

The potential Assignment Operators are + (plus) and – (minus); these are used to tell the system whether to add or remove the specific permissions.

Example:

```bash
#add read/write/execution permissions to the user
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod u+rwx February.txt
#add read/write permissions to groups
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod g+rw February.txt
#delete all permissions to others
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod o-rwx February.txt
```

**Using numeric references to set permissions**

Now that you understand the permissions groups and types this one should feel natural. To set the permission using binary references you must first understand that the input is done by entering three integers/numbers.

A sample permission string would be **chmod 640 file1**, which means that the owner has read and write permissions, the group has read permissions, and all other user have no rights to the file.

The first number represents the Owner permission; the second represents the Group permissions; and the last number represents the permissions for all other users. The numbers are a binary representation of the rwx string.

- ***r** = 4*
- ***w** = 2*
- ***x** = 1*

You add the numbers to get the integer/number representing the permissions you wish to set. You will need to include the binary permissions for each of the three permission groups.

Example:

```bash
#We have an example file with any permission
----------  1 genaroparedes  staff  0 Sep  8 19:09 example.txt

#add read/write/execution permissions to the user
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod 700 example.txt
#add read/write permissions to groups
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod 760 example.txt
#add execute permission to others
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod 761 example.txt

#It's not necessary step by step and this is the advantage for this method
#you just need put the three numbers together and that is all.
genaroparedes@GenaroParedes-MacBook-Pro devops % chmod 761 example.txt
```

## Create a new user and change the owner of the previous files to this user

**Owners and Groups**

I have made several references to Owners and Groups above, but have not yet told you how to assign or change the Owner and Group assigned to a file or directory.

You use the chown command to change owner and group assignments, the syntax is simple `chown owner:group filename`, **so to change the owner of file1 to user1 and the group to family you would enter `chown user1:family file1`*.*

Example:

```bash
#In this example we will change the owner of file1 to Haza
#and the group to adm
ecee@embedded-vm:~/example$ ls -l
total 0
-rw-r--r-- 1 ecee ecee 0 Sep  8 18:40 file1.txt
ecee@embedded-vm:~/example$ sudo chown Haza:adm file1.txt 
ecee@embedded-vm:~/example$ ls -l
total 0
-rw-r--r-- 1 Haza adm 0 Sep  8 18:40 file1.txt
```