---
layout: post
title: Jekyll algolia
date: 2018-05-10 05:44 +0000
---

### ENV
Make sure your OS support zlib (linux package)
Example of alpine linux 
```
apk add zlib-dev
```


### Update **Gemfile** file
```
group :jekyll_plugins do
  gem 'jekyll-algolia', '~> 1.0'
end
```

### Run command
```
bundle install
```


### Update `_config.yml`
```
algolia:
  application_id: 'algolia app id'
  index_name: index_name

```

### System var

```
export ALGOLIA_API_KEY='admin api key'
export ALGOLIA_INDEX_NAME='index_name'
```

### Build index
```
bundle exec jekyll algolia
```


