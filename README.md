# Git Talk

---

## First thing first


### What is GIT?

* Historical control of your files
* Any kind of file
* https://git-scm.com/book/en/v2/Getting-Started-Git-Basics

---

### Nice to know

* Missing git in your machine? https://git-scm.com/
* Github isn't git
  * Github is a service using git as a platform
  * Other services: gitlab, bitbucket
* You don't need a remote repository to work with git
  
---

### Everything is already on git

``` git
git clone git@github.com:jrfferreira/git-talk.git
cd git-talk
```

---

## From the beginning

### Making sure about your git avatar:

``` git
git config --global user.name "[name]"
git config --global user.email "[email address]"
```

### How to start using git:

``` git
mkdir my-git-repository
cd my-git-repository
git init
```

---

### Understanding the git states:

* Working tree: Your work
* Index / Staging area: What do you want git to know
* HEAD: reference to the local current state
* .git directory (repository): Where all changes snapshots are saved

---

### The help command

You can always finish your command with `--help` to check the documentation:

``` git
git config --help
git remote --help
git remote add --help
```

---

## Hands-on

---

### Understanding branches:
 
Branch an independent line of development.

#### How to create a branch:

``` git
git branch [branch name]
git checkout [branch name]
```

is the same as:

``` git
git checkout -b [branch name]
```

You can check here: https://backlog.com/git-tutorial/using-branches/

---

### the staging area

#### git status:

``` git
git status
```

#### Helpful status:
  * ' ' = unmodified
  * M = modified
  * A = added
  * D = deleted
  * R = renamed
  * C = copied
  * U = updated but unmerged
  
---

#### Difference between the staging and the working tree:

``` git
git diff
```

##### To show the difference between the staging and the current file version:

``` git
git diff --staged
```

---

#### adding/removing a file from staging:

``` git
git add [file]
```

#### To remove from staging (not the file):

``` git
git reset [file]
```

---

#### adding/removing hunks from staging:

``` git
git add -p [file]
```

``` git
git reset -p [file]
```

It will navigate between all hunks in an interactive mode.

---

### Committing

After staging we can register the current state:

---

#### With a message

``` git
git commit -m "A brief explanation about my work"
```

You can also tell the command to automatically stage files that have been modified and deleted, but it will not affect new files:

``` git
git commit -a
```

But, please, don't do it.

---

#### Fixing message

In case you had added a wrong message, you can fix it:

``` git
git commit --amend
```

---

#### Reverting commit

``` git
git revert [commit]
```

It will undo all changes from the commit and add it to the staging

---

### Reviewing history

---

#### log (and graph)

basic log:
``` git
git log
```

To follow all changes of a file (beyond renamings):
``` git
git log --follow [file path]
```

The see the changes:
``` git
git log -p [file path]
```

---

Do you need a visual help?

``` git
git log --graph
git log --graph --oneline
git log --graph --decorate
```

---

#### Log + search

To search in commit messages:

``` git
git log --grep "message"
```

By default, grep is case senstive, you can use `-i` to ignore it:

``` git
git log --grep -i "message"
```

---

To search in the history changes:

``` git
git log -G"message"
git log -S"message"
```

Helpful combinations:

``` git
git log --color-words -S"message"
git log -p -S"message"
git log --color-words -p -S"message"
```

---

#### show branch diff

``` git
git diff [branch1]..[branch2]
```
or
``` git
git diff HEAD..[branch2]
git diff ..[branch2]
```

---

#### show commit

``` git
git show [commit]
```

#### Checking author

``` git
git blame [path]
```

---

### Synchronizing changes

---

#### remotes

Once you need to synchronize your changes with a server or a team, you will need a remote:

``` git
git remote add [remote name] [remote url]
```

---

#### Fetch remote / all remotes

Fetch allows you to download the remote repository history:

``` git
git fetch [remote name]
git fetch --all
```

#### Pushing changes

``` git
git push [remote] [branch]
```

For new local branches, you need to set the remote branch relation:

``` git
git push --set-upstream [remote name] [remote branch]
```

---

#### Push --force

In case you need to replace a remote repository:

``` git
git push --force
```

DON'T use --force on public/shared branch

---

#### Merging branches

Merge is useful to bring the independent line of development to other branches:

``` git
git merge [branch]
```

In case you need to do more changes:

``` git
git merge --no-commit [branch]
```

---

#### Pull (syncing)

To sync your local repository with the remote:

``` git
git pull [remote]
```

This command is a sequence of `git fetch` and `git merge`

---

#### Rebase branch

Rebase is similar to merge, but it reapplies the commits on top of another branch

``` git
git rebase [branch]
```

Check more in https://hackernoon.com/git-merge-vs-rebase-whats-the-diff-76413c117333

  * Use merge in cases where you want a set of commits to be clearly grouped together in history
  * Use rebase when you want to keep a linear commit history
  * DON’T use rebase on a public/shared branch


---

## Going deeper

---

### Reflog

``` git
git reflog
```

The reflog is an ordered list of the commits that HEAD has pointed to.
The reflog isn't part of the repo itself (it's stored separately to the commits themselves)
It isn't included in pushes, fetches or clones; it's purely local.

---

### Conflicts

Sometimes, the remote or branch that you want to get changes can contain a different hunk.
In this case, git may not be able to auto-fix this, and you will need to act.

---

Example:

``` git
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

---

### Reseting

To clean your repository or reset the HEAD:

#### Resetting a specific file:

``` git
git reset -p [file path]
```

#### To resets the index and working tree discarding both:

``` git
git reset --hard [commit]
```

Any changes to tracked files in the working tree since `[commit]` are discarded.

---


#### To resets the index but not the working tree:

``` git
git reset --mixed [dommit]
```

The changed files are preserved but not marked for commit

#### To reset and keep the index and working tree:

``` git
git reset --soft [commit]
```

This leaves all your changed files "Changes to be committed"

---

### Patching

If you export `git diff` to a file, you can apply it in a different situation:

``` git
git diff > my-patch.diff
```

``` git
git apply my-patch.diff
```

---

### Cherry pick

Pick an exactly commit to where you're:

``` git
git cherry-pick [commit hash]
```

An example of cherry pick all commits from master branch:

``` git
git cherry-pick ..master
```

---

#### To continue the operation:

``` git
git cherry-pick --continue
``` 

#### To finish the current operation in progress.

``` git
git cherry-pick --quit
```

#### To cancel the operation:

``` git
git cherry-pick --abort
```

---

### Stash

You can also save changes on your side. It is useful for work in progress manipulation:

#### To save a staging state:

``` git
git stash
```

#### To load a stash:

``` git
git stash pop
```

#### To list all available stash:

``` git
git stash list
```

#### To delete a stash:

``` git
git stash drop
```

---

### The .git folder

You need to see to understand

---

#### .gitignore file

---

### Breadcrumb about the branch. Add to your `.bash_profile`:

``` git
  # Show current git branch in the command line
  
  parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
  }
  
  export PS1="\[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "
```

---

## Extras

---

### VSCode git support:

https://code.visualstudio.com/docs/editor/versioncontrol#_git-patchdiff-mode

---

### Maybe this talk was not necessary: 
https://services.github.com/on-demand/downloads/github-git-cheat-sheet

http://think-like-a-git.net/

---

Thank you! (Obrigado!)
