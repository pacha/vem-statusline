
Vem Statusline
==============

Vem Statusline is a simple and fast statusline for Vim.

![VemStatusline](doc/images/vem-statusline-dark.png)

It displays:

* Current active mode

* Current Git branch (requires [vim-gitbranch](https://github.com/itchyny/vim-gitbranch))
  or [fugitive.vim](https://github.com/tpope/vim-fugitive))

* Filename

* Indentation type and size (`tabs`, `spaces`, `tabs+spaces`)

* File enconding (eg. `utf-8`, `latin-1`  or `cp1251`)

* Newline type (Unix: `LF`, Windows: `CRLF`, Mac pre-OSX: `CR`)

* Position in the file (line:column) and percentage progress through the file

Vem Statusline is designed to be a very fast, small plugin and oriented to
people that want a bit more information in the statusline than the one provided
by default but that don't want to install a complex plugin for that.

If you prefer a plugin with more configuration options and that allows you to
define a great deal of elements and their positions, you can check the
following ones that are very popular:

* [lightline.vim](https://github.com/itchyny/lightline.vim): It allows you to
  define your own components and to completely configure the statusline.

* [airline.vim](https://github.com/vim-airline/vim-airline): Large,
  full-fledged statusline plugin with lots of options and that integrates with
  many other popular plugins.

In any case, Vem Statusline does provide some configuration options: you can
enable/disable any element in the statusline and you can also define custom
colors (see the *Colors* and *Configuration* sections).

*Note*: Vem Statusline is a component of a bigger Vim configuration setup named
Vem -still in the works-. Hence the plugin name. In any case, Vem Statusline
can be used totally independently from the Vem project. Other components of the
project are:

* [Vem Tabline](https://github.com/pacha/vem-tabline): A plugin to show the
  list of buffers in the tabline.

* [Vem Colors](https://github.com/pacha/vem-colors): A dark color scheme for
  Vim based on Wombat.

Installation
------------

You can use Vem Statusline straight away after installation. However, by
default Vim only shows the statusline if there are at least two windows. So if
you always want to have the statusline displayed, add this to your `.vimrc`
file:
```
set laststatus=2
```
Also, since the mode can be shown now in the statusline, you may also avoid
displaying the mode messages like:
```
-- INSERT --
```
at the bottom of the screen by also setting:
```
set noshowmode
```

Colors
------

By default, Vem Statusline uses the standard `StatusLine` and `StatusLineNC`
highlighting groups, which means that the statusline colors will automatically
adapt to your currently active color scheme.

However, you can also define specific colors for different parts of the
statusline:

Highlighting Group        | Default    | Color for
--------------------------|------------|-----------------------------------
VemStatusLineMode         | StatusLine | Mode indicator
VemStatusLineBranch       | StatusLine | Current Git Branch
VemStatusLineFileModified | StatusLine | File modified indicator (`*`) 
VemStatusLineFileRO       | StatusLine | Read-only file indicator (`[RO]`)
VemStatusLinePosition     | StatusLine | Position indicator (`line:col`)
VemStatusLineSeparator    | StatusLine | Symbols to separate elements (`|`)

For example, for a dark themed statusline, you can add this to your
configuration:

![DarkStatusline](doc/images/vem-statusline-dark.png)

```
highlight VemStatusLineMode         guifg=#cae682 guibg=#373737 gui=bold
highlight VemStatusLineBranch       guifg=#999999 guibg=#373737 gui=none
highlight VemStatusLineFileModified guifg=#cae682 guibg=#373737 gui=bold
highlight VemStatusLineFileRO       guifg=#e5786d guibg=#373737 gui=bold
highlight VemStatusLineSeparator    guifg=#999999 guibg=#373737 gui=none
highlight VemStatusLinePosition     guifg=#f6f3e8 guibg=#373737 gui=bold
```

For a light themed statusline, the configuration could be something like:

![LightStatusline](doc/images/vem-statusline-light.png)

```
highlight StatusLine                guifg=#272727 guibg=#e8e8e8 gui=none
highlight VemStatusLineMode         guifg=#228080 guibg=#e8e8e8 gui=bold
highlight VemStatusLineBranch       guifg=#777777 guibg=#e8e8e8 gui=none
highlight VemStatusLineFileModified guifg=#8ac6f2 guibg=#e8e8e8 gui=bold
highlight VemStatusLineFileRO       guifg=#e5786d guibg=#e8e8e8 gui=bold
highlight VemStatusLineSeparator    guifg=#777777 guibg=#e8e8e8 gui=none
highlight VemStatusLinePosition     guifg=#202020 guibg=#e8e8e8 gui=bold
```

Displaying the current Git branch
---------------------------------

Vem Statusline can optionally display the current branch of the repository
you're working on. To do so you need a Git Vim plugin.

If you don't have any Git Vim plugin and just want to display the name of
the branch, install:

* [vim-gitbranch](https://github.com/itchyny/vim-gitbranch)

And set the following variable in your `.vimrc` file:
```
let g:vem_statusline_branch_function = 'gitbranch#name'
```
This plugin by itchyny provides just the functionality to retrieve the
branch name.

If you have installed or prefer to use:

* [fugitive.vim](https://github.com/tpope/vim-fugitive)

by Tim Pope, the value to add is:
```
let g:vem_statusline_branch_function = 'fugitive#head'
```
Vem Statusline will then display current Git branch every time you edit
a file withing a repository.

*Note*: If you don't see the name of the branch and you have configured the
plugin to do so, make sure that the value of the `g:vem_statusline_parts`
variable contains a letter `b` (which is the value to display the branch name
as explained in the next section).

Configuration
-------------

You can set these variables to configure Vem Statusline in your `.vimrc` file:

`g:vem_statusline_parts`: string (default: 'mbfienpP')

    The value of this option specifies which elements of the statusline
    have to be displayed. There's a letter per element and the plugin
    will only diplay those elements whose letter is in this variable.

    For instance, if `g:vem_statusline_parts = 'mf'` then only the
    current mode and the current filename will be displayed.

    The meaning of the letters is:

    m: current mode
    b: current branch name
    f: current filename
    i: indent type and size (tabs, spaces, tabs+spaces)
    e: file encoding
    n: newline type (Unix: LF, Windows: CRLF, Mac pre-OSX: CR)
    p: position in the file (line:column)
    P: progress in percentage through the file

`g:vem_statusline_branch_function`: string (default: '')

    Name of the function to execute to retrieve the current Git branch
    name. Use:

    `gitbranch#name` for [vim-gitbranch](https://github.com/itchyny/vim-gitbranch)
    `fugitive#head` for [fugitive.vim](https://github.com/tpope/vim-fugitive)

    Actually, you can use here the name of any Vim script function that returns
    a string. So if you have such a function for a source control system other
    than Git you can perfectly use it here.

`g:vem_statusline_filename_format`: string (default: 't')

    Format in which the current filename should be displayed:

    t: only the filename without its path (tail)
    p: full path (path)

`g:vem_statusline_mode_separator`: string (default: ' ~ ')

    Symbol separator between the current mode and the brach/filename
    elements. Not shown if the branch and filename are not displayed.

`g:vem_statusline_branch_separator`: string (default: ':')

    Symbol separator between the current branch and the filename.
    Not shown if the filename is not displayed.

`g:vem_statusline_right_separator`: string (default: '|')

    Symbol separator between the indent, encoding and newline elements.
