---
layout: post
title: PHP OAuth Server
date: 2018-07-30 15:36 +0000
---

https://www.sitepoint.com/creating-a-php-oauth-server/
https://github.com/phpmasterdotcom/CreatingAPHPOAuthServer
https://github.com/zorrodg/mworell-oauth-php

**include.php**
```php



```


## OAuth2 Demo PHP [^oauth.net]

[^oauth.net]: [oauth.net example](https://oauth.net/code/php/)
Need PHP 7.0 or above.

### Download code 

```bash
git clone https://github.com/bshaffer/oauth2-demo-php.git
```

### Prepare config

```bash
cp data/parameters.json.dist data/parameters.json
{
  "client_id": "demoapp",
  "client_secret": "demopass",
  "token_route": "grant", # first
  "authorize_route": "authorize",
  "resource_route": "access", #second
  "resource_params": {},
  "user_credentials": ["demouser", "testpass"],
  "http_options": { "exceptions": false }
}

sed -i '' 's?"grant"?"http://localhost:8081/lockdin/token"?g' data/parameters.json
{
  "client_id": "demoapp",
  "client_secret": "demopass",
  "token_route": "http://localhost:8081/lockdin/token",
  "authorize_route": "authorize",
  "resource_route": "access",
  "resource_params": {},
  "user_credentials": ["demouser", "testpass"],
  "http_options": { "exceptions": false }
}

sed -i '' 's?"access"?"http://localhost:8081/lockdin/resource"?g' data/parameters.json
{
  "client_id": "demoapp",
  "client_secret": "demopass",
  "token_route": "http://localhost:8081/lockdin/token",
  "authorize_route": "authorize",
  "resource_route": "http://localhost:8081/lockdin/resource",
  "resource_params": {},
  "user_credentials": ["demouser", "testpass"],
  "http_options": { "exceptions": false }
}
```


### Start server

```bash
cd web
# 8080 client and app
# 8081 oauth server
php -S localhost:8080 & php -S localhost:8081
```




