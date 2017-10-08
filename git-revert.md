__________________
# ```Git Revert```
____________

The git revert command will undo a commit, to do that without removing the commit from the project history, it create a new commit without the changes made by the selected commit.

Imagine that you delete some old files, commit and push to the master repository, but then, the company need the files again.
There is no need to panic, git revert is here to salve you.
* for  the git revert command, you will need the commit hash e.g., fe896093b75b6bdbe8b228fa48d44ab19f839bc1 you can find the commit hash on github in the tab commit, or using the command line git log.

* after use git revert, git will remove the changes made by the commit and apply the result in a new commit.

_________________
## ```When use git revert```
_______________
The best scenario to use revert, is when you need to delete all changes made by a commit e.g. bad commits contain bugs.
### ```Example```

|command | Descrption|
|--------|----------|
|rm somefile.txt|delete some tracked files|
|	git commit -m “some changes”|commit the changes(snapshot)|
|	git push origin master|update the changes to origin master repository|
|	git revert (commit)|revert the last commit|

Generate a new commit that will undo all of the changes introduced in *commit*, then apply it to the current branch.
___________
## ```Advanced list of git revert examples```
_______________

### ```Revert more than one commit```
In the case when you make more than one commit contain some unwanted changes e.g., you make 3 different commits, and now you need to revert all.
```
git revert head~3
```
The ‘head’ stands for your actual branch (the present situation of your files), and the ‘3’ is the number of commits that will be unchanged.
this command will create a new commit with the reverted changes.
* Be careful, revert more than one commit at the same time, can cause merge problems.

with this code, git revert will not start the commit message editor .
```
git revert --no-edit <commit>
```

This code will revert the changes done by commits from the forth last commit in master (included) to the second last commit in master (included), but do not create any commit with the reverted changes. The revert only modifies the working tree and the index. 
```
git revert -n master~4..master~1
```
* This can cause merge problems too.

For full list of commands, please see the manual page.
