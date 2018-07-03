# git cherry-pick

## Introduction

As the name suggests, the primary reason for the existence of 
`git cherry-pick` is to carefully choose what changes should be
applied to the repository and where they should be applied to. 
This is commonly used when a commit (change) needs to be applied
to another branch (copy) of the code.

## Detailed Overview

When things go according to plan, there is less of a need for 
`git cherry-pick`. However, when things go wrong, this command
is very useful. 

### Simple Example

Consider the example of working on a repository
with multiple branches (copies). It can be easy to get caught up
in development and make mistakes. 

Say you come across a problem
that you already solved and committed in another branch. You could
redo this change manually. However, if this was a major change the
extra work required could be time consuming. This is where `git cherry-pick`
comes in to play. 

Every commit has a corresponding SHA-1 value. As far as we are
concerned, this is just a long string of characters and numbers. The
purpose behind this is to uniquely identify each commit for purposes
such as this. 

In order to fix our issue, the first step would be to
navigate to the branch that contains the solution by typing 
`git checkout <branch_name>`. 

From here the command `git log` would 
be used to display all commits and their ids for that branch.

Once the commit you want to apply is found, it's id should be copied.

Then you navigate to the branch to fix and type `git cherry-pick <id>`.

### Complex Example

Because of the specificity of this command, it may seem like niche topic.
However, it is important to recognize that `git cherry-pick` will be used
more often as collaboration increases. 

For instance, say two separate 
developers (Alice and Bob) take their own branches from a repository to work
on separate features. 

Say Alice is significantly ahead and fixes a bug present
in the original code. 

If the Bob wants to save time and apply
that fix, he could merge (combine) Alice's branch into his. 

However, since they
are working on different features, this would result in unwanted changes in
Bob's branch. 

The solution would be for Bob to find the specific commit Alice
applied to make her fix and use it's id with `git cherry-pick`. 

This elegantly
saves Bob's time by using Alice's work without overwriting Bob's individual
progress.


## Flags

The following is the default use of the command.

`git cherry-pick <commit>`

As mentioned in the Detailed Overview, commit represents the id of 
the commit you want to merge into the current branch. For most situations
the default command will be more than enough. 

However, a common flag to use in the mentioned scenarios is the edit flag:

`git cherry-pick -e <commit>`

This allows you to edit the commit message similar to a normal commit.
This is useful in order to keep track of the changes made.

Another useful flag is the -x flag. 

`git cherry-pick -x <commit>`

This is similar to the -e flag. However, instead of changing the commit
message, it appends a new line to the old commit message. This new line
specifies where the commit was originally from. This is also useful for
keeping track of changes.

One important side note to recognize here is that although cherry-pick
duplicates the action of the commit from one area to another, it doesn't
duplicate the commit id (SHA-1). This means that the commit id's for both
will differ in order to keep identification consistent. This is why when
the -x flag is used, the commit id is appended.

The -n flag allows you to stage the commit instead of directly committing.
This is similar to completing git add for an ordinary file to be committed.

`git cherry-pick -n <commit>`

The --keep-redundant-commits flag is useful because it allows you to commit
the same item multiple times if needed. The default method prevents this which
makes a repeated edit to your repository difficult.

`git cherry-pick --keep-redundant-commits <commit>`

While there are more flags with potential use, those covered above will be
the mot likely to be used. If you would like more details, please click [here](https://git-scm.com/docs/git-cherry-pick).



