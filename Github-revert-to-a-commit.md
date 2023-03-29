---  
share: true  
tag: public  
---  
[stackoverflow](https://stackoverflow.com/questions/1463340/how-can-i-revert-multiple-git-commits)  
  
_Expanding what I wrote in a comment_  
  
The general rule is that you should not rewrite (change) history that you have published, because somebody might have based their work on it. If you rewrite (change) history, you would make problems with merging their changes and with updating for them.  
  
So the solution is to create a _new commit_ which **reverts changes** that you want to get rid of. You can do this using [git revert](http://www.kernel.org/pub/software/scm/git/docs/git-revert.html "git-revert(1) Manual Page - Revert an existing commit") command.  
  
You have the following situation:  
  
A <-- B  <-- C <-- D                                  <-- master <-- HEAD  
  
(arrows here refers to the direction of the pointer: the "parent" reference in the case of commits, the top commit in the case of branch head (branch ref), and the name of branch in the case of HEAD reference).  
  
What you need to create is the following:  
  
A <-- B  <-- C <-- D <-- [(BCD)-1]                   <-- master <-- HEAD  
  
where `[(BCD)^-1]` means the commit that reverts changes in commits B, C, D. Mathematics tells us that (BCD)-1 = D-1 C-1 B-1, so you can get the required situation using the following commands:  
  
```  
$ git revert --no-commit D  
$ git revert --no-commit C  
$ git revert --no-commit B  
$ git commit -m "the commit message for all of them"  
```  
  
Works for everything except merge commits.  
  
---  
  
Alternate solution would be to [checkout](http://git-scm.com/docs/git-checkout "git-checkout(1) Manual Page - Checkout a branch or paths to the working tree") _contents_ of commit A, and commit this state. Also works with merge commits. Added files will not be deleted, however. If you have any local changes `git stash` them first:  
  
```  
$ git checkout -f A -- . # checkout that revision over the top of local files  
$ git commit -a  
```  
  
Then you would have the following situation:  
  
A <-- B  <-- C <-- D <-- A'                       <-- master <-- HEAD  
  
The commit A' has the same contents as commit A, but is a different commit (commit message, parents, commit date).  
  
---  
  
Alternate [solution by Jeff Ferland, modified by Charles Bailey](https://stackoverflow.com/questions/1463340/revert-multiple-git-commits/1463390#comment1312779_1463390) builds upon the same idea, but uses [git reset](https://www.kernel.org/pub/software/scm/git/docs/git-reset.html "git-reset(1) Manual Page - Reset current HEAD to the specified state"). Here it is slightly modified, this way WORKS FOR EVERYTHING:  
  
```  
$ git reset --hard A  
$ git reset --soft D # (or ORIG_HEAD or @{1} [previous location of HEAD]), all of which are D  
$ git commit  
```