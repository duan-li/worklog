---
layout: post
title: Update .env file by bash shell script
date: 2019-04-18 03:15 +0000
---


`ini` file or `.env` file

```ini
RELEASE_DATA='Thu 18 Apr 2019 13:03:46 AEST'
```

Shell script [^1]

[^1]: [find command working with sed command](https://stackoverflow.com/questions/19456518/invalid-command-code-despite-escaping-periods-using-sed)

```bash
#!/bin/bash

datetime=$(date)

find ./env -type f -exec sed -i '' -e "/^RELEASE_DATA=/s/=.*/=\'$datetime\'/" {} \;

```

---