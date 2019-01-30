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

# Theme develop

## Create theme [^1]

[^1]: [Creating your own Jekyll Theme Gem](https://medium.com/@jameshamann/creating-your-own-jekyll-theme-gem-1f8180a0e4b8)

```
jekyll new-theme sample-theme
cd sample-theme
```

## Config theme
On `sample-theme.gemspec` file

```
Gem::Specification.new do |spec|
  spec.name          = "sample-theme"
  spec.version       = "0.1.0"
  spec.authors       = [""]
  spec.email         = [""]
spec.summary       = %q{TODO: Write a short summary, because Rubygems requires one.}
  spec.homepage      = "TODO: Put your gem's website or public repo URL here."
  spec.license       = "MIT"
spec.files         = `git ls-files -z`.split("\x0").select { |f| f.match(%r{^(assets|_layouts|_includes|_sass|LICENSE|README)}i) }
spec.add_runtime_dependency "jekyll", "~> 3.6"
spec.add_development_dependency "bundler", "~> 1.12"
  spec.add_development_dependency "rake", "~> 10.0"
end
```

## Build theme

```
gem build sample-theme.gemspec
```


## Setup jekyll site
On your jekyll site, update `Gemfile`

```
gem "sample-theme", :path => "/var/theme"
```

## Install theme
```
bundle install
bundle install --path vendor/bundle
```

## config theme
```
# _config.yml

theme: sample-theme

```

## Build and run site

```
build exec jekyll build
build exec jekyll serve
```


# Config

## Show excerpts on post list.

```
show_excerpts: ture
```

Add `<!--more-->` post.


---

