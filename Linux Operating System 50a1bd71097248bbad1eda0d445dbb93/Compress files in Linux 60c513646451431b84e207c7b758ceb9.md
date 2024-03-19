# Compress files in Linux

## tar

The tar command is not specifically a compression command. It’s generally used to pull a number of files into a single file for easy transport to another system or to back the files up as a related group. It also provides compression as a feature, which makes a lot of sense, and the addition of the z compression option is available to make this happen.

```bash
#The command to use is tar, where -c flag means create an archive and -f flag...
#means the file name
tar -cf
#You must specifies the name for your file and the files that you want...
#To place in a single file 
tar -cf file.tar file1.txt file2.txt

#The result is the below:
```

![Screen Shot 2021-09-12 at 22.34.08.png](Compress%20files%20in%20Linux%2060c513646451431b84e207c7b758ceb9/Screen_Shot_2021-09-12_at_22.34.08.png)

```bash
#We will delete file1.txt and file2.txt to show an example
genaroparedes@GenaroParedes-MacBook-Pro devops % rm file1.txt file2.txt
#Files deleted
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
February.txt	README.md	file3.txt
January.txt	file.tar	file4.txt

#If you want decompress the file.tar created, just follow the following:
#-x flag to extract and -f name file
genaroparedes@GenaroParedes-MacBook-Pro devops % tar -xf file.tar
#Files again in the directory 
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
February.txt	README.md	file1.txt	file3.txt
January.txt	file.tar	file2.txt	file4.txt
```

## gz

Gzip compresses only single files and creates a compressed file for each given file. By convention, the name of a file compressed with Gzip should end with either .gz or .z.

```bash
genaroparedes@GenaroParedes-MacBook-Pro devops % gzip file1.txt file2.txt
#Compressed file result:
```

![Screen Shot 2021-09-12 at 23.23.10.png](Compress%20files%20in%20Linux%2060c513646451431b84e207c7b758ceb9/Screen_Shot_2021-09-12_at_23.23.10.png)

```bash
#If you want decompress, use the following example:
#gunzip filename
#file1
genaroparedes@GenaroParedes-MacBook-Pro devops % gunzip file1.txt.gz
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
February.txt	README.md	file1.txt	file3.txt	fileb.tar.gz
January.txt	file.tar.gz	file2.txt.gz	file4.txt
#file2
genaroparedes@GenaroParedes-MacBook-Pro devops % gunzip file2.txt.gz
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
February.txt	README.md	file1.txt	file3.txt	fileb.tar.gz
January.txt	file.tar.gz	file2.txt	file4.txt
```

## bz2

Bzip2 is a well known compression tool and it’s available on most if not all the major Linux distributions, you can use the appropriate command for your distribution to install it.

```bash
#We will use file1.txt and file2.txt as example
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
README.md	file1.txt	file2.txt	file3.txt	file4.txt
#For use this tool compression is just necessary use bzip2 command...
#following by the file name, you can add n files name
genaroparedes@GenaroParedes-MacBook-Pro devops % bzip2 file1.txt file2.txt
#Result 
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
README.md	file1.txt.bz2	file2.txt.bz2	file3.txt	file4.txt
genaroparedes@GenaroParedes-MacBook-Pro devops %

#For decompress just use bunzip2 command and the same structure
genaroparedes@GenaroParedes-MacBook-Pro devops % bunzip2 file1.txt.bz2 file2.txt.bz2
genaroparedes@GenaroParedes-MacBook-Pro devops % ls                                 
README.md	file1.txt	file2.txt	file3.txt	file4.txt
```

## tar.gz

```bash
#We can create a compressed file directly in just one step
genaroparedes@GenaroParedes-MacBook-Pro devops % tar -czf fileb.tar.gz file3.txt file4.txt
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
February.txt	README.md	file1.txt	file3.txt	fileb.tar.gz
January.txt	file.tar.gz	file2.txt	file4.txt

#If you want decompress just use the below command:
genaroparedes@GenaroParedes-MacBook-Pro devops % tar -xzf fileb.tar.gz 
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
February.txt	README.md	file1.txt	file3.txt	fileb.tar.gz
January.txt	file.tar.gz	file2.txt	file4.txt
```

## tar.bz2

```bash
#We can create a compressed file directly in just one step
genaroparedes@GenaroParedes-MacBook-Pro devops % tar -cjf newfile.tar.bz2 file1.txt file2.txt 
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
README.md	file2.txt	file4.txt
file1.txt	file3.txt	newfile.tar.bz2
#If you want decompress just use the below command:
genaroparedes@GenaroParedes-MacBook-Pro devops % rm file1.txt file2.txt 
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
README.md	file3.txt	file4.txt	newfile.tar.bz2
genaroparedes@GenaroParedes-MacBook-Pro devops % tar -xjf newfile.tar.bz2 file1.txt file2.txt
genaroparedes@GenaroParedes-MacBook-Pro devops % ls
README.md	file2.txt	file4.txt
```