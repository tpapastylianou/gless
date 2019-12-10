# gless
A less pager with additional syntax highlighting

----

`gless` is a simple bash script which can be used wherever one would use the `less` pager, but also providing additional 
syntax highlighting as provided by the python-pygments package (and the `pygmentize` command in particular).

Depends on the python pygments package which can be installed via your distribution or via pip.

Effectively it is a simple bash script which passes the input to pygmentize before passing it to less, with appropriate 
parameters in each case.

Simply copy the gless script in /usr/local/bin and make it executable.

Alternatively, you could alias `less` in your `.bashrc` to call `gless` instead.

Note that `gless` also works with pipe syntax (since pygmentize can accept pipes).
