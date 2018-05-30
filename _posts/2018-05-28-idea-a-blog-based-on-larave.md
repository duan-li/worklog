---
layout: post
title: "[IDEA]A blog based on larave"
date: 2018-05-28 11:18 +0000
---

## Requirement
* Front-end
* Back-end
   * user can login
   * user can create website
   * user can link domain(s) to webiste. 
   * user can see posts of website


### Backend

```mermaid
graph TB

u[User] -- login --> dashboard(dashboard)
dashboard(dashboard) -- create --> website((websites))
dashboard(dashboard) -- add --> domains((domains))
domains -- link --> website
website((websites)) -- add --> post((post))
website((websites)) -- add --> page((page))
website((websites)) -- manage --> comment((comment))
website((websites)) -- manage --> tag((tag))
website((websites)) -- manage --> category((category))
website((websites)) -- manage --> attachments((attachments))

```


## Highlight
* `view()` generate html and store to memcache



# Decition
Not possible unless php fully supply markdown
- [ ]check if possiable let front end js to handle markdown coverting.


