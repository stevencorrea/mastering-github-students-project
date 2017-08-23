# git add

## Overview

The `git add` command is used to mark which file changes made by a user in a Git repository need to be recorded permanently. 
Each Git repo has a local database that stores all recorded changes made to the files within the repo.
The `git add` command is the first stage in permanently recording changes to this database.

## Description

The Git process for managing changes to files works on a three-stage process:

1. Modify files within the local Git repo
2. Stage the files (using `git add`), adding snapshots of the changes you have made to the staging area
3. Commit the files using `git commit`, which permanently stores the files as they are in the staging area to the Git directory 


When a file has been added or changed, the process of updating the repository is as follows:

`unstaged file (not tracked) -> add file to staging area -> commit file`

The staging area contains all files that are to be included in the next commit. 

The `git add` command is used to add new and modified files to the staging areas, ready to be included when the next `git commit` command is run.
The process can be run multiple times, building up a collection of modified files in the staging area ready to be included in a single `commit`

### Ignored Files
The `git add` command will not include ignored files, as defined in the `.gitignore` file, by default. 
Ignored files can be added with the `-f` (force) option.

### Removing Items from Staging Area

`git reset` will unstage the files from the staging areas,but preserve their contents in the repo (so files can be readded if needed)
`git reset HEAD <file>` can be used to unstage individual files

## Details

Git maintains an `index` of the current content to be added to the repository. 
The `index` holds a snapshot of the current working tree, and this snapshot is taken as the contents of the next commit. 
The 'git add' command updates this index of new or modified files. 

## Examples

- find details about untracked files and files currently in the staging area:

`git status`

- add a particular file

`git add example-file.txt`

- add all files of a particular type in the current directory

`git add *.txt`

- add all changed files in a directory and all sub-directories

`git add .`

- add an ignored file

`git add -f ignored-file.txt`

- remove all staged files

`git reset`

- remove an individual file from the staging area

`git reset -HEAD remove-me.txt`
