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
  scripts:
   - cd ..
   - ls
 002:
  name: 'production server 2'
  scripts:
   - cd ..
   - ls
   
uat:
 005:
  name: 'build image and UAT'
  scripts:
   - ls
   - pwd
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

---