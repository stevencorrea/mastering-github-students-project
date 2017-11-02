# ```git checkout```

> ## Command Line Usage
>```git-checkout <branch> - Used to switch branches or restore working tree files.```

### Introduction
---
Branching allows users to work independantly on their own branched copies of a main repository without disrupting the workflow of the project to implement changes. Branches of the main repository can exist on a user's local machine, and remotely, as well.

Since branching is an integral part of a version control system such as Git, a mechanism to switch between branches must be implemented. In Git, the mechanism to achieve this goal is the `git-checkout` command. This command allows you to quickly and easily switch between different branches of the main repository to make changes that only affect the branch is currently _checked out_.


### Utilization
---
All repositories have at least one branch, the **master** branch, which is the default branch that is checked out when the repository is created. When a repository is cloned, or a new repository is created on the user's local machine, a master branch is automatically created and checked out. You can see this branch with the command `git branch`, which lists all branches of the repository:

```
$ git branch
* master
```
> **Note:** using `git branch` before any commits are made in a new repository will not give an output. There has to be at least one commit present before `git branch` will display any branches.

In the example above, only one branch is present, `* master`, because no other branches have been created yet. In order to check out a branch other than `* master`, one has to be present locally, or one or more branches must be **_fetched_** from a remote source to the local machine. (For a more detailed explanation of `git-fetch`, use the terminal command `info git-fetch`, or read the online GitHub documentation [git-fetch](https://help.github.com/articles/fetching-a-remote/) to learn more.)

After running the command to create a new branch called "another-branch" and verifying it has been added:
```
$ git branch another-branch
$ git branch
 another-branch
* master
```
The `git branch` command shows which branch is currently checked out by appending a `*` to the branch name.
The new branch can now be checked out with the command:

```
$ git checkout another-branch
Switched to branch 'another-branch'
```
After successful check-out of the new branch, any changes or commits made to the repository will not affect any of the other branches until the changes made in the current branch are **merged** with the master branch, or another remote branch. (For a more detailed explanation of merging, use the terminal command `info git-merge`, or read the online GitHub documentation [git-merge](https://help.github.com/articles/about-merge-methods-on-github/) to learn more.)

Checking-out a branch just updates the current working tree with the index and files of the branch you're checking-out. This is done by pointing HEAD at the branch. (_HEAD_ is just another name for the current branch.)

### Flags used with `git checkout`:
* `git checkout **-b|-B** <new_branch> [<start point>]` - creates a new branch and automatically checks it out. 
Using the `-B` flag acts exactly like `-b` if the branch doesn't exist. If the branch does exist, it is reset to the point provided by `<start point>`

* `$ git checkout -b <branch> --track <remote>/<branch>` - creates a new branch from the remote branch provided and tracks all changes that the remote undergoes

* `$ git checkout -f <branch>` force the branch change to occur, even if the working tree is different from HEAD. This is used to discard any changes that have been made locally.

### Other Uses
`git checkout` isn't limited to just checking-out branches. It can be also be used with commits and files.

### Using checkout with commits:
Being able to check-out commits is useful when you want to check out the state of a branch at a different time, such as when the branch first began to compare before and after snapshots of the changes you've made.
In order to check-out a commit, you'll need to know the ID of the commit. This can be found with the command `git log --oneline`, which provides the history of every ID, action taken, and message that was included on a single line for every commit on the branch.

#### Example:
```
$ git log --oneline
91bf0e9 Make a small format change to git-checkout.md.
5e15a01 Update git-checkout.md
d5cbdf1 Update git-checkout.md
57c236a Update git-checkout.md
:
```
The most recent commit will be at the top of the log. To revert to a previous commit, use the ID (the first number in the log) and type the `git checkout <commit ID>` command:

```
$ git checkout 57C23a
Note: checking out '57c236a'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 57c236a... Update git-checkout.md
```
This will place HEAD at the location of the commit ID that was checked-out. Since the HEAD is detached when you check-out a previous commit, you cannot perform any commits on changes that have been made while in this state. Checking out a commit is a **read-only** operation, and used to view previous commits only. You must return to master to commit the changes that have been made.
To return to the most recent commit, just return to the master:
```
$ git checkout master
Previous HEAD position was 57c236a... Update git-checkout.md
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
```
Now, you can either commit the changes that were made or reset back to the original state before the commit was checked out with `git reset`.

### Using checkout with files:
Checking out files uses the same procedure as checking out commits, with the exception that the file name must be included in the command: 
```git checkout <commit ID> <filename>```

Also, keep in mind that checking out an old version of a file **does** allow you to make changes to it that can be committed while the file is checked out. If you decide to discard the changes made to the file, you can revert back to the latest copy of the file with this command:
```git checkout HEAD <filename>```

### References
`info git-checkout` provides the command line documentation for the checkout command, but there are many online resources, as well:

GitHub help pages:

[GitHub](https://help.github.com/search/?utf8=%E2%9C%93&q=checkout)

Stackoverflow examples:

[Stackoverflow](https://stackoverflow.com/questions/1783405/how-do-i-check-out-a-remote-git-branch)

Great tutorial site for all things Git:

[www.atlassian.com](https://www.atlassian.com/git/tutorials/undoing-changes)

Online version of the command line info:

[git-scm.com](https://git-scm.com/docs/git-checkout)

The very best source for info on the checkout command:

[git checkout](https://github.com/KevinNiemeyer/kevin-niemeyer-git-checkout-contribution/edit/master/git-checkout.md) 









