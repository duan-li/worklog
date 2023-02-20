---
layout: post
title: Vim development environment
date: 2022-06-24 01:03 +0000
categories: [Development]
tags: [vim, editor, ide]
---

Vim (Vi Improved) is a highly configurable, powerful, and widely used text editor available on various platforms, including Linux, macOS, and Windows. It is based on the older Vi editor, which was originally created for the Unix operating system.

Vim is known for its modal editing approach, where it provides different modes for different tasks, such as normal mode for navigation and editing commands, insert mode for inserting text, visual mode for selecting text, and more. This modal editing paradigm allows for efficient and fast text editing once you become familiar with the editor.


## Use Vim as IDE

Vim can be configured and customized to serve as a powerful programming IDE (Integrated Development Environment). By installing plugins and making certain configurations, you can enhance Vim's capabilities for coding and make it more suitable for software development. 

### Configuring Vim

1. Plugin Manager: Install a plugin manager for Vim, such as Vundle, Pathogen, or vim-plug. These managers simplify the process of installing and managing plugins. Instructions for installation can be found on their respective GitHub repositories.

1. Syntax Highlighting: Enable syntax highlighting in Vim to visually differentiate different programming language elements. Vim already supports syntax highlighting for many languages by default. If you want to add support for additional languages, you can install plugins like `vim-polyglot` or specific language syntax plugins.

1. Code Completion: Install a code completion plugin to assist you while writing code. Plugins like `YouCompleteMe`, `coc.nvim`, or `deoplete` provide intelligent code completion capabilities for various programming languages.

1. Linter/Static Analysis: Set up a linter or static analysis tool to check your code for errors or potential issues. Plugins like `ALE` (Asynchronous Lint Engine), `syntastic`, or language-specific linter plugins can be used to integrate these tools into Vim.

1. Tagging and Navigation: Install a tags plugin such as `ctags` and a related Vim plugin (`tagbar`, `gutentags`) to generate and navigate through tags for functions, classes, and variables within your codebase. This allows for quick code navigation.

1. Git Integration: If you are using Git for version control, consider installing plugins like `vim-fugitive` or `vim-gitgutter` to provide Git integration within Vim. This enables features like viewing file diffs, staging changes, and more.

1. Customization and Keybindings: Customize Vim to match your preferences and workflow. You can modify the appearance, define custom keybindings, create code snippets, and configure various options according to your needs. This is typically done in your `.vimrc` configuration file.


## Vim as IDE for specific language

### For `python`

Vim can be an excellent choice for Python development, offering a lightweight and efficient environment for coding.

* [Vim python](https://www.fullstackpython.com/vim.html)
* [Vim python IDE](https://zhuanlan.zhihu.com/p/30022074)


### For `golang`


Vim can be an excellent choice for Golang development, offering a lightweight and efficient environment for coding. 

* [Vim Go IDE](https://learnku.com/articles/24924)


### For `PHP`

Vim can be a powerful choice for PHP development, providing a flexible and customizable environment for coding.

* [Vim PHP IDE](https://thevaluable.dev/vim-php-ide/)

### Other

* [How to Update Basic Settings in Vim](https://www.freecodecamp.org/news/vimrc-configuration-guide-customize-your-vim-editor/)


### Example

```
"------------------------------------------------------
" basic setting
set nocompatible
syntax on
filetype plugin indent on
set ic
set hlsearch
set incsearch
set noswapfile
set encoding=utf-8
set fileencodings=utf-8,ucs-bom,GB2312,big5
set cursorline
set autoindent
set smartindent
set scrolloff=4
set showmatch
set nu
set ts=4
set expandtab
set shiftwidth=4
set number



function! ToggleVerbose()
    if !&verbose
        set verbosefile=~/.vim/verbose.log
        set verbose=15
    else
        set verbose=0
        set verbosefile=
    endif
endfunction


"------------------------------------------------------
" python setting
let python_highlight_all=1
au Filetype python set tabstop=4
au Filetype python set softtabstop=4
au Filetype python set shiftwidth=4
au Filetype python set textwidth=79
au Filetype python set expandtab
au Filetype python set autoindent
au Filetype python set fileformat=unix
autocmd Filetype python set foldmethod=indent
autocmd Filetype python set foldlevel=99



"------------------------------------------------------
" F5 key press run code
map <F5> :call CompileRunGcc()<CR>
func! CompileRunGcc()
        exec "w"
        if &filetype == 'c'
                exec "!g++ % -o %<"
                exec "!time ./%<"
        elseif &filetype == 'cpp'
                exec "!g++ % -o %<"
                exec "!time ./%<"
        elseif &filetype == 'java'
                exec "!javac %"
                exec "!time java %<"
        elseif &filetype == 'sh'
                :!time bash %
        elseif &filetype == 'python'
                exec "!clear"
                exec "!time python3 %"
        elseif &filetype == 'html'
                exec "!firefox % &"
        elseif &filetype == 'go'
                " exec "!go build %<"
                exec "!time go run %"
        elseif &filetype == 'mkd'
                exec "!~/.vim/markdown.pl % > %.html &"
                exec "!firefox %.html &"
        endif
endfunc



" STATUS LINE ------------------------------------------------------------

" Clear status line when vimrc is reloaded.
set statusline=

" Status line left side.
set statusline+=\ %F\ %M\ %Y\ %R

" Use a divider to separate the left side from the right side.
set statusline+=%=

" Status line right side.
set statusline+=\ ascii:\ %b\ hex:\ 0x%B\ row:\ %l\ col:\ %c\ percent:\ %p%%

" Show the status on the second to last line.
set laststatus=2


```
