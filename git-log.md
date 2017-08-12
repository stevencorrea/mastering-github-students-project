# ```git log```

Using a version control system like Git you can record a detailed history of your project at different stages. The ```git log``` command allows you to view previous "commits" of your project, giving you the ability to travel back in time, find out where a bug may have been introduced to your code or find an important file that has gone missing.

For the simplest use of ```git log```, use the ```cd``` command to change to the location of your git repository and then type the command ```git log```:
```
cd my_git_repository
git log
```
This will show you a list of your previous commits in it's default format:
```
commit c190fb14712ef3e654b09783afa682f576d715ed
Author: Some Name <someemail@email.com>
Date:   Sat Jul 29 10:13:56 2017 -0700

    Updated README.md to include something
```
* ```commit c190fb14712ef3e654b09783afa682f576d715ed``` is the "commit hash" that was created to identify this particular commit. You will use this hash with the ```git checkout``` command if you want to revert back to this previous state of your project.

* ```Author: Some Name <someemail@email.com>``` is the author of this particular commit. This is especially useful if you have multiple people working on a project at one time.

* ```Date:   Sat Jul 29 10:13:56 2017 -0700``` is the date and time of this commit.

* ```Updated README.md to include something``` is the commit message that was included at the time of the commit.

This is the simplest way to use the ```git log``` command and would suffice for most users. If you are working on a large project with many contributors you may want to use the more advanced flags and options available.


## Advanced ```git log``` Examples

### Formatting ```git log```

You can customize the information that ```git log``` will display for each commit using flags requesting more or less information:

```
git log --oneline
```
Will show you the commit ID and the first line of the commit message on one line.
```
git log -p
```
Will show you all of the changes made with each commit.
```
git shortlog
```
Will show you commits sorted by author and lists the first line of each commit by that author.
```
git log --pretty=format:"%cn committed %H on %cd"
```
Using the ```--pretty=format:"<string>"``` structure you can create custom formatting. In the above example, ```%cn```, ```%H``` and ```%cd``` are place holders that are replaced by the committer name, commit hash and the commit date respectively. Using these place holders you create almost any format that you would like. You can find the complete list of the pretty format placeholders in the ```git log``` man page.

### Filtering ```git log```

If you are working on a project that has a long history of commits and many contributors you may want to filter the results of ```git log``` so that you can narrow down how many commit's you have to look through:

```
git log -5
```
Will display the 5 most recent commits. Substitute 5 with the number of the most recent commits you would like to display.
```
git log --after="2017-05-20"
```
Will display all commits after the date specified in quotes. You can also use ```--before```. 
```
git log --before="2017-07-20" --after="2017-05-20"
```
Using a combination of ```--before``` and ```--after``` to specify a range of dates.
```
git log --author="Robert"
```
Will sort the commits based on the author named "Robert". 
```
git log --grep="foo"
```
Will show commits that have a commit message containing "foo". 
```
git log -S"Some string"
```
Will show commits that have had "Some string" added or changed. This is particularly useful if you want to find a commit where a certain line of code was changed or added.
```
git log --no-merges
```
Will exclude all merge commits.
```
git log --merges
```
Will only show merge commits.


Most of these options and flags can be combined in complex ways to navigate the commit history of your project efficiently. Once you have a combination that is useful, you can create an alias shortcut using ```git config``` command to be able to use it easily and quickly. 

For a full list of options and flags, see the ```git log``` [manual]("https://git-scm.com/docs/git-log") page.