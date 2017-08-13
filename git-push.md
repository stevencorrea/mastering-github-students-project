# Git Push

## How to Use Git Push

The command git push is used to push committed changes on your local branch to your remote repository. The following syntax is used when doing a push:
```
$ git push <remotename> <branchname>
```

Using `$ git push` without additional parameters sends all matching branches that have the same names as remote branches. You can also push to all tags if you use the following:
```
$ git push <remote> --tags
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

### Rename Branch

You can also rename a remote branch name by using the following:
```
$ git push <remote> <local>:<remotebranch>
```
This would push the local to your remote, but it would be renamed as remotebranch.

### Delete Branch

You can also delete a branch using similar syntax as the rename function:
```
$ git push <remote> :<branch>
```
Notice there is a space between the remote and :, this is basically saying, push no changes to the branch so it deletes the branch.

### Upstream Repos

You can add an upstream repository so that you can fetch all changes on a forked repository. By using the following command, you can fetch changes that you may not have locally:
```
$ git remote add upstream <remote_url>
```
