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

> Check staged file different
`git diff --staged`

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

> Show last commit hash
`git rev-parse --verify HEAD` or `git rev-parse HEAD`

> Show last commit hash (short)
`git rev-parse --short HEAD`


## Branch
> List all branchs
`git branch -a`

> list remote branch
`git branch -r`

> Create new branch
`git branch <name>`

> Remove branch
`git branch -d <name>`

> check out branch
`git checkout <branch-name>` `git checkout -b <branch-name>`

> merge branch into current branch
`git merge from-branch`

> push branch with username and password 
`git push https://username:password@myrepository.biz/file.git --all`

> push branch to origin
`git push -u origin <branch-name>`

> get branch first commit
`git log master..<branch-name> --oneline | tail -1`

> get branch last commit
`LC-4174-suncorp-map-users-to-ids --oneline | head -1`

> archive branch [^3]
```
git tag archive/<branchname> <branchname>
git branch -d <branchname>
```

[^3]: [How can I archive git branches?](https://stackoverflow.com/questions/1307114/how-can-i-archive-git-branches)

> unarchive branch
`git checkout -b <branchname> archive/<branchname>`


## Remote

> prunes tracking branches not on the remote.
`git remote prune origin`

> lists branches that have been merged into the current branch.
`git branch --merged`


> deletes branches listed on standard input.
`xargs git branch -d`


> Remove tracking branches no longer on remote [^rm_remote_b]

[^rm_remote_b]: [Remove tracking branches no longer on remote](https://stackoverflow.com/questions/7726949/remove-tracking-branches-no-longer-on-remote)

```bash
git branch --merged > /tmp/merged-branches && \
  vi /tmp/merged-branches && \
  xargs git branch -d < /tmp/merged-branches && \
  rm /tmp/merged-branches
```



## Commit empty directory

Create a `.gitignore` file in directory.

```
# Ignore everything in this directory
*
# Except this file
!.gitignore
```


## Tag
> List all tags
`git tag`

> List all remote tags [^1]
`git ls-remote --tags ./.`

[^1]: [How to see remote tags?
](https://stackoverflow.com/questions/25984310/how-to-see-remote-tags)

> List all remote tags start with `v` [^2]
`git ls-remote --tags origin v\*`

[^2]: [git-ls-remote](https://git-scm.com/docs/git-ls-remote.html)

> Create Tag
`git tag -a v1.4 -m "my version 1.4"`

> Remvoe tag
`git tag -d <name>`





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


> In order to clean up remote-tracking branches while fetching, use the “git fetch” command with the “–prune” option. [^git_remote_fetch]
`git fetch --prune origin`

[^git_remote_fetch]: [how-to-clean-up-git-branches](https://devconnected.com/how-to-clean-up-git-branches/)


## Pull request (Github)
Update `.git/config`
```
[remote "origin"]
	url = git@bitbucket.org:loyaltycorp/rewards.git
	fetch = +refs/heads/*:refs/remotes/origin/*
	fetch = +refs/pull/*/head:refs/remotes/origin/pr/*
```

run `git fetch origin`

See [this](https://gist.github.com/piscisaureus/3342247)

## Other
### Repo size
[Ref](https://stackoverflow.com/questions/8185276/find-size-of-git-repo)

`git count-objects -vH`

### File size
[How to find/identify large files/commits in Git history?](https://stackoverflow.com/questions/10622179/how-to-find-identify-large-files-commits-in-git-history)
```
# need run brew install coreutils
git rev-list --objects --all \
| git cat-file --batch-check='%(objecttype) %(objectname) %(objectsize) %(rest)' \
| sed -n 's/^blob //p' \
| sort --numeric-sort --key=2 \
| cut -c 1-12,41- \
| gnumfmt --field=2 --to=iec-i --suffix=B --padding=7 --round=nearest
```

### Reduce Repo size
`git reflog expire --all --expire=now`
`git gc --prune=now --aggressive`


### Revert last commit
```
git reset HEAD~ 
// do some update
git add ...   
git commit -c ORIG_HEAD

git push --force
```

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
* `h`: help view

### Status view
* `u`: add file or unstage file
* `C`: make a commit


## Bind shortcut key

`bind status P !git push origin`

`bind P !git push origin`


## Tig refs
 - http://jonas.nitro.dk/tig/manual.html
 - https://devhints.io/tig


## Tig sheet
 - git fetch
 - git reset
 - git commit
 - git push
 - git pull
 - git diff `file`
 - git diff `branch`
 - git stack
 

## `.tigrc` example [^tigrc]

[^tigrc]: [tig document](https://jonas.github.io/tig/doc/tigrc.5.html)

```bash
bind status P !git push --set-upstream origin
bind status U !git pull origin
bind status T ?git checkout %(file)

bind refs P ?git push --set-upstream origin %(branch)
bind refs F ?git branch "%(prompt Enter branch name: )"
bind refs G ?git merge %(branch)
bind refs T ?git push --delete origin %(tag)
bind refs ! ?git branch --merged > /tmp/merged-branches && vi /tmp/merged-branches && xargs git branch -d </tmp/merged-branches && rm /tmp/merged-branches

bind refs L !git pull
bind refs E !git fetch --prune origin
bind refs M !git checkout master
```


---
