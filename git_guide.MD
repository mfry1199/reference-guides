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

### Remote

- git pull: Fetch and merge changes from the remote repository
- git push: Upload local commits to the remote repository
- git fetch: Download objects and refs from remote repository
