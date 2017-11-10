
## Understanding the `Git Pull` command


 - You are a part of a team, working on a project. You have to be aware of the things are being changed by your team members,  constantly update your own files with other teammates'  but ...
 
 - It seems like you are the smartest developer in your team.  It might be either to show you are making the most improvements and changes on the project or to lead your team efficiently i.e, whatever reason might be - you want to put your own changes on the top what everybody else has done but ...

 - I am reiterating you are the most brilliant one.  Eventually,  you guys have finished your project and uploaded it in GitHub as well. Two days later, when you were taking a cursory glance on codes, you have noticed some bugs in Tim's files. You made some improvements on codes and wanted to let him know about that but ...
 

    How do you do that?
    =================

![Don't know](https://theyouideology.files.wordpress.com/2013/06/idontknow.jpg)


<br/>
Well,  you just need to use `Git Pull` !! 
Let's talk about it.
<br/>

> Pull  =  Fetch + Merge
> -------------------------


**Okay, what does it mean?**

    Git Pull - gets the latest data from remote repo, modifies and merges it automatically with the local repository.

As a team member,  you have a copy of everybody  else's project files on your computer. 

    $ git pull <remote>
This command merges the upstream changes into your local repository. In other words, your local repository is updated with remote repos.

#### **Pull vs Fetch**
Here is an important thing. In the above line, we said `Git pull` is equivalent to `fetch + merge`. `Fetch command` - gets also the latest branch of remote repo but it doesn't automatically modify local repository  unless you use `merge command`; It is recommended to use the latter command combination since it is safe and manageable. 

    $ git fetch origin
    $ git merge origin/master

*origin - you can think of a remote repository
*master - your local branch ( a line of developments).

#### **Pulling via Rebase**
This command comes very handy when you want to prevent any kind of unnecessary merge commits and maintain a safe linear history of commits:

    $ git checkout master
    $ git pull --rebase origin

#### **Pull request**

If you want to contribute  changes to someone else's project, you actually need to send a formal request to let project owner know " You are initiating some sort of improvements on his project". In GitHub language, it is called `Initiating Pull request`. Here are the main steps for that:

 - You need to have a copy of the project on your computer. It can be done by **Forking** repository and use **Git clone** to have it a local copy.
 -  Edit the file you want to make changes and commit it.
 - Push the changes to your fork on GitHub:   ` $  git push origin`
 - There is a small green button **New Pull request**, click on it and make sure other settings are correct.
 - Click on **Create pull request** button.


To conclude,  to use `Git Pull` efficiently reveals another powerful feature of Git and it is also one of the important tool to interact with other users.


Tiyor Abdupattoev
08/25/2017
Career Path 5: Fullstack Engineer