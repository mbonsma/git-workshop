---
title: "Git Workshop"
author: "Madeleine Bonsma-Fisher"
output: html_document
---

<!---## Instructor setup

In command prompt:

  - set command prompt to just dollar sign:
`PS1 = "$"`
  - change size of text: ctrl-shift-+
  - git --version

General setup:

  - Slide show: https://docs.google.com/presentation/d/1IjOyrn7ZN8QRMtKzXdKg3epWTQRCSwYgKleJHj7--cM/edit?usp=sharing

Instructions for group:

  - Install Git Bash if on Windows
  - Make a GitHub account
--->

## Setup

- Install Git Bash (Windows) or Git for Mac. [Instructions here](http://carpentries.github.io/workshop-template/#git).
- Make a [GitHub](https://github.com/) account.

## Slide notes

#### Title slide (1)

Which of the following best describes you?

- I had never heard of Git or GitHub before I came to this workshop.
- I've heard of Git / GitHub, but never used it.
- I have installed Git or I have an account on GitHub, but never really used it.
- I occasionally use Git / GitHub.
- I use Git or GitHub all the time.

#### Version control slide (2)  

Have any of these happened to you?

- I saved many versions of a file with slightly different names (i.e. `_v1`, `_v2`)
- I like to save intermediate steps while I'm writing or coding so I can go back to old ideas if necessary.
- I sometimes make a change to a document and then later wish I could remember what I wrote previously.
- When I want to experiment with a piece of code or writing for a new purpose, I make a new file.
- I sometimes look at work I did in the past and can't figure out what I did or why.

#### Save changes (4)

* Save only the changes, as opposed to the two extremes:
    * Saving nothing,
    * saving everything.
* We'll see later how Git implements this.

#### Git & GitHub (5)

* Before we go on, I just want to say what Git actually is. Git is a piece of
software that actually does version control.
* GitHub is a service that uses Git in the back end and hosts your files.

#### Why I didn't use Git (6)

* This was my system of version control, which actually works okay if:
    * (a) you keep very good notes
    * (b) you have lots of space to store stuff.

#### Why I started Git (8)
* I started having trouble finding stuff. Finally a perfect storm of comfortable with commands, saw reason to use.

#### Git bandwagon (9)
* Git and GitHub are taking over.

#### Save changes (10)
* Now we'll see how Git does this.

#### Version control (11)
* Instead of multiple versions of a file, version control gives you a list of
changes so that you can go back in time and see previous versions of things.

#### Commit (12)
* In Git, a saved change is a "commit".

#### Where's my stuff (13)
* "repository" or "repo" is the collection of files for a particular project.

## Workshop notes

````
# <- this is a comment

# general command line tips
# use tab completion: when you start typing something, hitting 'tab' will finish it for you.
# use the 'up' arrow to cycle through past commands (to avoid re-typing)
# for Git commands, typing git <command> --help will show a help page
````

### Configure your local git setup

This only needs to be done once on your computer. Only the first two commands
are essential.

```
git config --global user.name "Your Name"
git config --global user.email "you@some.domain"
git config --global color.ui "auto"
git config --global core.editor "your_editor"

git config --list # List all the configurations completed
```

```
cd ~/Desktop # cd = change directory
mkdir thesis # mkdir = make directory (create a folder)
cd thesis # move to the thesis folder
```

### Create a Git repository

Note: it's not a good idea to create git repositories inside other git
repositories. When you run `git init`, everything in that folder and any
sub-folder is part of the same repository.

You can also run `git init` inside a folder that already has things in it; for
example if you want to put your current project folder under version control.

Each separate 'project' should have a separate repository, although there
aren't any hard and fast rules for what constitutes a project.

```
git init  #git init = initialize a git repo (start an empty git repo in that folder)
touch intro.txt # create a new file
ls # ls = list files and folders in the current location
git status # git status = check the status of your folder - see if there are any changes.
```

### Making changes

Let's add some text to the `intro.txt` file. If you don't have `nano` installed,
you can either use a different text editor that you do have (i.e. Atom, notepad,
notepad++, etc.), or open the file from your file browser and edit it however
you would normally edit a text file.

```
nano intro.txt
git status
cat intro.txt
```

### `git add` and `git commit`

```
git add intro.txt # git add = tells git to add file to staging area
git status
git commit -m "begin thesis introduction"
git status
```

> ### Exiting Vim
> Note that Vim is the default editor for many programs.
> If you haven't used Vim before and wish to exit a session without saving
> your changes, press `Esc` then type `:q!` and hit `Return`.
> If you want to save your changes and quit, press `Esc` then type `:wq` and hit `Return`.

### Viewing changes

```
git log # show commit history

nano intro.txt
cat intro.txt
git status

git diff # shows changes between working directory and what's been committed

git commit -m "Expand intro"
git status
```

Whoops, Git won't commit because we didn't use `git add` first.

```
git add intro.txt
git status
git commit -m "Expand intro"
git status
git log
```

### Exploring history

The real power of Git is that it gives you very precise control over the
history of your files - both viewing them and accessing them.

```
nano intro.txt
cat intro.txt

git diff HEAD intro.txt # same as without the HEAD in this case
git diff HEAD~1 intro.txt
git diff HEAD~2 intro.txt

git diff f22b25e intro.txt

git add intro.txt
git commit -m " "
```

What if we overwrote our file? `git checkout` can bring any version to the present.

```
nano intro.txt # overwrite file
cat intro.txt
git status

git checkout HEAD intro.txt # retrieves the version that was most recently committed
cat intro.txt
```

`git checkout` can be used on any commit. When you use it, it changes your
working directory to that version of the file

```
git checkout f22b25e intro.txt
cat intro.txt
git status

git checkout HEAD intro.txt # takes us back to the most recent commit
```

You can use both `git diff`, `git log`, and `git checkout` with or without a
specific filename.

### GitHub

* Log in to GitHub, then click on the icon in the top right corner to create a
new repository called `thesis`. Leave 'initialize this repository with a README'
unchecked.
* Copy the url (using HTTPS)

```
git remote add origin https://github.com/mbonsma/thesis
git remote -v

git push origin master # push your changes to GitHub
```

How is 'git push' different from 'git commit'?

### More tricks for Git on the command line (time-permitting)

The `decorate` option adds the branch names at the ends of commits

```
# Nicer options for git log:
git log --graph --abbrev-commit --decorate
```

If you want to see the name of the file that was changed:

```
# For full path names of changed files:
git log --name-only

#For full path names and status of changed files:
git log --name-status

#For abbreviated pathnames and a diffstat of changed files:
git log --stat
```

One that I'm always looking up: how to get commits in a particular date range.

```
git log --all --after="<date> 00:00" --before="<date> 23:59"
```

Search for a change by the content of the change
```
git log -S'<a term in the source>'
```

Add a staged change to the previous commit (with the option to change the message as well)
```
git commit --amend
```

Reword the previous commit message
```
git commit -v --amend
```

### Forking on GitHub (time permitting)

If you want to work on someone else's project that's on GitHub, or if other people
want to work on your project, you will likely do this through a *fork*.

```
# Fork https://github.com/mbonsma/group-project
# In the upper right hand corner, click 'fork'
# clone:
cd ~/Documents/GitHub # make sure you're out of your other repo
git clone https://github.com/mbonsma/group-project.git
cd group-project
```

Now you have a copy of my repo that you can do anything you want to. You can
make changes on GitHub, you can make changes on your computer, and if you want
to you can request that I add your changes to my copy of the repository as well.

## Notes and tips

* You can place any kind of file under version control with Git, but some file types are easier to work with than others.
* You can make changes to files any way you are comfortable and still use Git to track them.
* You can do most things on GitHub if you don't want to use the command line.
* There are lots of nice options for the commands we used: for example, `git diff --color-words` shows the specific words that were changed, `git diff --staged` shows the difference between HEAD and the staging area, or `git log --stat` shows lots of information: modified files, how many lines were added and removed.

## More information and helpful resources

* [Web-based tutorials and hands-on practice](https://try.github.io/)
* [Simple first-steps guide](https://rogerdudler.github.io/git-guide/)
* [More in-depth workshop material](https://swcarpentry.github.io/git-novice/) (~3 hours, also good for reference)
* [Interactive, visual tutorial on branching](https://learngitbranching.js.org/)
* [How to collaborate on projects with GitHub](http://mozillascience.github.io/working-open-workshop/github_for_collaboration/)
* [Helpful wiki for using Git and GitHub for project collaboration](https://github.com/KirstieJane/STEMMRoleModels/wiki#table-of-contents)
* [Huge list of Git tutorials for specific topics](https://www.atlassian.com/git/tutorials)
