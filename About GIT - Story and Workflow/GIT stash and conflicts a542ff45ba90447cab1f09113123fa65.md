# GIT stash and conflicts

### GIT stash

`git stash` saves the uncommitted changes locally, allowing you to make changes, switch branches, and perform other Git operations. You can then reapply the stashed changes when you need them.

For example this command is useful when you are working in *features* branch and you need to solve an issue in *bug* branch, so you quickly move from *features* to *bug* but first you applied a `git stash` to save your uncommitted changes in *features* branch. Then you come back and can use `git stash pop` to restore those changes when you are back in the branch where you were working.

In my opinion is not good idea use this command when you are unsure how long you are going to be working on another branch because you might forget that you had done work there, it is a possibility, and then you re-make the work.

**GIT CONFLICT CASE**

I was working with two branches, *main* and *features.* I edited my file in *features* branch and then I wanted to switch to the another branch but I got the below error:

```bash
genaroparedes@GenaroParedes-MacBook-Pro devops % git branch
* features
  main
genaroparedes@GenaroParedes-MacBook-Pro devops % echo "adding text" > newfile.txt
genaroparedes@GenaroParedes-MacBook-Pro devops % git checkout main
error: Your local changes to the following files would be overwritten by checkout:
	newfile.txt
Please commit your changes or stash them before you switch branches.
Aborting
```

**APPROACH TO SOLVE THE ERROR**

I solved this error using `git stash`, this is a perfect situation to show how the command works.

```bash
#First we need to apply git stash to save the uncommitted changes applied
#in features branch
genaroparedes@GenaroParedes-MacBook-Pro devops % 
git stash save "stash example"
Saved working directory and index state On features: stash example

#Now you can switch to main branch without error
genaroparedes@GenaroParedes-MacBook-Pro devops % git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

#DO WHATEVER YOU HAD TO DO WITH MAIN

#Then you come back to features branch and apply a git stash pop to restore
#those changes
genaroparedes@GenaroParedes-MacBook-Pro devops % git checkout features
Switched to branch 'features'
genaroparedes@GenaroParedes-MacBook-Pro devops % git stash pop
On branch features
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   newfile.txt

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (c68afd06e9d6cedc4f288c47df6d75c2a15dfcc9)
genaroparedes@GenaroParedes-MacBook-Pro devops %
```

### GIT diff

`git diff` command is used in git to track the difference between the changes made on a file.

This command takes two inputs and reflects the differences between them. It is not necessary that these inputs are files only. It can be branches, working trees, commits, and more.

Let's see an example about this command and how to use it:

```bash
#For example we created a new file to work
genaroparedes@GenaroParedes-MacBook-Pro GITexample % touch example.txt

#After that we checked the uncommitted file status
git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	example.txt
genaroparedes@GenaroParedes-MacBook-Pro GITexample % git add example.txt 

#We make a change to the file 
genaroparedes@GenaroParedes-MacBook-Pro GITexample % echo "Adding some text" > example.txt 
#Finally we can see the changes using git diff
genaroparedes@GenaroParedes-MacBook-Pro GITexample % git diff
diff --git a/example.txt b/example.txt
index e69de29..7342e25 100644
--- a/example.txt
+++ b/example.txt
@@ -0,0 +1 @@
+Adding some text
```