---
layout: post
title: CI/CD policy
date: 2018-05-11 10:28 +0000
---

## Request
 - Test case: run test case, all should pass
 - Test case coverage: test case coverage should cover most of code
 - Code style: psr-2.
 - Code analysis: code qaulity
 - Build: build project
 - deploy: deploy project

No compiled js or css file commit to repo. (reduce size of repo)
Those js or css only compile in CD process.

## Resources and Services
 - Test case 
 - varCI: PR and issue management
 - CodeCov code test coverage
 - coveralls.io code test case coverage
 - sonarqube
 - [buddy ci/cd](https://buddy.works/guides/first-steps-with-laravel-and-continuous-delivery), [Example like laravel](https://buddy.works/guides/first-steps-with-laravel-and-continuous-delivery)