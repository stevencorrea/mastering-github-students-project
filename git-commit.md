# ```git commit```

## Introduction
```git-commit``` is used to record changes in a git repository.

## Description
Git is a distributed version control system. It simply means more than one person can work on a single file at the same time. However, in order for any version control system to work, we need to have a *way* of indicating/marking/creating these various versions of a file. This is where a **commit** becomes useful.

A commit is the mechanism used to mark a specific point as a point of reference.In Git, a commit is a **snapshot** of the git repository at that particular point in time. The snapshot being the *entire contents of every file* in the repository. But how do we create a commit? 

```git-commit``` is used to record changes in a git repository by creating commits. For ```git-commit``` to work, files to be committed must have been added to a special area called a *staging area*. This allows you to choose the specific files you want committed.

### Ways of specifying the content to be added to a commit

```git add new-file``` - adds new file to the staging area

```git add modified-file``` - adds modified file to the staging area

```git rm file-to-be-removed``` - removes file from the local directory and staging area.

```git commit -a``` - automatically adds changes from the modified files to the staging area and also remove files from the staging area that have been removed from the local directory.

### Usage

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

-edit 
### Options