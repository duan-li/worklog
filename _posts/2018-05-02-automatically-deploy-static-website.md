---
layout: post
title: Automatically deploy static website
date: 2018-05-02 11:06 +1000
---


```bash
FROM ubuntu:18.04

# How-To
 # Local Build: docker build -t lc/sw-toolbox:1 .
 # Local Run: docker run -it --name="toolbox" lc/sw-toolbox:1 /bin/bash
 # Restore Local Run: docker start -ai toolbox

 # USER root
ENV TZ=Australia/Melbourne
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
	apt-get update -y && \
	apt-get autoclean && \
	apt-get autoremove && \
    apt-get clean && \
	apt-get install -y zsh git nano wget \
					 autoconf libtool build-essential libffi-dev \
					 python python-pip \
					 ruby ruby-dev \
					 nodejs npm \
					 golang-go 


# AWS command line
RUN pip install awscli

# Ruby GEM Package
RUN gem install bundler


# Hugo (0.38)
# RUN wget https://github.com/gohugoio/hugo/releases/download/v0.38/hugo_0.38_Linux-64bit.deb && \
#	dpkg -i hugo_0.38_Linux-64bit.deb && \
#	rm hugo_0.38_Linux-64bit.deb



# Clean system
RUN apt-get autoremove && \
	apt-get clean autoclean && \
    rm -rf /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
```

```bash
git clone https://github.com/inputx/worklog.git;cd worklog

bundle install
jekyll build

aws configure <<< 'key
secr
reg
json'


aws s3 rm s3://good2all.com --recursive
aws s3 sync ./_site s3://good2all.com/
```