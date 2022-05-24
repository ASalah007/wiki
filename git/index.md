# Git / GitHub


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

## basic commands

* `git status --short` will show two columns beside every file  
  the first column indicates the status of the staging area  
  the second column indicates the status of the working tree  
  - M -> for modified
  - A -> for newly added files (normaly in staging area)
  - ?? -> for untracked files
* 

