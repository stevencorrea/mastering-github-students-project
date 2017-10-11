# `git stash`

### The `git stash` command allows you to temporarily save or "stash" changes you've made in your project so you can apply them later.

#### This is handy if you need to work on something on a different branch, but aren't ready to commit.

Git stash takes your uncommitted changes, saves them - then reverts your project to a clean working copy (from your last commit) - meaning no local changes.

A stash is just for your own personal use, so you can't push a stash to a remote repository.

After performing a `stash` you're able to use any other git features such as changing branches, creating new commits, etc. Then, when you're ready you can come back and apply your stashed changes.

Because you're able to have multiple stashes - it's a good idea to annotate them just like you would a message to your commits.

You can do that with" `git stash save "helpful message"`

This is a good practice because you'll be able to easily identify what each stash contains.

When you're ready to reapply your stashed changes you can do `git stash pop`. Pop will remove the changes from your stash and reapply them to your project.

By default `git stash pop` will reapply the most recent stash.

You can also do `git stash apply` to apply your stashed changes and keep them in your stash. You might use this if you want to apply the changes in more than one branch.

To see all of your stashes do `git stash list`.

You can specify which stash to apply by passing the identifier like this: `git stash pop stash@{1}`

Note the stash identifier uses a zero-index. So, the most recent stash would be {0}, then {1}, {2}, and so on.

By default, stash doesn't not include ignored files or new files in your project that haven't been staged.

Passing the `-u` option will include untracked changes in your stash.

To include everything, including ignored files, pass the `-a` (--all) option.

`git stash` = tracked files
`git stash -u` = tracked and untracked
`git stash -a` = tracked, untracked and ignored

To delete a stash do `git stash drop stash@{1}` and to delete all of your stashes do `git stash clear`

`git stash` is a handy tool for saving work on the fly without needing to commit.