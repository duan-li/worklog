---
layout: post
title: Vim development environment
date: 2022-06-24 01:03 +0000
---

## For `python`

* [Vim python](https://www.fullstackpython.com/vim.html)
* [Vim python IDE](https://zhuanlan.zhihu.com/p/30022074)


## For `golang`

* [Vim Go IDE](https://learnku.com/articles/24924)


## For `PHP`

* [Vim PHP IDE](https://thevaluable.dev/vim-php-ide/)

## Other

* [How to Update Basic Settings in Vim](https://www.freecodecamp.org/news/vimrc-configuration-guide-customize-your-vim-editor/)

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



" STATUS LINE ------------------------------------------------------------ {{{

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

" }}}

```
