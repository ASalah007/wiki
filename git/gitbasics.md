# Git Basics
* with every commit git saves a snapshot of every modified file that is  
  it creates a totally new file, and saves a references to each non modified file. 

## configuration 

* `git config --global` -> will edit the configuration file of the current machine user
* `git config --local` -> will edit the configuration file of the current git repo (default)
* `git config user.name <name>`
* `git config user.email <email>`
* `git config core.editor <nvim>`
* `git config init.defaultBranch <main>` -> the name of the first branch created on init
* `git config --list --show-origin` -> will list the configs that git read the last one is the applied one
* `git config <key>` -> will print the value of this specific config key
* `git config --show-origin <key>` -> to see what file it is declared in
* `git config --unset <key>`
* `git config --global diff.tool <vimdiff>` 

## Working with commits

* `git status --short` will show two columns beside every file  
  the first column indicates the status of the staging area  
  the second column indicates the status of the working tree  
  - M -> modified
  - A -> newly added files (normally in staging area)
  - R -> renamed
  - D -> deleted
  - ?? -> untracked files
* `git diff (--staged)` -> will show the modified changes unless --staged option is passed which will show the staged changes
* `git difftool` -> will show the modified changes in difftool
* `git rm` -> will remove the file from git and from your working tree
* `git rm --cached` -> this will tell git to stop tracking the file from now on but will not be removed from working tree
* `git add ./\*\*/file` -> this will add the file no matter how deep it is in the file system
* `git mv <f1> <f2>` -> this is equivalent to `mv f1 f2; git rm f1; git add f2`
* `git log -p -N` -> will show you the diff of last N commits
* `git log --stat` -> will give brief statistics of each commit
* `git log --pretty=<option>`-> option can be: oneline, short(default), full, fuller, format
* `git log -S <keyword>` this will get all the commits which edited something contains the <keyword>
* `git log -- path/to/file` this will get you all the commits containing this file

* `git commit --amend` -> this will commit every thing to the last commit, if nothing staged then only change commit message
* `git reset HEAD <file>` -> to unstage a file 
* `git checkout -- <file>` -> this will delete the unstaged changed of that file
* `git restore --staged <file>` -> this will unstage a file
* `git restore <file>` -> this will delete the modified file

## Working with remote 

* `git remote -v` -> will show you the remotes of this repo and where they came from
* `git fetch <remote>` -> will get the updates in the remote repo but will not merge it
* `git pull <remote>` -> will get the updates from remote and merge it
* `git push <remote> <branch>` 
* `git remote show <remote>` -> will show information about remote repo
* `git rename <old> <new>` -> if you want to rename local remote
* `git remote rm <remote>` -> to remove a remote from local
* `git tag --list <glob pattern>` -> to list tags that matches that pattern

lightweight tags -> just a pointer to specific commit<br>
annotated tags -> contains tagger name, email and date tagging message

* `git tag -a <tag_name> <commit_SHA>` -> this creates an annotated tag, if commit_SHA was not provided the last one is chosen
* `git show <tag_name>` -> will show information about specific tag

By default git push doesn't push tags you have to explicitly call `git push <remote> <tag_name>`

* `git push <remote> --tags` -> this will push all tags that not in remote 
* `git push --follow-tags` -> this pushes annotated tags only 
* `git tag -d <tag_name>` -> this deletes the tag from local repo
* `git push <remote> --delete <tag_name>` -> this deletes the tag from remote









