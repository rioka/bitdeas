---
title: Some aliases
---

# Some aliases

!!! note 
    Aliases are saved in `.gitconfig`, in user home folder, e.g. `%UserProfile%` in Windows, or `~` in Linux.

Here are some common aliases I use

|Entry|Description|
|-|-|
|`st = status`| Shortcut for `git status`|
|`cl = clone`| Shortcut for `git clone`|
|`co = checkout`| Shortcut for `git checkout`|
|`ci = commit`| Shortcut for `git commit`|
|`com = checkout master`|Shortcut for `git checkout master`|  
|`cob = checkout -b`|Shortcut for `git checkout -b`; create a branch and check it out|
|`delb = branch -D`|Delete a branch|  
|`pl = pull`|Shortcut for `git pull`|
|`plp = pull --prune`|Pull and prune local branches|
|`ps = push`|Shortcut for `git push`|
|`psup = push`|Shortcut for `git push upstream origin`; push and create branch in remote origin|
|`lo1g = log --oneline --graph`||  
|`lobd = log --branches --date-order`||
|`showalias = config --get-regexp alias`||
|`unstage = reset HEAD --`|delete last commit, but keep file; so you get back 1 commit, but do not lose anything|
|`mt = mergetool`| Run mergetool to solve conflicts|