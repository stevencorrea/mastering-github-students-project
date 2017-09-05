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

### Removing configuration values

When you mistype a configuration name or value, you'll want to remove it's register inside your ```.gitconfig``` file. In order to do that you need to use the ```--unset``` directive.

```bash
# Let's add a wrong configuration
git config user.age 25

# To remove user.age use --exclude
git config --exclude user.age
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

### Colors

You can configure your git console colors very precisely using predefined colors or hexadecimal color values.

#### Color definition process

When configuring a color you need first to enable color configuration. There are six main color areas you can configure with ```true``` or ```false```.:

* ```color.branch```: Colors referent your git branch
* ```color.decorate```: ```git log --decorate``` output colors.
* ```color.diff```: Colors of diff presentations.
* ```color.grep```: Output colors of ```git grep``` command.
* ```color.interactive```: Colors of ```--interactive``` directive.
* ```color.status```: Colors used when showing your git repository status. ```git status```

When you set any of these areas as ```true```, you'll be able to configure their color <slots>.

For instance ```color.status```, have the following slots of color to change:

* color.status.added       
* color.status.changed     
* color.status.header      
* color.status.nobranch    
* color.status.untracked   
* color.status.updated


Let's say you want your modified files listed on ```git status -s``` to be shown in magenta, you need to do the following:

```bash
# 1 - Make sure you have your color.status marked as true, this will enable you to configure all git status slots colors
git config color.status true

# 2 - Now you're able to change the color slot of modified files to magenta.
git config color.status.changed magenta
```

It works the same configuring other color areas.

#### Default color list

The predefined git colors are listed below.

* normal
* black
* red
* green
* yellow
* blue
* magenta
* cyan
* white

### Editor
Sometimes when using git, it opens an text editor.

If the text editor is not of your preference you can say to git which one you want to use with the option ```core.editor```

```bash
# Sets vim as my OS user prefered terminal text editor.
git config --global core.editor vim
```

### Aliases

Aliases are great to reduce your daily efforts using git command line.

Using git aliases you can create shortcuts from simple to complex commands that will save you lots of typing energy.

#### Simple command alias example

If you want to shorten your ```git commit``` command to ```git ci```.

```bash
# git config alias.<alias_name> <command being shortened>
git config --global alias.ci commit

# Using the alias
git ci
```

**PS:.** ```--global``` directive is advised to use, because normally aliases are going to be integrated inside your daily workflow to all projects.

#### Complex command aliases

Shortening git commit to git ci, may not look like something of great improvement.
To show you the aliases power, I'm going to explain this article [User friendly git log](https://coderwall.com/p/euwpig/a-better-git-log) which creates an alias for a beautiful ```git log``` command.

The normal ```git log``` command.

![Normal git log](http://i.imgur.com/XgZxY5r.jpg)

The extended ```git log``` command.


![Improved git log](https://i.imgur.com/hPpuHu9.jpg)

```bash
# This git log command shows the <commit hash> - <branch> - <commit message> - <elapsed time> <commiter name>
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit

# Now let's encapsulate this inside a git lg alias
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bo
ld blue)<%an>%Creset' --abbrev-commit"

# Using the alias
git lg

# Using the alias showing the diff code.
git lg -p

# Using the alias showing the last two commits.
git lg 2

```

Guilherme Soldateli

08/24/2017

Career Path 3: Modern Frontend Developer
