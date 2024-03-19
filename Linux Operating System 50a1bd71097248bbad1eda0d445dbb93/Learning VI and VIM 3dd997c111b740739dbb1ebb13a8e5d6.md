# Learning VI and VIM

### Tell us a brief history (in your own words) about VIM and why I should learn vim

VIM is a free open-source, screen-based text editor program for unix. It is an improved clone of Bill Joy's vi. Vim's author, Bram Moolenaar, derived Vim from a port of the Stevie editor for Amiga(Computer). I would like to emphasize that VI and VIM are similar but not the same, because VI refers to *visual* and VIM to *visual improved*, both are visual text editors. This last one has improvement and new features to handle text files.

The main reason to learn it, is Linux uses a lot of configuration files, you'll often need to edit them and VIM is a great tool to do so.

For example in the previous homework "Learning SSH" we used it often because it was necessary modified many times ssh_config and sshd_config files for specific purposes.

Even you can create scripts and work with your code in the editor.

### What steps are needed to create a file with vim?

```bash
#Just type the below command followed by the name file
#You can choose any name that you want
genaroparedes@GenaroParedes-MacBook-Pro devops % vim examplefile.txt
#The editor will immediately open
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                                                                                                            
"examplefile.txt" [New]
```

### How many modes has vim to work and what do each of them do?

- **Normal mode**

Normal mode is the initial mode of the Vim editor. When you open a new file edit an existing one, it starts in normal mode by default. In normal mode, you cannot insert any character. Normal mode is also known as command mode because all the keystrokes you perform are interpreted as commands. For instance, if you press k, it will move the cursor position up one line instead of inserting the character “k”. Similarly, if you press yy, it will copy the current line instead of inserting “yy”. Also, in normal mode, the uppercase and lowercase letters are treated differently. For instance, pressing o create a new line for the text below the current cursor location, while pressing O creates a new line for text above the current cursor location

To access normal mode from other modes, press Esc key.

- **Insert mode**

Insert mode is where you can insert your text in the file. This mode inserts every character you type at the current cursor location.

- **Visual mode**

Visual mode allows you to select text so that you may perform certain operations (cut, copy, delete) on it.

**Changing the modes**

As already discussed, when you create or open a file in vim, it first opens in Normal mode.

In order to type any character, you will need to switch to the Insert mode. The most commonly used command to enter in to insert mode is “i”. To shift back to normal mode, press Esc.

To switch to the visual mode from Normal mode the most commonly used command to enter into insert mode is “v”.

To switch to the visual mode from Insert mode, first shift to Normal mode by pressing the Esc, then press v to get into the Visual mode.

![1-9.png](Learning%20VI%20and%20VIM%203dd997c111b740739dbb1ebb13a8e5d6/1-9.png)

### How do you edit a file using vim?

```bash
#Create a new archive 
genaroparedes@GenaroParedes-MacBook-Pro devops % vim examplefile.txt
~                                                                               
~                                                                               
~                                                                               
~                                                                               
~                                                                                                                                                            
"examplefile.txt" [New]
#And then go to insert mode as per explained above
#Just type "i" in the opened editor
~                                                                               
~                                                                               
~                                                                               
~                                                                                                                                                        
~                                                                                                                                                   
-- INSERT --
#Now you are able to write down
Hi there, this is an example how to edit on VIM                                                                     
-- INSERT --
```

### What commands can be used inside vim?

Most of them below are in command mode

- x - to delete the unwanted character
- u - to undo the last the command and U to undo the whole line
- CTRL-R to redo
- A - to append text at the end
- :wq - to save and exit
- :q! - to trash all changes
- dw - move the cursor to the beginning of the word to delete that word
- 2w - to move the cursor two words forward.
- 3e - to move the cursor to the end of the third word forward.
- 0 (zero) to move to the start of the line.
- d2w - which deletes 2 words .. number can be changed for deleting the number of consecutive words like d3w
- dd to delete the line and 2dd to delete to line .number can be changed for deleting the number of consecutive words

### What tips and tricks do you know using vim?

I specially know one, it is my favorite because is very useful. In the normal mode just type  / followed by the word that you are searching, example:

```bash
Hi there, this is an example how to edit on VIM.
I´m typing different words to show you how to use / for search a specific word:
Cat
Dog
Bird
Cow
Lion
Apple
Smartphone
~                                                                               
~                                                                               
~                                                                                                                                                                                                                                    
/show
#The cursor go to the word and will show you it
```

I like dd, dw and p commands:

- dd is for delete an entire line
- dw just delete the cursor selected
- p is for paste once you had use dw and dd

### Create 5 files using vim with the following naming convention: file01, file02....file05

```bash
#for create more than one file in just one line command
#we will use the below example
genaroparedes@GenaroParedes-MacBook-Pro devops % vim file{01..05}.txt
5 files to edit
#When you run this command, Vim editor will open and you have to save...
#the files one by one
~                                                                               
~                                                                                                                                               
~                                                                               
"file01.txt" 1L, 14B written
E173: 4 more files to edit
Press ENTER or type command to continue

#You can navigate between files using :n for the next file and :prev to go back
```

### Add to file01 28,333 lines that contains the text "Welcome to DigitalOnUs"

```bash
#For achive the mentioned task is neccesary uses yanked command in command mode
#Enter to the file using vim file1.txt
#Then in command mode type the number of lines you want yank followed by yy
#28333yy, finally paste using P
Welcome to DigitalOnUs
Welcome to DigitalOnUs
Welcome to DigitalOnUs
Welcome to DigitalOnUs
Welcome to DigitalOnUs
Welcome to DigitalOnUs
Welcome to DigitalOnUs
Welcome to DigitalOnUs
28333 lines yanked
```

### Add to file02 11,212 lines that contains your favorite fruit

```bash
#Use the previous method
Apple
Apple
Apple
Apple
Apple
Apple
Apple
Apple
Apple
11212 lines yanked
```