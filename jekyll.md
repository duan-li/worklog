---
layout: page
title: Jekyll
---

# Run in docker
```
docker run -it --rm -v ~/blog:/blog dockercraft/bundler
```

# Installation
**Initial** 
```
gem install jekyll bundler

```

**Create new website**
```
jekyll new my-awesome-site
```

## For an exist webiste
```
bundle install
bundle install --path vendor/bundle
```


# General Usage
**Build website**
```
jekyll build
```

```
bundle exec jekyll build
```

## Preview
**Start local server**
```
bundle exec jekyll serve
```

**Set listener**
```
bundle exec jekyll serve --host 0.0.0.0
```

**Set port**
```
bundle exec jekyll serve --port 3000
```



# Compose

## Installation
Add this line to your application's Gemfile:
```
gem 'jekyll-compose', group: [:jekyll_plugins]
```

And then execute:
```
bundle
```
or 
```
bundle install
```


## Usages
 - draft      Creates a new draft post with the given NAME
 - post       Creates a new post with the given NAME
 - publish    Moves a draft into the _posts directory and sets the date
 - unpublish  Moves a post back into the _drafts directory
 - page       Creates a new page with the given NAME

### Create new page
```
bundle exec jekyll page "My New Page"
```


```
jekyll page "My New Page"
```

### Create new post
```
bundle exec jekyll post "My New Post"
```

```
jekyll post "My New Post"
```

### Create new draft
```
bundle exec jekyll draft "My new draft"

```

```
jekyll draft "My new draft"

```

### Publish draft
```
bundle exec jekyll publish _drafts/my-new-draft.md
```

```
jekyll publish _drafts/my-new-draft.md
```

**specify a specific date on which to publish it**
```
jekyll publish _drafts/my-new-draft.md --date 2014-01-24
```

### Unpublish Post
```
bundle exec jekyll unpublish _posts/2014-01-24-my-new-draft.md
```

```
jekyll unpublish _posts/2014-01-24-my-new-draft.md
```

### Build index
```
bundle exec jekyll algolia
```


# Ignore files and folders
```
_site
.sass-cache
.jekyll-metadata
.puls.swp
.push
.bundle
.bundle/*
```

