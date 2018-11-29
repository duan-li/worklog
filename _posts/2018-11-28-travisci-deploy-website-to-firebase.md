---
layout: post
title: TravisCI deploy website to firebase
date: 2018-11-28 22:24 +0000
---


## Use `ubuntu` docker image
```
docker pull ubuntu
```

## Run docker container
```
docker run -it --rm -v /website:/website -p 9005:9005 ubuntu bash
```

## Inside of docker container
```
apt-get update -y

apt-get install npm ruby git ruby-dev -y

```

### firebase
Run firebase [^1]
```
npm install -g firebase-tools

cd /website

firebase login:ci

firebase init
```

### Travis CI
#### Install [^2]

```
gem install travis --no-rdoc --no-ri
travis login --pro
travis encrypt "key string" --add
```

config [^3]

[^1]: [firebase doc](https://firebase.google.com/docs/cli/?authuser=0)
[^2]: [travis command line](https://github.com/travis-ci/travis.rb#ubuntu)
[^3]: [travis doc](https://docs.travis-ci.com/user/deployment/firebase/)


---
