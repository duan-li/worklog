---
layout: post
title: Oh my zsh on MacOS
date: 2018-10-31 22:57 +0000
---

1. Use `brew install zsh zsh-completions` install zsh [^1]
2. Install `oh-my-zsh` by using `sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"` [^2]
3. Edit file `~/.zshrc`
4. Change your default shell `chsh -s /bin/zsh`
5. Setup font [^3], Set this font in iTerm2 (14px is my personal preference) (iTerm → Preferences → Profiles → Text → Change Font).


[^1]: [Installing ZSH](https://github.com/robbyrussell/oh-my-zsh/wiki/Installing-ZSH)
[^2]: [Using Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh)
[^3]: [Install a patched font](https://gist.github.com/kevin-smets/8568070#install-a-patched-font)


After `brew install zsh zsh-completions`, can see.
```bash

To activate these completions, add the following to your .zshrc:

  autoload -Uz compinit
  compinit

You may also need to force rebuild `zcompdump`:

  rm -f ~/.zcompdump; compinit

Additionally, if you receive "zsh compinit: insecure directories" warnings when attempting
to load these completions, you may need to run this:

  chmod -R go-w '/usr/local/share/zsh'

zsh completions have been installed to:
  /usr/local/share/zsh/site-functions

```


## Edit file `~/.zshrc`

### Update theme 
```
ZSH_THEME="agnoster"
```

### Update plugins
```
plugins=(
  git
  dotenv
  osx
  docker
  docker-compose
  iterm2
  laravel5
  sublime
  composer
)
```

## Plugins

### git [^7]

* `gss`: `git status -s`
* `gst`: `git status`
* `ga`: `git add`
* `gaa`: `git add --all`
* `gapa`: `git add --patch`
* `gcmsg`: `git commit -m`
* `glg`: `git log --stat --max-count = 10`
* `ggp`: `git push`
* `gl`: `git pull`


### web-search [^4]
* `google keyword` open web page with google search

### sublime [^5]

* `st` open sublime
* `st filename` open file in sublime
* `stt` open current in sublime
* `sst` sudo sublime

### osx [^6]


| Command         | Description                                         |
| :-------------- | :-------------------------------------------------- |
| `tab`           | Open the current directory in a new tab             |
| `split_tab`     | Split the current terminal tab horizontally         |
| `vsplit_tab`    | Split the current terminal tab vertically           |
| `ofd`           | Open the current directory in a Finder window       |
| `pfd`           | Return the path of the frontmost Finder window      |
| `pfs`           | Return the current Finder selection                 |
| `cdf`           | `cd` to the current Finder directory                |
| `pushdf`        | `pushd` to the current Finder directory             |
| `quick-look`    | Quick-Look a specified file                         |
| `man-preview`   | Open a specified man page in Preview app            |
| `showfiles`     | Show hidden files                                   |
| `hidefiles`     | Hide the hidden files                               |
| `itunes`        | Control iTunes. Use `itunes -h` for usage details   |
| `spotify`       | Control Spotify and search by artist, album, track… |
| `rmdsstore`     | Remove .DS\_Store files recursively in a directory  |


[^4]: [plugins/web-search](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins/web-search)
[^5]: [plugins/sublime](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins/sublime)
[^6]: [plugins/osx](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins/osx)
[^7]: [Cheatsheet](https://github.com/robbyrussell/oh-my-zsh/wiki/Cheatsheet#git)

---