---
layout: post
title: GIT SSH key
date: 2019-01-02 21:31 +0000
---

**Generate key [^1]**

`ssh-keygen -t rsa -C "your_email@example.com"`

[^1]: [Creating SSH keys](https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html?utm_campaign=in-app-help&utm_medium=in-app-help&utm_source=stash)


```
cd ~/.ssh
ls
```

* `id_rsa.pub`: public key [^2]
* `id_rsa`: private key [^3]

[^2]: [SSH user keys for personal use](https://confluence.atlassian.com/bitbucketserver/ssh-user-keys-for-personal-use-776639793.html)

[^3]: [How to Set Up SSH Keys on CentOS 7](https://linuxize.com/post/how-to-set-up-ssh-keys-on-centos-7/)

---