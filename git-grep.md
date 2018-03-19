# git grep command

Sometimes you will need some content from your repository,and simply looking through all files manualy can be time-consuming. In some cases when u have a very large repository and you need something quick,it's not always obvious where to search for it.Luckily,`Unix tools` such as `grep` allow you to find the content with ease. By the definition from offical [Git website](https://git-scm.com/docs/git-grep), `git grep`:
>Look for specified patterns in the tracked files in the work tree, blobs registered in the index file, or blobs in given tree objects. Patterns are lists of one or more search expressions separated by newline characters. An empty string as search expression matches all lines.

Imagine you have something like this in your code:

```javascript
for (i = 1; i < 10; i++) {
               let b = c;;
               while (next < last) {
```

Obviously,the double-semicolon is wrong. JS engine,in this particular case,will ignore this and it would not affect your code at all,but it should not be there. Now,imagine that you have one project with a couple of thousands,even hundreds of thousands lines of code.You would search mistakes like this one by looking at every line separately? No,you would not! You would probably started crying after couple hundred lines.We all would do! If you were in a working three controlled by VCS other then Git,here is what you would normally do to find this:

      find . -type d \\( -name CVS -o -name .svn -o -name RCS \\) -prune -o \\
     -type f -print0 | xargs -0 grep -n -e ';;'

Is this looking simple to you ? You got desire to quit ? I had when i saw this,and even when i learned what it means.But since we are now living in `Git` era,we can say this instead:

      git grep -e ';;'

This tells: go and search in the work three for all occurrences of double semi-colons.However this will search all the files in your repository and we often do not want this. To tell your console to search only in specefic files type this:

      git grep -e ';;' -- '*.js'

Because `git grep` can take options,pattern strings and commits,you use double-dash to mark the beginning of the optional list of path patterns that come at the end of the command line.Asterisk is just telling: give me just javascript files.

You can do the same search in a version you have scheduled for the next commit in the index:

      git grep --cached -e ';;' -- '*.js'

 --cached tells the command that usually works on the work tree to work only on the data in the index instead. Of course, you can search in an arbitrary commit, e.g. run the search in the current and in the "next" branch:

      git grep -e ';;' next HEAD -- '*.js'

With `git grep`, you can do this:

      git grep -e ';;' --and --not -e 'for *(.*;;' -- '*.js'

When you give more than one patterns to grep with -e option, you can only say "lines matching this or that". But "git grep" allows you to say "lines matching this and that" by specifying --and. The above example goes one step further. By prefixing a term with --not, you can even say "lines matching this and not that".

There are of course many more arguments that `git grep` takes,fo example:`-l` lists files with matches (and `-L` is files without), `-E` allows an extended regexp, `-i` is ignore case and `-w` is word regexp.

There are also some options which are specific to git. The `--no-index` example scans the files in the directories,`--untracked` searches in  addition to the tracked files in the working tree,also in untracked files,`--text` processes binary files as if they were text,`--word-regexp`
matches the pattern only at word boundary (either begin at the beginning of a line, or preceded by a non-word character; end at the end of a line or followed by a non-word character),`--invert-match` selects non-matching lines etc.

I hope that you will find this article useful and that it will expand your knowledge.