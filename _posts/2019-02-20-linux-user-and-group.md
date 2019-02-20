---
layout: post
title: Linux user and group
date: 2019-02-21 10:03 +0000
---


### List all user

```
cat /etc/passwd
```

### List all group

```
cat /etc/group
```

### Create user

```
adduser user-name
```


### Create group
```
groupadd group-name
```


### Check my group

```
groups
groups user-name
```


### Check user group

```
groups user-name
```

### Add user to group [^1]

```
usermod -a -G group-name user-name
```

[^1]: [How to add existing user to an existing group?](https://askubuntu.com/questions/79565/how-to-add-existing-user-to-an-existing-group)



---