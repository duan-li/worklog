---
layout: page
title: User Manual
---

# User Manual

- [Introduction](#introduction)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)
- [Support](#support)

---

## Introduction

This manual provides guidance on setting up, configuring, and using the project. It is intended for developers, operators, and end users who need to understand the system's features and workflows.

---

## Installation

### Prerequisites

- **Git** 2.x or later
- **Ruby** 2.7+ (if using Jekyll-based features)
- **Bundler** (`gem install bundler`)
- **Docker** (optional, for containerized builds)

### Steps

1. Clone the repository:
   ```
   git clone https://github.com/user/repo.git
   cd repo
   ```

2. Install dependencies:
   ```
   bundle install
   ```

3. Build the project:
   ```
   bundle exec jekyll build
   ```

### Verify Installation

Run the local development server to confirm everything works:

```
bundle exec jekyll serve
```

Open a browser to `http://localhost:4000`.

---

## Configuration

### Site Configuration

Edit `_config.yml` to set your site's title, description, base URL, and theme.

```yaml
title: My Site
description: A description of the site
baseurl: ""
url: "https://example.com"
```

### Environment Variables

| Variable            | Description                  | Default   |
|---------------------|------------------------------|-----------|
| `JEKYLL_ENV`        | Build environment            | production|
| `BUNDLE_GEMFILE`    | Path to the Gemfile          | Gemfile   |

### Docker

Edit `docker-compose.yml` to adjust ports, volumes, or environment variables as needed.

---

## Usage

### Local Development

Start the development server with live reload:

```
bundle exec jekyll serve --livereload
```

### Build for Production

Generate the static site into `_site/`:

```
JEKYLL_ENV=production bundle exec jekyll build
```

### Creating Content

**New page:**
```
bundle exec jekyll page "Page Title"
```

**New post:**
```
bundle exec jekyll post "Post Title"
```

**New draft:**
```
bundle exec jekyll draft "Draft Title"
```

**Publish a draft:**
```
bundle exec jekyll publish _drafts/my-draft.md
```

---

## Troubleshooting

### `bundle install` fails

Ensure you have the correct Ruby version installed. Use `rbenv` or `rvm` to manage versions.

```
rbenv install 3.1.0
rbenv local 3.1.0
```

### Port already in use

Specify an alternate port:

```
bundle exec jekyll serve --port 4001
```

### Missing dependencies

Run `bundle update` to refresh the lockfile and install the latest compatible gems.

---

## Support

- **Issues:** Report bugs or feature requests on the [GitHub Issues](https://github.com/user/repo/issues) page.
- **Discussions:** Join the community discussion on GitHub Discussions.
- **Contributing:** See `CONTRIBUTING.md` for guidelines on submitting changes.

---

*Last updated: July 2026*