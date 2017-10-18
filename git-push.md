# Git Push

## How to Use Git Push

The command git push is used to push committed changes on your local branch to your remote repository. The following syntax is used when doing a push:
```
$ git push <remotename> <branchname>
```

Example of pushing to the master repository:
```
$ git push origin master
```

Using `$ git push` without additional parameters sends all matching branches that have the same names as remote branches. You can also push to all tags if you use the following:
```
$ git push <remote> --tags
```

Example of pushing all tags to the origin:
```
$ git push origin --tags
```

If you are receiving the following error when attempting to push changes to a remote repository, this simply means that you are missing upstream changes and must do a "fetch" for the changes first before pushing new changes to the reposirtory.

Error:
```
non-fast-forward updates were rejected
```
Look for information on `git pull` for how to fetch changes from an upstream remote. 

## Common Uses

### Push to Master

The most common use of git push is the push to master. The following can be user to push all committed changes to the master remote repository: 
```
$ git push origin master
```

### Delete Branch

You can also delete a remote branch using similar syntax as the rename function:
```
git push origin --delete branch_being_deleted
```
This will delete the remote branch named "branch_being_deleted" in your remote repository.

### Rename Branch

You can also rename a remote branch name by using the following, essentially we will be using some of the syntax from deleting an existing branch and at the same time creating a new one:
```
$ git push origin :old_branch new_branch
```
This would essentially push the local repository to your remote repository, delete the existing branch (old_branch) and create a new branch (new_branch) with  the name specified.

### Upstream Repos

You can add an upstream repository to your current repository so that you can fetch changes from the upstream repository using the fetch command. By using the following command, you can add an upstream repository:
```
$ git remote add upstream <remote_url>
```
