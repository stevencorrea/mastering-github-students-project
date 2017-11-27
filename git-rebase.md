`git rebase` is one of two Git commands that helps in integrating changes from one branch onto another. The other command that helps with integrating changes is `git merge`. Merge is always a forward moving change record. Alternatively, rebase has powerful history rewriting features. Rebase itself has 2 main modes: "manual" and "interactive" mode. 

The git rebase command allows you to easily change a series of commits, modifying the history of your repository. You can reorder, edit, or squash commits together.

Typically, one would use git rebase to:

1) Edit previous commit messages
2) Combine multiple commits into one
3) 	Delete or revert commits that are no longer necessary

Common options available while rebasing:

| Option        | Description |
| ------------- |------------- |
| pick      |pick simply means that the commit is included. Rearranging the order of the pick commands changes the order of the commits when the rebase is underway. If you choose not to include a commit, you should delete the entire line. |
| reword      | The reword command is similar to pick, but after you use it, the rebase process will pause and give you a chance to alter the commit message. Any changes made by the commit are not affected. |
| edit | If you choose to edit a commit, you'll be given the chance to amend the commit, meaning that you can add or change the commit entirely. You can also make more commits before you continue the rebase. This allows you to split a large commit into smaller ones, or, remove erroneous changes made in a commit. |
| squash | This command lets you combine two or more commits into a single commit. A commit is squashed into the commit above it. Git gives you the chance to write a new commit message describing both changes. |
| fixup | This is similar to squash, but the commit to be merged has its message discarded. The commit is simply merged into the commit above it, and the earlier commit's message is used to describe both changes.|
| exec | This lets you run arbitrary shell commands against a commit. |   

Git rebase interactive is when git rebase accepts an `-- i` argument. This stands for "Interactive." Without any arguments, the command runs in standard mode.

Git rebase in standard mode will automatically take the commits in your current working branch and apply them to the head of the passed branch.

Running git rebase with the -i flag begins an interactive rebasing session. Instead of blindly moving all of the commits to the new base, interactive rebasing gives you the opportunity to alter individual commits in the process. This lets you clean up history by removing, splitting, and altering an existing series of commits.
