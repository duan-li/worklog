---
layout: post
title: Codeception test DB with .env file
date: 2018-12-19 10:08 +0000
---

In file `codeception.yml` add
```yml
params:
	- .env
```

like 
```yml
paths:
  tests: tests
  output: tests/_output
  data: tests/_data
  support: tests/_support
  envs: tests/_envs
actor_suffix: Tester
extensions:
  enabled:
  - Codeception\Extension\RunFailed
params:
  - .env
```

In `*.suite.yml` files
```yml
actor: AcceptanceTester
modules:
  enabled:
  - PhpBrowser:
      url: http://localhost:8000
  - Db:
      dsn: "mysql:host=%ORDERS_DATABASE_HOST%;dbname=%ORDERS_DATABASE_NAME%"
      user: "%ORDERS_DATABASE_USERNAME%"
      password: "%ORDERS_DATABASE_PASSWORD%"
      databases:
        orderDB:
          dsn: "mysql:host=%ORDERS_DATABASE_HOST%;dbname=%ORDERS_DATABASE_NAME%"
          user: "%ORDERS_DATABASE_USERNAME%"
          password: "%ORDERS_DATABASE_PASSWORD%"
        newsDB:
          dsn: "mysql:host=%NEWS_DATABASE_HOST%;dbname=%NEWS_DATABASE_NAME%"
          user: "%NEWS_DATABASE_USERNAME%"
          password: "%NEWS_DATABASE_PASSWORD%"
  - \Helper\Acceptance

```

In test cest.

```php
public function accessDB(\AcceptanceTester $I)
{
    $I->amConnectedToDatabase('orderDB');
    $I->seeInDatabase('table_name', ['column_name' => 'value']);
    $I->amConnectedToDatabase('newsDB');
    $I->seeInDatabase('table_name', ['column_name' => 'value']);
}
```




---