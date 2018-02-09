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

## Branch
> List all branchs
`git branch`

> Create new branch
`git branch <name>`

> Remove branch
`git branch -d <name>`

> check out branch
`git checkout <branch-name>`

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

## Remote
> Set a new remote
`git remote add origin https://github.com/user/repo.git`

> Verify new remote
`git remote -v`

> Fetch remote branch
`git fetch origin`

> Push to remote branch
`git push origin master`