# Git's `diff` Command 

This is an introduction to comparing versions of code, using Git's **`diff`** command. This article assumes a basic understanding of [`git clone`](https://git-scm.com/docs/git-clone) and [`git commit`](https://git-scm.com/docs/git-commit). 

<br />  

## So What Is a Diff?  
So let's say you've checked out some code on GitHub to fix a bug. It happens to us all: life sends us a family emergency, the plumbing backs up, or other bugs take precedence. Your code is set aside. A couple weeks later all the major fires are out, and it's time to get cracking on the original bug. Do you even remember what you were working on? Do you know what functions you've changed? Did you delete anything important? Is it safe to push?

We can answer these questions with a `diff`. 'Diff' is a shortcut for the word *difference*; essentially we are comparing two versions of code to see what differs between them. Any proper versioning tool should be able to show you a diff (even many text editors can generate file diffs), and Git is no exception. Let's take a look at how Git helps you keep code changes in check. 

<br />  

## Diff on the Command Line    
We can find the syntax of the `diff` right on the command line, using `$ git diff -h`, which presents us with the following:    

`git diff [<options>] [<commit> [<commit>]] [--] [<path>...]`     

where things in brackets `[]` are optional, dependent upon what it is you need to compare. Git syntax is not always obvious, but we can think of the `diff` in terms of ***"show me how file A (or commit A) is different, as compared with file B (or commit B)."*** We can usually think of `A` as being the 'old' or 'original' version, while `B` is our intended change to `A`.  

![Diff Diagram](https://i.imgur.com/h5RlYOe.png)  

In this article, we will use `diff` to:  

* ***Compare commits*** -- `$ git diff [Commit A][Commit B]`)  
* ***Compare your working directory to the last committed version*** -- `$ git diff [HEAD(A)]` while inside `pwd (B)`  
* ***Compare staged files to unstaged files*** -- `$ git diff`, where `A` is staged files and `B` is the present working directory (`pwd`)    
* ***And to compare staged files to the master copy*** -- `$ git diff --staged`, where `A` is the master copy and `B` is staged files.

<br />  

## Comparing Your Working Directory to the Master  

|`$ git diff HEAD`| `A` = Master/HEAD; `B` = `pwd` |  
|-----------------|--------------------------------| 

To see how `git diff` works, all we need is a Git repo file that is different than the original, master copy. Let's use Git's practice repo, 'Spoon-Knife'. You can clone it from https://github.com/octocat/Spoon-Knife, then navigate into the directory you've cloned it to. Running `ls -1` should return something similar to this:     

> README.md  
Spoon-Knife.wiki   
index.html  
styles.css

We need to make a change here, so we have something to compare with the original. Let's add a text file:

`$ touch help-turtles.txt`  
`$ echo >> 'The turtles are escaping!' >> help-turtles.txt`    
*(Note the use of single quotes, to ensure the `!` is interpreted as plain text.)*  
  
Let's also stage our changes:

`$ git add help-turtles.txt`

. . . and run **`$ git diff HEAD`**. The `HEAD` option indicates that we want to look at our local master copy (the last commit), and compare it to the working directory. The results you get should look similar to this (without the line numbers):

![Diff1](https://i.imgur.com/XAZHqxI.png)

* On **line 1**, we can see that `diff` is comparing File A (a/help-turtles.txt) to File B (b/help-turtles.txt). In this case, **a** represents the master copy, and **b** represents the change you've staged.
* Skipping to **line 4**, we can see File A represented as `dev/null`. This simply indicates that we are submitting a new file; File B will be compared to `null`, which in this case means a previously non-extant file.
* On **line 5** we can see that File B is our new file, `turles-help.txt`.
* **Line 6** shows how many lines were added and removed. The `-` indicates lines were removed, shere indicating that starting at line 0, 0 lines were removed. This makes sense, because we are adding a new file. The `+` indicates that we added lines. In this example we can see that, starting at line 0, we added 1 line.
* At **line 7** we can see what, exactly, is being changed. In this case our added text is prepended with a `+`, indicating that this text is an addition. 

If we had staged a change that removed text from a file that was already in the original, it would be prepended by a `-`. To see this in action, we can edit the Spoon-Knife `index.html` file. Remove the contents of the `<p>` element, and replace them with "The turtles are loose!" (without the quotes). Do a `$ git add index.html`, then `$ git diff HEAD`:

![Diff2](https://i.imgur.com/d90TuaG.png)


Notice that our original file still shows up in the `diff`, but now we have another change. File A is the original `index.html` file we pulled in form the master copy, and File B is our revised `index.html`. 

If you look at line 15 above, you will notice that removed text appears in <span style="color: crimson;">red</span>, prepended by a `-`. This indicates that our change to File B lacks this text, as compared with the original File A. Line 16, prepended by a `+` and showing in <span style="color: green;">green</span>, indicates that our File B will include this line, which does not exist in the original.

<br />  

## Comparing Staged Files to Unstaged Files  

|`$ git diff`| `A` = Stage/Index file; `B` = Unstaged changes in `pwd` |  
|------------|---------------------------------------------------------| 

Git uses an ***index*** file to keep track of what you are planning to commit. Adding a file to the index is commonly referred to as **staging** it, or 'adding it to the staging area'. Files are staged by using the `$ git add [file]` command. Once a file is staged, you've told Git to include it in your next commit. There may be times that you are working on code and don't recall what you've already staged, or what you've changed in staged files. Let's see how we might compare what we've staged to what is in our working directory but **not staged**:  

First, alter the `help-turtles.txt` file again, and stage it:  

`$ echo "So. Many. Turtles." >> help-turtles.txt`    
`$ git add help-turtles.txt`   

Then alter it again, but without staging the changes:  

`$ echo "All the way down." >> help-turtles.txt`  

Now we have both staged and unstaged changes. Comparing them is now a simple matter:

`$ git diff`

The results show our unstaged changes as an addition relative to the committed changes:

![Diff3](https://i.imgur.com/MOp7iNS.png)   

So how is this different from `$ git diff HEAD`? Using the `HEAD` option means that we are comparing our changes to the last commit; everything that is different than the source you cloned from will show as something being added to or removed from the original. Here wa are comparing STAGED files to UNSTAGED files--files that ***will*** be committed vs. files that ***can*** be committed. Here, staged files are `A`, and unstaged files are `B`. 

<br />  

## Comparing Staged Files to the Master Copy  

|`$ git diff --staged` or `$ git diff --cached`|`A` = Master copy; `B` = Stage, a.k.a. index file|  
|----------------------------------------------|-------------------------------------------------|

A `diff` can also show you what changes are staged--that is, what changes are set to move up with the next commit, as compared with the master copy. We can do this with either the `--cached` or `--staged` options, which differ in name only. Try running it:  

`$ git diff --staged`

Recall from our previous exercise that we made two changes to our text file:  

* We added, "So. Many. Turles.", ***then staged this change***.
* We added, "All the way down.", ***without*** staging this change.

As expected, we only see the difference between the master copy and what is staged:

![LastDiff](https://i.imgur.com/djKD1YA.png)  

<br />  

## Comparing Commits  

| `$ git diff [Commit A] [Commit B]`| `A` = Some commit's ID; `B` = Some other commit's ID | 
|-----------------------------------|------------------------------------------------------| 

We can also use `diff` to compare one commit to another. To try it out, go ahead and `commit` (`$ git commit`) your changes. Let's run `$ git log` to get the id numbers for specific commits. This should look something like `commit 5a11f9d...b8d2f1e6a`, and there should be at least one log entry that lists you as the author, because you just committed. Let's try diffing your commit, and one of the commits from the original author. Copy the ID number for the oldest commit you can find in the log, and make that your Commit A (the first commit argument). This should be something authored by 'The Octocat'. Then copy the ID for the commit you just made, and make that Commit B. Let's try it out.

This syntax:

**`$ git diff [Commit A] [Commit B]`**   

. . . becomes this command:  

**`$ git diff a30c19e3f13...e95cee4 5a11f9d16...b8d2f1e6a`**

This should return a good deal more text--the entirety of the first commit! You can scroll through the diff using the arrow keys if it does not all fit in the terminal window. 

<br />  

## Options  
There are a few options you can use to tweak the output of your diff. Here are a some of the more common ones:

| Option    | Purpose | Usage |
|-----------|---------|-------|
|**--check**| This is used to have your diff report any <br /> whitespace errors. Things like a trailing <br /> space on the end of a line, or full blank <br /> lines will appear as possible errors. | `$ git diff HEAD --check`|
|**--color:**| The color option dictates whether differences <br /> are highlighted with color or not. |`$ git diff HEAD --color=always` <br /> (`color=never`, `color=auto`). You <br /> can also use `--color` on it's own <br /> (without the always, never or auto) to use <br /> color, or `--no-color` to turn it off.|
|**--M** or <br /> **--find-renames:**| You can tell your diff to detect when a file <br />appears to have been renamed. This is based on a changed name with some percentage of the files content left unchanged. For example, if you use `--M90%`, your diff will check for any file that is 90% (or more) the same as the last commit, but with a different name. |`$ git diff HEAD --M90%`|
|**-G:**| Find regex matches within a diff. |`$ git diff HEAD -G .urtl*` (which would return files that include changes to the words 'turtle', 'Murtle', 'burtli', etc.).|

* A full listing of options is available in the `diff` section of the Git Manual at https://git-scm.com/docs/git-diff, or right in the terminal using `$ git help diff`.

<br />  

<hr />  
 
Whether comparing works in progress to stage, stage to master, or commit to commit, Git's `diff` command is a powerful tool for version control. You can use it to find potential bugs, guide you in regression testing, or just to remind yourself what you've changed before committing code changes. Be sure to check out the [Git Manual](https://git-scm.com/doc) for more info on `diff` and Git's other commands.  

<hr />  
  
Michael M. Chandler, December 25, 2017, Front End Engineering
