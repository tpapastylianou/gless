# gless
A less pager with additional syntax highlighting

----
## About:

`gless` is a simple bash script which can be used wherever one would use the `less` pager, but also providing additional
syntax highlighting as provided by the python-pygments package (and the `pygmentize` shell command in particular).

Depends on the python pygments package which can be installed via your distribution or via pip.

Effectively it is a simple bash script which passes the input to pygmentize before passing it to less, with appropriate
parameters in each case.

----

## Installation:

Simply copy the gless script in your `/usr/local/bin` directory and make it executable.

----

## Usage:

    gless [valid pygmentize options] <filename>

Alternatively, `gless` also works with pipe syntax:

    cat <filename> | gless [valid pygmentize options]


### Examples:

Basic use:

    gless mymodule.py


Basic pipe use:

    cat mymodule.py | gless


Use with additional options, specifying an explicit lexer (python) and style (fruity):

    gless -lpython -O style=fruity my_executable_python_script


The 'native' colour-scheme is particularly useful for `svn diff` outputs (unlike normal `diff`, `svn diff` does not provide a `--color` option):

    svn diff | gless -O style=native

----

## Miscellaneous Notes:

- Any options passed to `gless` are effectively passed on to `pygmentize`; however these need to be defined before the input filename.

- In pipe mode, the pipe is effectively intercepted and handled by pygmentize under the hood, which means it is possible to pass options to pygmentize in pipe mode as well.

- The `-g` option is passed to pygmentize by default; this tells pygmentize to try and guess the content of the file. If you want to specify a lexer explicitly, passing a subsequent `-l` option overrides this.

- Many commands (e.g. `ls`, `grep`, `ack`, `diff`, etc) have a `--color` option, outputting their own colour-scheme of choice. It typically makes more sense to use this with `less -R` directly, rather than attempt to re-pygmentize via gless. E.g.

        diff --color=always file1 file2 | less -R

    would most likely be preferable to

        diff file1 file2 | gless

- If you're not happy with the default pygments style, you can edit the script directly to add a style parameter to the pygmentize part.

    E.g. instead of

        pygmentize -g "$@" | less -R

    to make 'fruity' the default style, change this to

        pygmentize -g -O style=fruity "$@" | less -R

    A list of available pygments styles can be found in your pygments installation directory (e.g. `/usr/local/lib/python3.6/dist-packages/pygments/styles` )

- If one also wants to pass options to the underlying 'less' pager, rather than just to pygmentize, the way to do this is via the LESS bash variable.  
  E.g. to call 'less' with the '-N' (i.e. show line numbers) switch enabled, one can call gless like so:

    LESS='-N' gless [valid pygmentize options] <filename>


