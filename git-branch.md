#### Understanding the `Git branch` command

# When using Git, a `branch` can be thought of as simply a movable pointer.

Whenever you make a change (commit) using Git within a repository you are provided with a `"master"` branch automatically, which points to the last commit you made. Every time you perform a commit, this master branch moves forward. 

The pointer itself is referred to as the `HEAD`- which points to the `current` branch, i.e. the direction in which your workflow is headed. 

When a new branch is created (and given a suitable title) the user can then move the HEAD, to the newly created branch, and this will provide the user with a new direction in which to take their workflow. This new branch will now move forward automatically with each commit.

The user can at any time switch back to the master branch to make changes, and will then move forward with each new commit from an older version of the repository- as both sets of commits will be isolated in separate branches. 

You can find out which branch the HEAD is pointing at by using the following command:

  ```
  cat .git/HEAD
  ```

## Getting started with the Git Branch command

One reason that a developer may wish to create a new branch would be to test a new feature. The feature itself may or may not be included in the final project. A good name for this branch could be "testing-branch" for example. This branch can be created using the `git branch` command as follows: 

  ```
  git branch testing-branch
  ```

Simply typing `git branch` into the terminal will now show the presence of two branches within Git: "master", and "testing-branch." An asterisk will appear next to the current branch.

  ```
  git branch
  ```

Which should give a result that looks like this:

  ```
  * master
    testing-branch
  ```

Adding the flag `-a` to the command will also list the branches that exist on your local device, but this time include remote-tracking branches as well. Remote-tracking branches can be thought of as bookmarks to remind you where the branches in your remote repositories were the last time you connected to them. 

  ```
  git branch -a
  ```

If for any reason you need to change the name of a branch, lets say from "testing-branch" to "john-testing-branch" (to make your identity clear to fellow contributors), using the `-m` option as follows will do this:

  ```
  git branch -m testing-branch john-testing-branch
  ```

## When and how to delete a branch

As mentioned previously, it is common for branches to be created for developing a new feature. If the code for the new feature is fully developed and ready to become a permanent fixture within the master branch, the programmer will perform a process called merging, i.e. to "merge" commits present on the new feature branch, with those found on the master. 

When such a merge occurs it is good practice to then delete the new feature branch from which the commits were "pulled" to help maintain a workspace free from un-necessary clutter. Deleting a `local` branch is done using the `-d` option with the git branch command:

  ```
  git branch -d john-testing-branch
  ```

In the event that you try to delete a branch when the code present on it has not yet been merged with the master an error message will occur that warns you of the potential loss of unmerged commits. By simply capitalizing the previous flag, the branch will be deleted irrespective of its merged status. This is not regarded as a "safe" way to delete branches and should only be used with caution to avoid losing valuable code. See below:

  ```
  git branch -D john-testing-branch
  ```

Deleting a `remote` branch uses a slightly different command, note the use of `:`

  ```
  git push origin :branch-to-delete
  ```

## Help finding a commit

One of the very helpful aspects of Git is that it is carefully designed to protect against the loss of your data. Lets say you are currently on your master branch, and you wish to find out if a particular desirable commit from a new feature branch was merged to the master. Using the aforementioned `-d` will of course issue a warning when you try to delete the new feature branch (if there are unmerged commits present on it), but there is another way to find the location(s) of a specific commit.
Using the `--contains` flag will output a list of all branches that contain the commit. Using the flag as follows, making sure to include the unique code associated with the commit in question, we can easily find out where the commit is present within the existing branches. Take the commit `f3b1808` as an example and see how the command is entered below:

  ```
  git branch --contains f3b1808
  ```


## A note on Git Branch tracking

A `tracking branch` in Git is a local branch that is connected to a remote branch- referred to as the upstream branch. When you push (send) and pull (fetch) commits on your local branch, this automatically pushes and pulls to the remote branch which the local branch is tracking. Sometimes a developer will find that they need to amend the upstream branch they are tracking, and this can be done with the help of the `-u` option. Lets take the branch example of "john-testing-branch" once again, and lets set it to track the upstream origin branch. Note the position of the flag this time around:

  ```
  git branch john-testing-branch -u origin
  ```

The `-vv` option can then be used to provide a list of your local branches, outlining the upstream remote branches that each of your local branches are tracking. This output will also outline if your local branches are ahead, behind or both in their commits.

  ```
  git branch -vv
  ```

See below that local branches "john-testing-branch" and the "master" are now both tracking the remote origin, with "john-testing-branch" ahead of the origin by 6 commits. Both local branches can now push and fetch commits to and from the origin- often located on Github.

  ```
* john-testing-branch                  97cc9a8 [origin/john-testing-branch: ahead 6] updated john-testing-branch
  master                               3bad51f [origin/master] Initial commit
  ```

## The real power of `git branch`

Understanding and mastering the `git branch` command will give any developer a dynamic and unique tool with which to bring about the `parallel evolution` of a project. 

John Gribbin
07/27/2017
Career Path 5: Fullstack Engineer