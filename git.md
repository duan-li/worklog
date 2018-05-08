---
layout: page
title: GIT
---

## Basic
> Initial git repo
`git init`

> Config user name
`git config user.name "Name"`

> Config user email
`git config user.email "name@email.com"`

> Check unstage changes
`git status`

> Check changes for single file
`git diff <file>`

> Add all files, a single file or a dir
`git add */<file>/<dir>`
or
`git add -A`

> Make a commit with message
`git commit -m "commit message"`

> Make a commit and use a text file as commit message
`git commit -F <file>`

## Commit

> Check changes in a git commit
`git diff <commitID>^!`
`git diff-tree -p <commitID>`

> Serach keyword from commit message
`git log --grep=<keyword>`

## Branch
> List all branchs
`git branch`

> Create new branch
`git branch <name>`

> Remove branch
`git branch -d <name>`

> check out branch
`git checkout <branch-name>`

> merge branch into current branch
`git merge from-branch`

## History
> check commit history
`git log`

> check history with file name
`git log --name-only`

> check history with file status
`git log --name-status`

> check history with file statistic
`git log --stat`

> history order reverse
`git log --reverse`

> View the change history of a file or dir
`git log -p dirname/filename`

> simplify history message
`git log --oneline -- _includes/`

## Remote
> Set a new remote
`git remote add origin https://github.com/user/repo.git`

> Verify new remote
`git remote -v`

> Fetch remote branch
`git fetch origin`

> Push to remote branch
`git push origin master`


# Tig
## Install
`brew install tig`

## View 
* `m`: Main view
* `s`: status view like `git status`
* `l`: log view like `git log`
* `d`: diff view like `git diff`
* `r`: branch refs view like `git branch`, but it shows remote branchs
* `c`: stage view

### Status view
* `u`: add file or unstage file
* `C`: make a commit
* ``


## Bind shortcut key

`bind status P !git push origin`

`bind P !git push origin`