# git add

## Overview

The `git add` command is used to mark which file changes made by a user in a Git repository need to be recorded permanently. 
Each Git repo has a local database in the .git directory that stores all recorded changes made to the files within the repo.
The `git add` command is the first stage in permanently recording changes to this database.

## Description

The Git process for managing changes to files works on a three-stage process:

1. Modify files within the local Git repo
2. Stage the files (using `git add`), adding snapshots of the changes you have made to the staging area
3. Commit the files using `git commit`, which permanently stores the files as they are in the staging area to the Git directory 

Git monitors the state of all files within the repository by comparing each file to the version stored in the staging area and the permanent copy stored in the repo.

The user can see the state of the files in the repo by running `git status`. This will tell the user:
- which files have been modified, but not staged
- which files have been staged, ready to be committed permanently to the Git database.

The process of updating the files in a Git repository is as follows:

`modify files -> add files to staging area -> commit files`

The staging area contains all files that are to be included in the next commit. 

The `git add` command is used to add new and modified files to the staging areas, ready to be included when the next `git commit` command is run.

The `git add` process can be run multiple times, cumulatively building up a collection of modified files in the staging area ready to be included in a single `commit`

### Ignored Files
If there are particular files or folders that the user wants to permanently exclude from the Git database, the user can mark them to be ignored by adding them to the `.gitignore` file. Examples of files that the user may wish to ignore are log files, or compiled files created during a code build. 

Git does not track any changes to files listed in the `.gitignore` file. The `git status` command will not display any details regarding changes to these files, and the `git add` command will not include ignored files, as defined in the `.gitignore` file, by default. 

If required, the user can add ignored files with the `git add -f` (force) option.

### Removing Items from Staging Area

The staging area is a temporary location holding files ready to be committed permanently. If required, the user can remove any updated files from the staging area, so they will not be included in the next `git commit` update that preserves changes in the Git database.

The `git reset` command will unstage all files from the staging areas, but preserve their updated contents in the repo - so files can be readded if needed, and changes made are not lost.

The `git reset HEAD <file>` command can be used to unstage individual files.

Alternatively, if no changes are required (both staged and unstaged) then the command `git reset --HARD` can be used to revert all the files in the Git repo back to the last saved snapshot. *Warning*: this command will remove any changes made to files in the repo, either staged or unstaged - so all changes will be lost permanently.

Further details on the `git reset` command can be found here: [git reset documentation](https://git-scm.com/docs/git-reset).

## Examples

- To find details about both unstaged changed files and files currently in the staging area:

`git status`

- To add a specific file to the staging area:

`git add <filename>`

- Use wildcards to add all modified files of a particular type within the current directory:

`git add *.txt`

- To add all files in a directory and all sub-directories that have been modified:

`git add .`

- To add all new or modified files in the Git repo to staging:

`git add [-A-|-all]`

- To force an a specific ignored file to be added to the staging area:

`git add -f <filename>`

More complicated options that can be used with the `git add` command can be found in the [Git documentation](https://git-scm.com/docs/git-add)


## Links to more specific details about how Git tracks and stores file changes

The [Git documentation site](https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain) contains a detailed chapter on how Git manages to keep track of changed files and add them to the database)
