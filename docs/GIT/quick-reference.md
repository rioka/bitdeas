---
title: Quick reference
---

# Quick reference

Quick recap and reminder of most frequently (by me!) used GIT commands


## How to...

### Clean working directory

`git clean` delete files which are not part of git.

Main cptions

|Option|Description|
|-|-|
|`-f`|Delete files from the repository|
|`-fd`|Delete files and folders from the repository|
|`-n`, `-dry-run`|*dry run*: Print out the list of files which will be removed|
|`-X`|Remove ignored (ie files in `.gitignore`) files|
|`-x`|Remove ignored and non-ignored (ie manually created ones) files|

### Delete a branch

```bash
git branch -d name_of_branch
```

### Remove a remote branch

```bash
git push origin --delete the_remote_branch
```

### Ccreate a branch from a given source

```bash
git checkout -b name-of-new-branch name-of-source-branch
```

### Create a new branch from changes in current branch

```bash
#first, stash changes
git stash save <message>

#then create a new branch from that stash
git stash branch name-of-new-branch stash@{0}
```

Or simply

```bash
# create and checkout a new branch keeping all changes in the previously current branch
git checkout -b name-of-new-branch
```

### Rename a branch

Rename current branch
```bash
# on branch to be renamed
git branch -m new-name
```

Rename a different (i.e. not current) branch

```bash
# from a different branch
git branch -m old-name new-name
```

Then

```bash
# delete the old-name remote branch and push the new-name local branch
# local branch will have no upstream after this command
git push origin :old-name new-name

# reset the upstream branch for the new-name local branch: switch to the branch and then
git push origin -u new-name
```

### Checkout a tag

Checkout a specific tag
```bash
git checkout  tags/name-of-tag
```

### List tags

List tags
```bash
# --list can be omitted
git tag --list
```

List tags matching a pattern
```bash
# list all tags starting with "v-"
git tag --list 'v-*'
```

### Create a tag
Create an annotated tag
```bash
git tag -a name-of-tag -m "<message>"
```

### Stash changes

```bash
git stash save -m "<message>"
```

### Check stash

View content of a stash
```bash
# show content of second-to-last stash
git stash show -p [stash@{1}]
```

View content of stash, filename only
```bash
# show filename of files stashed (second-to-last stash)
git stash show [stash@{1}] --name-only
```

### Apply stash

```bash
Apply a stash
git stash pop stash@{1}
```

### Search for a commit

```bash
# search in all git history
git grep <regexp> $(git rev-list --all)
```

### Unstage a file

```bash
git reset /path/to/file
```

### Revert committed changes in a file

```bash
git checkout <commit-hash> /path/to/file

# revert last commit
git revert HEAD

# revert specific commits
git revert <commit1> [<commitN>]
```bash
