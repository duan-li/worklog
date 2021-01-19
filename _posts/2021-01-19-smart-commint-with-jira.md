---
layout: post
title: Smart commint with JIRA
date: 2021-01-19 05:14 +0000
---


When you manage your project's repositories in Bitbucket or GitHub, or use Fisheye to browse and search your repositories, you can process your Jira Software issues using special commands, called Smart Commits, in your commit messages.[^1]

[^1]: [Process issues with smart commits](https://support.atlassian.com/jira-software-cloud/docs/process-issues-with-smart-commits/)

You can:

* comment on issues
* record time tracking information against issues
* transition issues to any status defined in the Jira Software project's workflow.

### Comment

> JRA-34 #comment corrected indent issue

### Time 

> JRA-34 #time 1w 2d 4h 30m Total work logged

### Workflow

> JRA-090 #close #comment Fixed this today

* `#start-review`
* `#start-progress`


## Example

> JRA-123 #comment Imagine that this is a really, and I mean really, long comment #time 2d 5h

> JRA-123 JRA-234 JRA-345 #resolve

> JRA-123 JRA-234 JRA-345 #resolve #time 2d 5h #comment Task completed ahead of schedule

