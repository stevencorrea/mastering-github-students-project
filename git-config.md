# ```git config```
```git config``` is of great help during your daily life as a developer.

Configuring your git to meet your (or your team) preferences may save many precious hours of work.

During this article some examples will be shown and hopefully you'll be able to configure your git to fit your best preferences.

## Basic usage

```git config``` is a command line interface to configure your ```.gitconfig``` files. You may add/change or remove your git preferences with this command.

### Setting configuration values

As an basic example, let configure your name and e-mail into your git installation.

```bash
# git config theorical basic syntax
# git config <--directives-you-want-to-use> <option.suboption> <value>

git config --global user.email  "your@mail.com"
git config --global user.name  "Your Name"
```

**PS:.**
 ```--global``` directive will be explained in the section 
 [Configuration levels](#configuration-levels)


### Retrieving configuration values
Now let's understand how to retrieve the configuration you've done in the example above.

You just have to use ```git config <option>``` without assigning any value to retrieve the value.

```bash
#Let's say you want to know your configured user.name
git config user.name 

#OUTPUT:
# Your Name
```

```<option>``` accepts **TAB AUTOCOMPLETE**. This is great when you don't know what options are availabe to you!

```bash
git config user.<press TAB twice>

#OUTPUT:
# user.email        user.name         user.signingkey 
```

## What ```git config``` really does inside your OS?

```git config``` is a command that store your configurations across the ```.gitconfig``` files located in your OS.

You will want use this command to avoid architectural mistyping errors inside the `.gitconfig` file.

When you have a brand new git installation in your machine, your `.gitconfig` file will probably be empty.

```bash
cat ~/.gitconfig 

#Output: (EMPTY FILE)
```

After running the basic examples above, your .gitconfig file may look like this:
```bash
cat ~/.gitconfig 

#Output:
#[user]
#     email = your@mail.com
#     name = Your Name
```

### Configuration levels

As said before, there are more ```.gitconfig``` files around your OS than the file located in your home folder ```~/.gitconfig```.

Each of these files corresponds to a hierarquic level of configuration.

* ```/etc/gitconfig``` : Configuration relative to the whole OS (All OS users).
* ```~/.gitconfig``` : Configuration relative to your OS user (Unix based OS)
* ```your_project_directory``` : Configuration relative only inside the folder of your cloned repository.

For more information please take a look on how these configurations are interrelated.

| Level | Directive |Location (Unix OS) | Importance |
|---|---|---|---|
|Entire OS| --system  | /etc/gitconfig | Using ```git config --system``` you'll be setting a configuration to the whole OS. all OS users will be affected.  |
|Your OS User   | --global  | ~/.gitconfig   | Using ```git config --global``` the configuration scope will be only for the current logged user. Everything you configure here will override the ```--system``` conf.  |
|Local git repository   | --local (Or none, this is default)  | <Whatever your git repository is placed>  | Using ```git config --global``` the configuration scope will be only for the current repository. Everything you configure here will override the ```--system``` and ```--global```  conf. |


## Most common git configurations you may take advantage of.

### User

### Colors
**Visual example**

### Editor

### Aliases
#### Complex command aliases

**User friendly git log** https://coderwall.com/p/euwpig/a-better-git-log







---

## Why should you use .gitconfig?

Using .gitconfig enables you to configure your git to meet your preferences of colors/workflow/personal data.

Let's see some examples of what you're capable of using git config command.

First things first.

```git config``` is a command that writes inside your .gitconfig files, you will want use this command to avoid mistyping errors inside the `.gitconfig` file.

**When you have a fresh git installation in your machine, your `.gitconfig` file will probably be empty.**

```bash
cat ~/.gitconfig 

#Output: (EMPTY FILE)
```

### Setting your user name and email.

**Now, let's add your user email and name to your `.gitconfig` file.**

```bash
# git config theorical basic syntax
# git config <--directives-you-want-to-use> <option.suboption> <value>

git config --global user.email  "your@mail.com"
git config --global user.name  "Your Name"
```
**PS:.** *```--global``` directive will be explained in the sections below with more detail, for the moment you need to understand that ```--global``` relates to the git configuration of your OS user.*


**Look what ```git config``` did to your gitconfig file:**
```bash
cat ~/.gitconfig 

#Output:
#[user]
#     email = your@mail.com
#     name = Your Name
```

Now git knows the basic information needed when logging your actions within your repositories.

### Setting your prefered text editor to vim

Sometimes when using git, it opens an text editor inside the terminal. 

If the text editor is not of your preference you can say to git which one you want to use with the option ```core.editor```

```bash
# Sets vim as my OS user prefered terminal text editor.
git config --global core.editor vim
```

### There is a better way to debug ```gitconfig``` files instead using ```cat``` ?

If you want to see what configurations are in place without having to read the entire configuration file you may use: 
```bash
## You may use git config <option> without assigning value
git config user.name #Let's say you want to know your user.name

#OUTPUT:
# Your Name
```

```<option>``` accepts TAB AUTOCOMPLETE. This is great when you don't know what options are availabe to you!
```bash
git config user.<press TAB twice>

#OUTPUT:
# user.email        user.name         user.signingkey 
```




## A brief explanation on WHY to use ```--global```.

The thing is... there are more ```.gitconfig``` files around your OS than the file located in your home folder ```~/.gitconfig```.

Each of these files corresponds to a hierarquic level of configuration.

If you write 

| Level | Directive |Location (Unix OS) | Importance |
|---|---|---|---|
|Entire OS| --system  | /etc/gitconfig | Using ```git config --system``` you'll be setting a configuration to the whole OS. all OS users will be affected.  |
|Your OS User   | --global  | ~/.gitconfig   | Using ```git config --global``` the configuration scope will be only for the current logged user. Everything you configure here will override the ```--system``` conf.  |
|Local git repository   | --local (Or none, this is default)  | <Whatever your git repository is placed>  | Using ```git config --global``` the configuration scope will be only for the current repository. Everything you configure here will override the ```--system``` and ```--global```  conf. |
---

I really hope this content can be of help showing how important is to configure your git avoiding misconceptions that may make you lose precious time of life.



Guilherme Soldateli

08/24/2017

Career Path 3: Modern Frontend Developer
