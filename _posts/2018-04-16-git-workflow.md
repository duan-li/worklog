---
layout: post
title: GIT workflow
date: 2018-04-16 11:53 +1000
---


# Branch
## Branch type
 - Feature
 - Hot Fixes
 - Master
 - Release
 - Staging
 - Maintenance

Any new branch you start, either hot fix or feature, you should always branch off from master.
You do the magic and once you have finished, you merge master again in your brach to keep it up to date
If your current branch needs some other feature that is not in master but in release. You can merge that feature branch in to your current branch instead of release.


# Commit
```
Short (50 chars or less) summary of changes

More detailed explanatory text, if necessary.  Wrap it to about 72
characters or so.  In some contexts, the first line is treated as the
subject of an email and the rest of the text as the body.  The blank
line separating the summary from the body is critical (unless you omit
the body entirely); tools like rebase can get confused if you run the
two together.

Further paragraphs come after blank lines.

  - Bullet points are okay, too

  - Typically a hyphen or asterisk is used for the bullet, preceded by a
    single space, with blank lines in between, but conventions vary here

```

## Hot Fixes branch
```mermaid
graph TB
M1((Master Branch)) --fork--> M2((Master Branch))
M2((Master Branch)) --> M3((Master Branch))



M1((Master Branch)) --> W1((Work Branch))
W1((Work Branch)) --> W2[Commit work]
W2[Commit work] --> W3((Work Branch))
M2((Master Branch)) --resolve conflict--> W3((Work Branch))
W3((Work Branch)) --> P{Pull request}
P{Pull request} --merge to--> M3((Master Branch))
```


## Feature branch
```mermaid
graph TB

```


## Release branch

Branch name is `release-<release-number>`. `release-number` will be `platform-version-frameword-version-<any-number>`. 
	







Ref 
https://git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project
https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow