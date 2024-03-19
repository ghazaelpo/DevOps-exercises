# GIT - Commands

## Mario Armando Robles Espinoza & Genaro Hazael Paredes Ovalle

### clone:

- The clone commands takes a repository from a remote source such as GitHub, Gitlab or Bitbucket, and make a copy in your local environment.

example:

```bash
git clone https://gitlab.com/Mario_Genaro/Repository.git
```

### pull:

- pull command is used to merge and fetch the remote repository changes to your local environment.

example:

```bash
git pull
```

### push:

- The push command is the opposite of the pull command, that means the push will put your local modifications on your remote repository .

example:

```bash
git push
```

### add:

- git add is used to put your changes on the stage area.

example:

```bash
git add
```

### commit:

- when you want to record the changes to your repository, you should use de commit command.

example:

```bash
git commit
```

### merge:

- The merge command incorporates changes from the named commits (since the time their
    
    histories diverged from the current branch) into the current branch.
    

example:

```bash
git merge
```

### rebase:

- rebase do a reorganization fusion and reapply commits on top of another base tip.

example:

```bash
git rebase
```

### status:

- git status show the current branch, the paths that have differences between the working tree and the index file

example:

```bash
git status
```

### log:

- The log command displays all the commits, the output is given in reverse chronological order by default.

example:

```bash
git log
```

### checkout:

- if you want to move, or created new branches, you should use the checkout command

Example:

```bash
git checkout
```

### Difference between add and commit:

- the difference is that the add command put the changes on the staging area and the commit put the changes on the local repository

### Difference between merge and rebase:

- the difference between merge and rebase is that while merge preserves history as it happened, rebase rewrites it.