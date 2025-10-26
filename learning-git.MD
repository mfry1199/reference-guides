# Git and GitHub Guide

## Definitions

- Staging area: Where files go that are ready to be committed (after running "add")

## File Types

### .gitignore

Specify files/file types that should be ignored by git, remaining untracked and unseen. Good for any file that shouldn't be pushed to remote, but needs to be kept locally.

- ***.log:** Ignore log files
- **/build/:** Ignore build files such as from pyinstaller
- **./vscode:** Ignore vscode specific file

## Commands

### Setup and Configuration

- **`git init`:** Initialize a git repo locally (Create a git repo)
- **`git clone <GitHub URL>`:** Make an exact copy of a remote repo so that you have a local repo that's an exact copy
- **`git remote add origin <GitHub URL>`:** Connects local repo to remote repo in GitHub
- git config user.name / user.email <name> / <email>
- .gitignore

### Working Directory and Staging

- **`git pull`:** Fetch and merge changes from the remote repository (git fetch and then merge or rebase depending on configuration. Typically merge is set up)
- **`git pull --rebase`**: Rebases local commits onto remote version to add your changes to the most updated version
- **`git fetch`**: Download objects and refs from remote repository (Doesn't merge or rebase anything; Grabs info about what has changed in remote without changing anything)
- **`git fetch --prune`**: Cleans up remote tracking branches (local) to match actual remote branches
- **`git fetch --tags`**: Removes tracking tags locally that are no longer in remote repository
- git status
- git add <file> / git add --all
- git reset <file> 
- git checkout -- <file>
- git rm <file>: Remove file from tracking

### Committing and Versioning

- git checkout -- [file]: Discard changes in working directory
- git reset [file]: Unstage changes (remove from staging area)
- git rm [file]: Remove file from working directory and staging area
- git merge: Combines changes by pointing 2 commits to the same history effectively merging the codebases. Creates forks because initial separate of checkout remains and is pointed to by a new commit (Safest option for combining changes)
- git rebase \<target-branch\>: Combines changes by moving commits from one branch to target branch creating a linear commit history. Shouldnt be used in shared repos or main branches. Main benefit is readability and debugging and a cleaner history. If a rebase a feature branch it takes the commits and puts them on top of main or whatever branch I put.

### Branching and Merging

- git push origin v1.0.0
- git push: Upload local commits to the remote repository

### Stashing and Temporary Changes

- git tag v1.0.0: Adds a tag to a commit so that commit can have a version attached or some other label that makes it easier to roll between versions by checking out to them. Also able to add metadata using a few add on flags
- git tag -a v1.0 -m "First stable release": Allows metadata to be added to tag. Additional flags available.
  - -a: Adds annotated tag which saves the taggers info
  - -m: Specify a tagging message
- git tag -l "v1.8.5*": Searches for commits with this pattern so that different version series can be looked at
- git tag -a v1.2 9fceb02: Tag a commit using the commits checksum in case you need to tag an old commit
- git show v1.0.0: Shows tagged commit and the data it has

### Collaboration and Remotes

- **git diff:** Shows diff between current working directory and staging area
  - add **--staged:** Shows diff between staging area and last commit so you can see how committing added files will change the repository
  - add **<file_name>**: Shows diff between current working directory for that specific file and staging area.
- git diff v1.0.0..HEAD: Find diff of working directory compared to the tagged commit
- git diff v1.0.0...HEAD: Find diff of working directory compared to merge base of 2 branches. The merge base is the divergence point of the branches meaning this command finds what has changed since the branches separated.
- git diff v1.0.0..HEAD: Find the diff between working directory and tagged commit
- git log \<branch\>..origin/\<branch\>: Shows new commits on remote branch (Need to run git fetch first)
- **`git diff \<branch\> origin/\<branch\>`**: Shows code difference between local and remote branch (Need to run git fetch first)

### Inspection and Debugging

### Undoing and Recovery

## General Workflows

### Contributing and Rebasing in Shared Repo

1. git checkout main
2. git pull origin main
3. git checkout -b feature/my-new-feature
4. git add .
   git commit -m "Implement my new feature"
5. git fetch origin
  git rebase origin/main
6. git push -u origin feature/my-new-feature
7. Open PR from your feature branch into main in GitHub
8. git branch -d feature/my-new-feature
  git push origin --delete feature/my-new-feature
