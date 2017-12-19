# ```git merge ```
<hr>

The ```git merge``` command combines two or more repository histories together by reconstructing the commit history of the current branch to include any commits that have been added or modified by the specified branch or commit. It is also the second command used in the two step command ```git pull```, which is a combination of ```git fetch``` and ```git merge``` and commonly used to retrieve the changes from a specified remote or branch and integrate those changes into a local repository.

While working within a repository with multiple branches and a main "master" branch, a developer may want to  commit final changes to the master branch before pushing to a remote copy of the repository's corresponding branch. ```git merge``` is used in the case of integrating changes made on other branches into the current HEAD by reorganizing its commit history to include the commits made in the referenced branch and updating the "pointer" of the current HEAD to point at the most recent commit, which should contain the changes of the specified branch.

```git merge``` will perform the appropriate merge strategy depending on the the quantity of commits to merge by default, but a merge strategy can be specified by using the ```-s``` or ```--strategy``` option and naming the 

### Syntax

>*git merge* [--option][<commit>...] <br>
 *git merge* --abort <br>
 *git merge* --continue

## Simple example of merging a branch into the current branch

	git checkout master
	git merge feature-branch

This series of commands is commonly used when a developer has finished working on a branch and has made the necessary commits on that branch, and is ready to commit those changes into the specified branch's parent branch. Even though the commit histories between the master branch and the branch to be merged may have changed, ```git merge``` will attempt to combine them as two commits and create a new commit on master containing the updates to the working tree and commit history from the merged branch. Merging strategies will be discussed briefly later on, but covering each one is beyond the scope of this article.

### Breakdown of merging process

After using ```git checkout``` to check out into the master branch, (the branch that will be pushed to the remote) running ```git merge``` followed by the name of the branch, in this case *feature-branch*, to merge into the current branch will attempt to merge the two together and publish the result as a new commit on the master branch. If there have been commits made on either branch since the child branch was created, the commit history of the master branch will most likely need to be updated with the new commits added to the child branch in order to keep the master branch up to date with the current state of the repository. A successful merge will with either result in a *fast-forward* or a *merge commit* on the currently checked out branch, which is determined by the ```git merge``` command when it looks for changes in commit histories and if the commit histories between the master branch and the merging branch haven't changed since the merging branch was created, Git will perform the fast-forward merge by relocating the pointer of the current commit to the merging branch's tip (current commit) without creating a merge commit.

These merging processes may be understood more easily through a visual diagram. The diagrams used for the purpose of this article haved been borrowed from [Atlassian's Git Merge tutorial](https://www.atlassian.com/git/tutorials/using-branches/git-merge).

### Diagram of fast-forward merge

![Fast-forward merge of feature into master](https://wac-cdn.atlassian.com/dam/jcr:b87df050-2a3a-4f17-bb80-43c5217b4947/07%20(1).svg?cdnVersion=iq)

This diagram shows how the master branch's pointer is moved to point at the HEAD of the feature branch as a "fast-forward" since there are no changes to merge since the creation of feature. The master branch acquires the commits available in feature and and now has them in its commit history. After merging the feature branch into the master, it is common practice to delete the merged branch after the merge since it will no longer need to be used to contribute to the main project. Master contains all the merged changes from the branch it was fast-forwarded into, but during this process, a new merge commit was not made because there were no diverged histories to merge between master and feature. In some cases, a developer may want to turn off this default behavior in order to publish a merge commit even in the case that a fast forward would be possible. This behavior may be disabled by using the ```--no-ff``` option as follows:

	git merge --no-ff feature-branch

### Diagram of 3-way merge to create merge commit

![3-way merge of feature into master resulting in merge commit](https://wac-cdn.atlassian.com/dam/jcr:91b1bdf5-fda3-4d20-b108-0bb9eea402b2/08.svg?cdnVersion=iq)

When two histories diverge, a 3-way merge is necessary to combine the histories into one history as a merge commit on the current branch. This results in the merge commit having two parent commits, hence the term "3-way" describing how three commits are referenced to complete the merge. This strategy is the default merging strategy when merging two branches that have different commit histories since an ancestor commit.

## Reviewing state of repository before merging

A merge conflict between the remote repository and the local repository can be avoided through fetching the latest commits made to the remote and integrating those changes into the local environment by running ```git pull```. If there are changes in the remote that haven't been included in the local copy, attempting to push back to the remote before extracting changes will likely cause the push to fail. with this in mind, a developer will find it useful to reference any commits made to the remote through running ```git branch``` with the ```-va``` flags to display the branches in the current local repository and any remote repositories associated with it. Along with the branch name will be the most recent commit made to that branch shown with the shortened commit hash and commit message, as well as the status of the branch regarding the number of commits ahead of or behind its remote, which is displayed after the shortened commit hash in the commit. 

### Check for changes in upstream to merge into local branch

	git branch -va	

#### Output

	* master                                    6422e6c [ahead 4] Update answer to Advanced Project 2
 	feature-branch               				e958d1a [behind 2] Add git reset command to reference list.
	remotes/origin/HEAD                         -> origin/master
 	remotes/origin/master                       6346e6e Update answer Exercise 16
  	remotes/origin/feature-branch     		    e998z1b Add git diff command to reference list.

Notice the status after the commit hash. On the master branch, it is reported as ahead of its remote repository by 4 commits, while in the feature branch, the status of the branch's commit history is behind it's remotely track branch by 2 commits. This command is helpful when a developer wants to be able see the status of all the tracked branches in a repository, local and remote. There are a few ways to display the status of a branch's commit history, but this command is preferred if a developer wants to be able to view more than one branch's history at a time. 

To view the status of a specified branch's commits, the ```git show-branch``` command passed in with the name of a branch as an argument will display the commits in that branch or passing in the ```-r``` option after the command with no arguments will list all remote tracking branches along with each one's most recent commit. Likewise, running ```git status``` -uno will return a message with information regarding the current HEAD's remote status, that is, whether the remote branch being tracked by the current branch is ahead of, behind, diverged from the current HEAD. 

## Resolving merge conflicts

Merge conflicts will occur occasionally when the commits have been made in either the local or remote repositories that either version do not contain. This is usually the case when a developer has started working within a repository from a certain commit but did not merge the changes committed to the remote since he/she started working on his/her copy. This simple diagram taken from a Stack Overflow forum shows the history of the remote (upstream) branch and the local branch's history while their paths have diverged:

	... o ---- o ---- A ---- B  origin/master (upstream work)
                	   \
                  	    C  master (your work)

Referenced from Stack Overflow: [master branch and 'origin/master' have diverged, how to 'undiverge' branches'?](https://stackoverflow.com/questions/2452226/master-branch-and-origin-master-have-diverged-how-to-undiverge-branches)

The local branch C has not made any new commits since it was created, but the remote tracking branch has acquired one new commit that has not yet been included into the local repository's history. If a developer were to attempt to push a commit into the remote master branch in this state, a merge conflict would occur because the local repository does not contain the updated changes added to the remote and any changes made to the local branch since the ancestor commit that it was copied from have the potential to not be relevant to the main branch anymore because new commits may conflict with the local repository's commit history. 

### Merge remote branch into local branch

To resolve this conflict, running ```git pull``` with the name of the upstream repository to merge will create a new merge commit in the local branch, which will reference the tip of each branch (current HEAD for each branch) as a parent of the merge commit. The reason why ```git pull``` is used here is because it is a shorthand for the commands ```git fetch``` and ```git merge```, so running a single command is just as valid as running the two commands in stated order, but if a more verbose method or merging changes is preferred, the developer may choose to use the longer command to confirm what is to be committed before it happens. To merge up-to-date changes from the remote repository into the local repository, run ```git pull``` with the remote repository name to integrate remote changes into the local repository. Even if local changes have diverted, the merge will still be able to merge changes if they do not directly conflict with each other. (see *Resolving conflicts among changes to same files*)

### git pull to update local branch:

	git pull origin master

### Visual diagram of *origin/master* merging into *master*

	... o ---- o ---- A ---- B  origin/master (upstream work)
                 	   \      \
                  		C ---- M master (your work) (merge commit)

Referenced from Stack Overflow: [master branch and 'origin/master' have diverged, how to 'undiverge' branches'?](https://stackoverflow.com/questions/2452226/master-branch-and-origin-master-have-diverged-how-to-undiverge-branches)

### Resolving conflict among changes to same files

If a merge conflict were to occur in the case of merging changes into a branch but separate changes have been made to the same committed files in both branches, Git cannot decide which version to use out of the two and human intervention is needed to make the decision. To view which files have been modified in more than one branch, run ```git status``` when encountering the conflict and the command line will present a message identifying the conflicting paths:

### Output of ```git status``` when merge conflict is detected

	On branch master
	Unmerged paths:
	(use "git add/rm ..." as appropriate to mark resolution)
	both modified: hello_world.html

After identifying which files contain conflicts, the developer must manually 

### Syntax of merge conflict area in conflicted file

	Here are lines that are either unchanged from the common
	ancestor, or cleanly resolved because only one side changed.
	<<<<<<< yours:sample.txt
	Conflict resolution is hard;
	let's go shopping.
	=======
	Git makes conflict resolution easy.
	>>>>>>> theirs:sample.txt
	And here is another line that is cleanly resolved or unmodified.

Example referenced from Kernel man pages for git-merge: [git-merge(1) manual page](https://www.kernel.org/pub/software/scm/git/docs/git-merge.html#)

The changes made in the current branch are presented under a line of < signs labeled as *yours:filename* and followed by a trail of = signs to visually separate the changes made in the branch that were made in the merge destination branch, which are presented below the previous symbol and followed by > signs and similarly associated with a *theirs:filename* to mark that changes are from a branch other than "yours". The developer must make appropriate changes here in order to resolve the conflict, either by selecting which version to use or making necessary edits to relocate changes so that they are not in the same area.

### Committing the merge commit

Merge conflicts are often resolved in a similar way that changes in a working tree are staged and committed, by running ```git add``` and ```git commit``` after the conflicts have been resolved to complete the merging process. After making the necessary edits to the files to resolve conflicts, simply add them to the index with ```git add``` and commit the changes with ```git commit``` or ```git merge --continue```, which acts exactly as ```git commit``` does but scans if there are currently an interrupted merge occurring before committing the merge. There are also several other useful commands that can help a developer resolve a merge conflict, which can also be accessible on Kernal man pages git ```git merge```.

### Not committing the merge

In the case that all changes in the working tree should be discarded up until the pre-merge state, using the ```--abort``` option with ```git merge``` with no arguments will attempt to reset the state of the working tree to the state before the merge conflict. Changes that were added to the index but not committed may not be able to be restored, so committing changes is highly advised to avoid losing work.
	
	git merge --abort

This article covered several aspects of the ```git merge``` command and potential situations a developer might come into while using the command. If one wishes to know more about the command, he/she may view any of the links referenced in this article to further expand his/her knowledge. 

Tara Chan <br>
12/13/17 <br>
Fullstack Engineer


