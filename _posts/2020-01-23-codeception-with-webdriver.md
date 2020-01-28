---
layout: post
title: Codeception with webdriver
date: 2020-01-23 22:09 +0000
---


```bash
# install codeception framework
composer require --dev codeception/codeception

# install webdriver module
composer require --dev codeception/module-webdriver

# This module was bundled with Codeception 2 and 3, but since version 4 it is necessary to install it separately.
codecept init upgrade4

# or
vendor/bin/codecept init upgrade4


```


Original `*.suite.yml` will be like 

```yaml

actor: AcceptanceTester
modules:
  enabled:
  - PhpBrowser:
      url: http://localhost:8000
  - \Helper\Acceptance

```

After change

```yaml
actor: AcceptanceTester
modules:
  enabled:
  - PhpBrowser:
      url: http://mp.test
      port: 9515
      browser: chrome
      capabilities:
        "goog:chromeOptions": # additional chrome options
  - \Helper\Acceptance
```

For `url` if is in Docker container, `http://localhost:8000` may not working, should using `http://<service-name>:8000`, the `<service-name>` can be find in `docker-compose.yaml` file.




https://codeception.com/docs/modules/WebDriver.html#algolia:p:nth-of-type(2)

