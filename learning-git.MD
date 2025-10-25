# Git and GitHub Guide

## Definitions

- Staging area: Where files go that are ready to be committed (after running "add")

## General

### Git Ignore (.gitignore)

- *.log: Ignore log files
- /build/: Ignore build files such as from pyinstaller
- ./vscode: Ignore vscode specific file

## Commands

### Diff-ing

- git diff: Shows diff between current working directory and staging area
- git diff --staged: Shows diff between staging area and last commit so you can see how committing added files will change the repository
- git diff <file_name>: Shows diff between current working directory for that specific file and staging area.

### Local

- git reset [file]: Unstage changes (remove from staging area)
- git checkout -- [file]: Discard changes in working directory
- git rm [file]: Remove file from working directory and staging area
- git tag v1.0.0: Adds a tag to a commit so that commit can have a version attached or some other label that makes it easier to roll between versions by checking out to them. Also able to add metadata using a few add on flags
- git diff v1.0.0..HEAD: Find the diff between working directory and tagged commit
- git tag -a v1.0 -m "First stable release": Allows metadata to be added to tag. Additional flags available.
  - -a: Adds annotated tag which saves the taggers info
  - -m: Specify a tagging message
- git tag -l "v1.8.5*": Searches for commits with this pattern so that different version series can be looked at
- git push origin v1.0.0
- git show v1.0.0: Shows tagged commit and the data it has
- git tag -a v1.2 9fceb02: Tag a commit using the commits checksum in case you need to tag an old commit
- git merge: Combines changes by pointing 2 commits to the same history effectively merging the codebases. Creates forks because initial separate of checkout remains and is pointed to by a new commit (Safest option for combining changes)
- git rebase \<target-branch\>: Combines changes by moving commits from one branch to target branch creating a linear commit history. Shouldnt be used in shared repos or main branches. Main benefit is readability and debugging and a cleaner history. If a rebase a feature branch it takes the commits and puts them on top of main or whatever branch I put.
- git diff v1.0.0..HEAD: Find diff of working directory compared to the tagged commit
- git diff v1.0.0...HEAD: Find diff of working directory compared to merge base of 2 branches. The merge base is the divergence point of the branches meaning this command finds what has changed since the branches separated.

### Remote

- git pull: Fetch and merge changes from the remote repository (git fetch and then merge or rebase)
- git push: Upload local commits to the remote repository
- git fetch: Download objects and refs from remote repository (Doesn't merge or rebase anything; Shows you how remote has changed without changing anything in working directory)
- git fetch --prune: Cleans up remote tracking branches (local) to match actual remote branches
- git log \<branch\>..origin/\<branch\>: Shows new commits on remote branch (Need to run git fetch first)
- git diff \<branch\> origin/\<branch\>: Shows code difference between local and remote branch (Need to run git fetch first)
- git fetch --tags: Removes tracking tags (local) that are no longer in remote repository
- git pull --rebase: Rebases local commits onto remote version to add your changes to the most updated version
- git remote add origin \<remote_http_url\>: Adds a remote repo to local repo


# 1. Make sure you're on the main branch
git checkout main

# 2. Update your local view of the remote repository
git fetch origin

# 3. Pull the latest changes into your local main (optional, but keeps main usable)
git pull origin main

# 4. Create and switch to a new feature branch
git checkout -b feature/my-new-feature

# 5. Make code changes, stage, and commit them
git add .
git commit -m "Implement my new feature"

# 6. Rebase your feature branch onto the latest remote main before pushing
git fetch origin
git rebase origin/main

# 7. Push your rebased feature branch to the remote
git push -u origin feature/my-new-feature

# 8. Open a pull request (PR) from your feature branch into main
# (done via GitHub, GitLab, etc.)

# 9. Delete local and remote feature branches after merge
git branch -d feature/my-new-feature
git push origin --delete feature/my-new-feature

