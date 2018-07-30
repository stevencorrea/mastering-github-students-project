# Git Reset

_git reset_ is a commonly used command that reverts a local branch reference backwards in time to an older commit. In this writeup, I will try to break down a complex command and the flags you can use to make it more powerful and useful in certain situations.

To understand how _git reset_ works, we must first get our minds around the three areas that git uses when tracking changes. **HEAD**, a file that points to the most recent checked out commit, is often used as a fallback point when using _git reset_. Next, **Index** or the staging area for your files you've added to be committed to the repository. Finally, **Working Directory**, which includes any changes (new or modified files and folders) you might have locally, but are not yet reflected in the **Index** or **HEAD**.

_git reset_ can be used in a variety of ways. Advanced users might use the `--soft` or `--mixed (Default)` flags to resolve certain situations locally, while beginners might use it to simply wipe out and changes they have locally using the `--hard` flag.

_git reset_ takes flags, aliases such as **Head**, commit SHAs (short or long) and individual filenames as parameters.

To better understand the relationship between **Working Directory**, **Index**, and **HEAD** please see the image below.

![git workflow explanation chart](https://git scm.com/book/en/v2/images/reset-workflow.png)


## Basic Usage

### Reset Index while maintaining local files
In the event that you've added files to the index that you didn't intend, and you wanted to keep said files around, the default behavior of _git reset_ is to used `--mixed` mode. This resets the index while preserving your now untracked changes. This is most useful if you have several files staged for commit but need to pull one out for some last minute modifications.

> git reset HEAD

### Unstaging a file
Similarly to the above example, this will revert a file added to **Index** allowing you to make further changes or add it to an entirely new commit. You can think of resetting like this as unstaging a commit or committed file.

> git reset [filename]

### Undo the last commit
If those files that we didn't want to be committed actually made it to being committed, we can undo our last commit, then add, stage and commit the correct files.

> git reset --soft HEAD^

## Advanced Usage

### Start from Scratch
Common usage of _git reset_ is to start over from scratch and erase your local changes. To return to the point where your changes originated from in the branch, we can use **HEAD** as our reference point, and the `--hard` flag. Very uncommonly, **HEAD** will be in a detached state (where head is not pointed to the most recent commit of your remote). If this is the case, we can use 'origin/master' in the example below instead of **HEAD**. 

> git reset --hard HEAD

The --hard flag specifies that we do not want to keep any changes we've made changes to the branch's **Working Directory** or **Index**. For situations in which we'd like to keep some work committed locally to **Index**, or modified files in the **Working Directory**, we can use --soft or no flag at all (_git reset_ defaults to the `--mixed` flag). Note that using this flag is destructive and all local changes in the repo will be lost.

### Let me choose which changes I want
Similar to resolving a merge conflict, the `--patch` flag can be applied in situations where you want to pick and choose which changes of file contents you want to keep.

> git reset --patch [commit SHA, HEAD or filename]

## Other Information
While some of the functionality above can be dealt with using other tools, (see: [_git add_](https://git scm.com/docs/git add), [_git rm_](https://git scm.com/docs/git rm) git reset is a really powerful tool. Knowing when to use it is crucial and will only come with time and situations where it's needed. For less destructive and safer ways to reset or undo changes, see also [_git revert_](https://git scm.com/docs/git revert).
Here's a cheatsheet illustrating the differences of what gets modified depending on what flag is used:
![git reset cheatsheet](https://git scm.com/book/en/v2/git Tools-Reset-Demystified#_summary_8)

## References and further readings
[git reset](https://git scm.com/docs/git reset)
[SO: Difference between --soft, --hard and --mixed](https://stackoverflow.com/questions/3528245/whats-the-difference-between-git reset-mixed-soft-and-hard)
[Git Reset at Atlassian](https://www.atlassian.com/git/tutorials/undoing-changes/git reset)

## Advanced further reading
[Git Tools - Reset Demystified](https://git scm.com/book/en/v2/git Tools-Reset-Demystified#_git_reset)

