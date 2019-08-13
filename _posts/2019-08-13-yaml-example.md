---
layout: post
title: Yaml example
date: 2019-08-13 01:18 +0000
---

[Online YAML editor](https://onlineyamltools.com/edit-yaml)

```yaml
name: ""
url: ""
items: 
  -
    name: "title"
    path: "" # filter
    position: "first" # eq 0, last, siblings, children
    content: "text"
  - 
    name: "price"
    path: ""
    position: "first"
    content: "text"

```
```json

Array
(
    [name] =>
    [url] =>
    [items] => Array
        (
            [0] => Array
                (
                    [name] => title
                    [path] =>
                    [position] => first
                    [content] => text
                )

            [1] => Array
                (
                    [name] => price
                    [path] =>
                    [position] => first
                    [content] => text
                )

        )

)
```


```yaml
production:
 001:
  name: 'production server 1'
  trigger: 'new-tag'
  validation: ''
  scripts:
   - cd ..
   - ls
  email_result_to: devops@com.au
  
 002:
  name: 'production server 2'
  trigger: 'new-tag'
  validation: ''
  scripts:
   - cd ..
   - ls
   
uat:
 005:
  name: 'deploy to UAT'
  trigger: 'pr-marge'
  validation: 'develop'
  scripts:
   - ls
   - pwd

worker:
 005:
  name: 'Build docker image'
  trigger: 'pr-marge'
  validation: 'master'
  scripts:
   - docker build .
   - docker push image

```

```json
Array
(
    [production] => Array
        (
            [001] => Array
                (
                    [name] => production server 1
                    [scripts] => Array
                        (
                            [0] => cd ..
                            [1] => ls
                        )

                )

            [002] => Array
                (
                    [name] => production server 2
                    [scripts] => Array
                        (
                            [0] => cd ..
                            [1] => ls
                        )

                )

        )

    [uat] => Array
        (
            [005] => Array
                (
                    [name] => build image and UAT
                    [scripts] => Array
                        (
                            [0] => ls
                            [1] => pwd
                        )

                )

        )

)
```


```yaml
environment:
 prod-001:
  jobs:
    - prod-deploy
 prod-002:
  jobs:
    - prod-deploy
 uat-005:
  jobs:
    - uat-deploy
    - prod-build

job:
 prod-deploy:
  name: production deploy
  trigger: new-tag
  validation: ''
  script:
   - docker pull
   - composer down
   - composer up
   - docker rmi
 prod-build:
  name: build production image
  trigger: pr-marge
  validation: 'master'
  script:
   - git pull
   - cp .env
   - docker build
   - docker push
 uat-deploy:
  name: UAT deploy
  trigger: pr-marge
  validation: 'develop'
  script:
   - cd dir
   - git pull
```

```php

interface Job 
{
  // __construct($array);
  public function getName(): string;
  public function getTrigger(): string;
  public function getStript(): array;
}

interface Validation
{
  // __construct($rule)
  public function isValid($trigger): bool;
}

interface Config
{
  // __construct($dotEnv)
  public function set($key, $value): bool;
  public function get($key);
  public function has($key): bool;
  public function del($key): bool;
}

interface Environment
{
  // __construct($name)
  public function setJobs(array $jobs): this;
  public function setConfig(Config $config): this;
  public function getName(): string;
  public function getJobs(): array;
}


interface AssemblyLine
{
  // __construct($dotEnv)
  public function conveyor(Environment $env): this;
  public function produce($trigger);
}
```

---