# Git Branches 

* when you add a file git computes a checksum(SHA-1) for each file and stores the file in the repo
* git refer to the file as blob
* when you run git commit git checksums each subdirectory and stores them as tree objects then it creates a commit object that refers to the tree object.

* A branch in git is nothing but a pointer to the last commit, when you add another the pointer points to the new commit
* `git branch <branch>` -> this will create a branch that points to the last commit.
* git keeps track of which branch you are currently in by the **HEAD** pointer which refer to the branch pointer you are in.
* `git checkout <branch>`
* `git log <branch>` -> will show the log of that branch
* `git log --all` -> will show the log of all branches
* `git merge <branch>`

when you merge a branch that all of its commits are directly ahead of master branch in one straight line, git **fast-forward**
the master branch to the new branch.

* `git branch -d <branch>` -> deletes the branch
* when you merge a branch to master what it does it creates a new commit (merge commit) that points to the two commits(master commit and branch commit)
* `git branch -v` -> will show you the branches with the last commit
* `git branch --move <old> <new>` -> locally rename a branch
* `git push --set-upstream origin corrected-branch-name` -> to push branch rename to remote
* `git push origin --delete bad-branch` -> to delete a branch in remote

remote-tracking branches are pointers to the remote Branches for example origin/master 

* `git push origin local-branch:remote-branch`
* `git checkout -b branch-name origin/branch-name` -> this will give you editable copy of the branch-name
* or `git checkout --track origin/branch-name`
* `git branch -vv` -> will tell you which branch you are tracking
* `git rebase master`
* `git rebase --onto master branch1 branch2` -> if you want to rebse branch2 as if it was diverged directly from master not branch1
* 
