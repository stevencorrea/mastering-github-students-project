#### zero to hundred with `git tag`

# `git tag` Is All About Version Tagging!

When working on large projects that are constantly evolving, it becomes necessary to be able to classify major changes into versions for easier access.

The `git tag` is the git command that makes this possible. It is used to tag major changes in a repository by naming the changes as versions along with adding a message to the version description to easily identify such changes at a later date.

To help you understand this completely, we'll go through how to tag a project using the `git tag` command.

## Creating tags

Let's go ahead and tag a project repo named 'pills' using `git tag` and     I'll explain every line of code.

```
65black@ElevenPC MINGW64 ~/Desktop/workspace/pills (master)
$ pwd
/c/Users/65black/Desktop/workspace/pills

65black@ElevenPC MINGW64 ~/Desktop/workspace/pills (master)
$ git tag -a 'v1.0' -m 'Example using Git Tag' HEAD

```
First, we use the `pwd` command to ensure that we're in the right repo. Note that this is not a necessary step to using `git tag`. I just like being thorough.

Next, we actually use the `git tag` command to tag our repo as 'v1.0' and add a message 'Example using Git Tag' to help us access and understand it easier in the future.

The first flag `-a` is used to give a name to the tag you're attaching to your repo. The `-m` flag is used to add a message to the tag so that you can understand it easily in the future.

### Commits are also welcome

One great thing about `git tag` is that you can also use it to tag individual commits. Say I have a commit with a shortened hash id ` 3b8b40f` that I want to tag, the command will look like this:

```
$ git tag -a 'v1.0' -m 'My very first Release' 3b8b40f
```
You can see that the only difference in this bit of code and the previous one is the replacement of the `HEAD` argument with `3b8b40f` which is actually the shortened ID of the commit we're tagging.

## Viewing Tags

Why create something you will be unable to see at a later date? This is why `git tag` also comes with flags for viewing previously created tags.

Say we want to view all the tags in our current 'pills' project, our command would look like this: 

```
$ git tag -l
v1.0
```
The first line is just the `git tag` command with  an `-l` flag passed to it. This flag lists all the tags in the current project.

If you want to see more details about a particular tag, you will need to use the `git show` command. Here's an example:

```
65black@ElevenPC MINGW64 ~/Desktop/workspace/pills (master)
$ git show v1.0
tag v1.0
Tagger: 65black <kevinokeh@gmail.com>
Date:   Wed Mar 28 21:22:21 2018 +0100

Example using Git Tag

commit 689202728ce95ca870745bfe8ef4fc07294de182 (HEAD -> master, tag: v1.0, origin/master, origin/HEAD)
Author: 65black <kevinokeh@gmail.com>
Date:   Wed Mar 28 20:44:05 2018 +0100

    added a dummy file for a git tag tutorial

diff --git a/commit.txt b/commit.txt
new file mode 100644
index 0000000..e69de29


```
Pretty cool huh?

---
#### Note: If you cannot exit `git show`, press Q
----

## Deleting Tags

Yes, you can also delete previously created tags very easily using the `-d` flag. Here's how we'd delete our previous 'v1.0' tag.

```
$ git tag -d v1.0
Deleted tag 'v1.0' (was 085d0c2)
```
To delete the tag from the remote repository too, we'd do this:

```
$ git push origin :v1.0
To git@github.com:65black/pills.git
- [deleted]
v1.0
```

## Conclusion

We have hardly scratched the surface of the `git tag` command as it is a very powerful command with tons of uses.

I recommend going through the documentation of this powerful command from the official [Git Docs](https://git-scm.com/docs/git-tag). Learning how to use this tool effectively will give you another useful addition to your toolkit as a programmer.

Ovie Okeh |
March 28, 2018 |
Career Path 3: Modern Frontend Developer