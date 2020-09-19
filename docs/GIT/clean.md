---
title: Git clean
---

# What it does

`git clean` delete files which are not part of git.

## Main cptions

|Option|Description|
|-|-|
|`-f`|Delete files from the repository|
|`-fd`|Delete files and folders from the repository|
|`-n`, `-dry-run`|*dry run*: Print out the list of files which will be removed|
|`-X`|Remove ignored (ie files in `.gitignore`) files|
|`-x`|Remove ignored and non-ignored (ie manually created ones) files|

