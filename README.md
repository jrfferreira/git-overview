# Git Talk


# First thing first


## What is GIT?

* Historical control of your files
* Any kind of file
* https://git-scm.com/book/en/v2/Getting-Started-Git-Basics

## Nice to know

* Missing git in your machine? https://git-scm.com/
* Github isn't git
  * Github is a service using git as a platform
  * Other services: gitlab, bitbucket
* You don't need a remote repository to work with git
  
## Everything is already on git :)

``` bash
  $ git clone git@github.com:jrfferreira/git-talk.git
  $ cd git-talk
```

---

# From the beginning

## Making sure about your git avatar:

``` bash
  $ git config --global user.name "[name]"
  $ git config --global user.email "[email address]"
```

## How to start using git:

``` bash
  $ mkdir my-git-repository
  $ cd my-git-repository
  $ git init
```

## Understanding the git states:

* Working tree: Your work
* Index / Staging area: What do you want git to know
* HEAD / .git directory (repository): Where all changes snapshots are saved

## The help command

You can always finish your command with `--help` to check the documentation:

``` bash
  $ git config --help
  $ git remote --help
  $ git remote add --help
```

---

# Hands on


## Understanding branches:
 
Branch an independent line of development.

How to create a branch:

``` bash
  $ git branch [branch name]
  $ git checkout [branch name]
```

is the same as:

``` bash
  $ git checkout -b [branch name]
```

You can check here: https://backlog.com/git-tutorial/using-branches/

## the staging area

* git status:

``` bash
  $ git status
```

Helpful status:
  * ' ' = unmodified
  * M = modified
  * A = added
  * D = deleted
  * R = renamed
  * C = copied
  * U = updated but unmerged

* Diference between the staging and the working tree:

``` bash
  $ git diff
```

To show the difference between the staging and the current file version:

``` bash
  $ git diff --staged
```

* adding/removing a file from staging:

``` bash
  $ git add [file]
```

To remove from staging (not the file):

``` bash
  $ git reset [file]
```

* adding/removing hunks from staging:

``` bash
  $ git add -p [file]
```

``` bash
  $ git reset -p [file]
```

It will navigate between all hunks in a interative mode.

## Committing

After staging we can register the current state:

* With message

``` bash
  $ git commit -m "A brief explanation about my work"
```

You can also tell the command to automatically stage files that have been modified and deleted, but it will not affect new files:

``` bash
  $ git commit -a
```

But, please, don't do it.

* Fixing message

In case you had added a wrong message, you can fix it:

``` bash
  $ git commit --amend
```

* Reverting commit

``` bash
  $ git revert [commit]
```

It will undo all changes from the commit and add it to the staging

## Reviewing history

* log (and graph)

basic log:
``` bash
  $ git log
```

To follow all changes of a file:
``` bash
  $ git log --follow [file path]
```

The see the changes:
``` bash
  $ git log -p [file path]
```

Do you need a visual help?

``` bash
  $ git log --graph
  $ git log --graph --oneline
```

* show branch diff

``` bash
  $ git diff [branch1]..[branch2]
```
or
``` bash
  $ git diff HEAD..[branch2]
  $ git diff ..[branch2]
```

* show commit

``` bash
  $ git show [commit]
```

## Synchronizing changes

* remotes

Once you need to synchronize your changes with a server or a team, you will need a remote:

``` bash
  $ git remote add [remote name] [remote url]
```

* fetch remote / all remotes

Fetch allows you to download the remote repository history:

``` bash
  $ git fetch [remote name]
  $ git fetch --all
```

* pushing changes

``` bash
  $ git push [remote] [branch]
```

For new local branchs, you need to set the remote branch relation:

``` bash
  $ git push --set-upstream [remote name] [remote branch]
```

* push --force

In case you need to replace a remote repository:

``` bash
  $ git push --force
```

DON'T use --force on public/shared branch

* pull

To sync your local repository with the remote:

``` bash
  $ git pull [remote]
```

* merging branchs

Merge is useful to bring the independent line of development to other branch:

``` bash
  $ git merge [branch]
```

In case you need to do more changes:

``` bash
  $ git merge --no-commit [branch]
```

* rebase branch

Rebase is similar to merge, but it reapply the commits on top of another branch

``` bash
  $ git rebase [branch]
```

Check more in: https://hackernoon.com/git-merge-vs-rebase-whats-the-diff-76413c117333

  * Use merge in cases where you want a set of commits to be clearly grouped together in history
  * Use rebase when you want to keep a linear commit history
  * DON’T use rebase on a public/shared branch


---

# To add "git" in your Linkedin

## Conflicts

Sometimes, the remote or branch that you want to get changes can contain a different hunk.
In this case, git may not be able to auto-fix this, and you will need to act.

Example:

``` bash
This part still the same
<<<<<<< HEAD
but I added this
=======
and other person added this.
>>>>>>> playground
```

in this case:
* Everything from `<<<<<<< HEAD` to `=======` is related to your changes
* Everything from `=======` to `>>>>>>> playground` is what is coming from `playground` branch.

## Reseting

To clean your repository or reset the HEAD:

* Reseting a specific file:

``` bash
  $ git reset -p [file path]
```

* To resets the index and working tree discarting both:

``` bash
  $ git reset --hard [commit]
```

Any changes to tracked files in the working tree since `[commit]` are discarded.


* To resets the index but not the working tree:

``` bash
  $ git reset --mixed [dommit]
```

The changed files are preserved but not marked for commit

* To reset and keep the index and working tree:

``` bash
  $ git reset --soft [commit]
```

This leaves all your changed files "Changes to be committed"


## Patching

If you export `git diff` to a file, you can apply it in a different situation:

``` bash
  $ git diff > my-patch.diff
```

``` bash
  $git apply my-patch.diff
```

## Cherry pick

Pick a exactly commit to where you're:

``` bash
  $ git cherry-pick [commit hash]
```

An example to cherry pick all commits from master branch:

``` bash
  $ git cherry-pick ..master
```

* To continue the operation:

``` bash
  $ git cherry-pick --continue
``` 

* To finish  the current operation in progress.

``` bash
  $ git cherry-pick --quit
```

* To cancel the operation:

``` bash
  $ git cherry-pick --abort
```

## Stash

You can also save changes on your side. It is useful for work in progress manipulation:

* To save a staging state:

``` bash
  $ git stash
```

* To load a stash:
``` bash
  $ git stash pop
```

* To list all available stash:
``` bash
  $ git stash list
```

* To delete a stash:
``` bash
  $ git stash drop
```

## The .git folder

You need to see to understand

---

# Getting easy

* .gitignore file

* Breadcrumb about the branch. Add to your `.bash_profile`:

``` bash
  # Show current git branch in the command line
  
  parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
  }
  
  export PS1="\[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

* VSCode git support: https://code.visualstudio.com/docs/editor/versioncontrol#_git-patchdiff-mode

* Maybe this talk was not necessary: 
  * https://services.github.com/on-demand/downloads/github-git-cheat-sheet/
  * http://think-like-a-git.net/
