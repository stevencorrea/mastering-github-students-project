# ```git commit```

## Introduction
```git-commit``` is used to record changes in a git repository.

## Description
Git is a distributed version control system. It simply means more than one person can work on a single file at the same time. However, in order for any version control system to work, we need to have a *way* of indicating/marking/creating these various versions of a file. This is where a **commit** becomes useful.

A commit is the mechanism used to mark a specific point as a point of reference.In Git, a commit is a **snapshot** of the git repository at that particular point in time. The snapshot being the *entire contents of every file* in the repository. But how do we create a commit? 

```git-commit``` is used to record changes in a git repository by creating commits. For ```git-commit``` to work, files to be committed must have been added to a special area called a *staging area*. This allows you to choose the specific files you want committed.

### Ways of specifying the content to be added to a commit

1. ```git add new-file``` - adds new file to the staging area

1. ```git add modified-file``` - adds modified file to the staging area

1. ```git rm file-to-be-removed``` - removes file from the local directory and staging area.

1. ```git commit -a``` - automatically adds changes from the modified files to the staging area and also remove files from the staging area that have been removed from the local directory.

## Usage

```git commit -m "commit message"``` - performs a commit with the value in quotes as the commit message. You should edit it to be meaningful to you.

The terminal will then output

```git-bash

[master 6a683b1] <commit message>
 1 file changed, 2 insertions(+), 2 deletions(-)

```
**master** stands for the branch on which the commit has been done.
**6a683b1** are the first 7 characters for the hash(a 40 character name used to uniquely identify a commit).
**<commit message>** stands for your unique commit message
Thereafter, the number of files, together with the changes performed on each are listed.

```git commit --file=<file>``` - performs a commit while getting the commit message from the file <file>.

```git commit --author=<author>``` - performs a commit while overriding the commit author with <author>.

```git commit --date=<date>``` - performs a commit while overriding the author date with <date>.

```git commit [--file=<file>| -m <msg> ]``` - performs a commit while allowing you to edit the messages taken from the various sources e.g. file, commit message.

```git commit -q -m "commit message"``` - the ```-q``` or ```--quiet``` flag performs a commit while suppressing the commit summary message.

```git commit --dry-run -m "commit message"``` - the ```dry-run``` option doesn't perform the commit but allows you to see what would happen if a real commit was done. It will show you the files that will be commited and the ones that will not. The files that will not be committed are the modified files and the untracked files. The modified files are the ones that had been added to the staging area before changes were made to them. The untracked files are the ones that have never been added to the staging area.

```bash

touch file1 file2 file3
git add .
git commit file1

```
This will only commit file1 while leaving the other changes eg. file2 and file3 in the staging area. Thus, it allows you to commit only certain changes from the staging area.

```git commit``` - is preferred to commiting using the ```-m``` option. This is because it allows you to write your commit in the default editor that is started. Thus it gives you the opportunity to write better commits which would be more meaningful to you later especially when you find yourself in a fix and would really want to know the exact changes you made in each commit. Usually, it is preferred to write a small summary of about 50 characters or less. Thereafter, you skip one line then list all the changes that are taking place in that commit. The commit is performed when you save and close the editor.

Checkout the [manual](https://git-scm.com/docs/git-commit) for a full list of options and flags.