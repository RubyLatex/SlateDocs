---
title: API Reference

toc_footers:
  - <a href='https://github.com/RubyLatex'>Hosted on Github</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

search: true
---

# Introduction

This is the official RbTeX documentation. The documentation here includes the useage of RbTeX, GMath,
and other information regarding RubyLatex.  

# Installing
RubyLatex was build on OS X 10.11 (El Capitan), and as such is configured for that environment. For the
time being, the ``rblatex`` processor requires that you have Ruby installed at ``usr/local/bin/ruby``.
If you need to change this, simply change the shebang in the first line of the ``rblatex`` program.

# LaTeX
On the LaTeX side, you simply need to include the rubylatex package. The package includes several
commands discussed in this section.
> You can include the rubylatex package like this

```tex
\documentclass{myclass}
\usepackage{rubylatex}

\begin{document}
% content here
\end{document}
```

## RbTeX
``\RbTeX`` is a fancy command that displays the RbTeX logo. It must be used in math mode.

```tex
\documentclass{myclass}
\usepackage{rubylatex}

\begin{document}
Hi! I'm using the $\RbTeX$ package.
\end{document}
```

## rbtex
``rbtex`` is the default environemnt for injecting Ruby code. Anything inside the ``rbtex`` environemnt
needs the be ruby code. For example, using ``%`` to comment items inside the ``rbtex`` will not work;
you must use a ``#`` instead.

```tex
\documentclass{myclass}
\usepackage{rubylatex}

\begin{document}

% out here, use LaTeX supported commands
\begin{rbtex}
# in here, use Ruby supported commands
puts 'hello, world'
\end{rbtex}
\end{document}
```

## frbtex
<aside class='warning'>THIS IS NOT YET IMPLEMENTED</aside>
``frbtex`` provides an interface with which to include an entire external file. The file will be copied
verbatim, so there is no need to ``require 'rbtex'`` in the supplied script.

```tex
\documentclass{myclass}
\usepackage{rubylatex}

\begin{document}
\frbtex{myfile.rb}

\begin{rbtex}
myFunctionDefinedInMyFileDotRb
\end{rbtex}
\end{document}
```

# Tex
The ``Tex`` module contains tools to generate LaTeX output from ruby.

## Tex.print(arg0)
This command prints `arg0` to the LaTeX document.

### Arguments
* `arg0`: The string to be printed out

> Print a string to the TeX document

```tex
\documentclass{myclass}
\usepackage{rubylatex}

\begin{document}

\begin{rbtex}

Tex.print("Hello, world from Ruby!")

\end{rbtex}
\end{document}
```

## Tex.cmath(arg0)
Wraps `arg0` in a centered equation environemnt
### Arguments
* `arg0`: The string to be wrapped by `\[` and `\]`

### Returns
* A string representing the term `\[arg0\]`

> Centering an equation is easy

```tex
\documentclass{myclass}
\usepackage{rubylatex}

\begin{document}

\begin{rbtex}

myfx = "f(x)"
Tex.print Tex.cmath(myfx)

\end{rbtex}
\end{document}
```

## Tex.imath(arg0)
Wraps `arg0` in an inline math mode environemnt

### Arguments
* `arg0`: The string to be wrapped by `$` and `$`

### Returns
* A string representing the term `$arg0$`

```tex
\documentclass{myclass}
\usepackage{rubylatex}

\begin{document}

\begin{rbtex}

myfx = "f(x) = x^{2}"
Tex.print "#{Tex.imath(myfx)} is a nice equation."

\end{rbtex}
\end{document}
```

## Tex.center(arg0)
Wraps `arg0` in an center environment.

### Arguments
* `arg0`: The string to be wrapped by `\begin{center}` and `\end{center}`

### Returns
* A string representing the term `\begin{center}arg0\end{center}`

```tex
\documentclass{myclass}
\usepackage{rubylatex}

\begin{document}

\begin{rbtex}

Tex.print Tex.center("This is important!")

\end{rbtex}
\end{document}
```

## Table
The `Tex` module provides a simple way to create a generic table.

### Minimal Working Example
This example provides a simple use case for generating a table. The `rubylatex` package by default
formats this to be a `tabularx` environment with all columns set to `|X|`.

```tex
\documentclass{myclass}
\usepackage{rubylatex}

\begin{document}

\begin{rbtex}

array = [
    ["Header 01","Header 02","Header 03"],
    ["Content 01","Content 01","Content 01"],
    ["Content 02","Content 02","Content 02"]
]

myTable = Tex::Table.new array
content = myTable.create
Tex.print(content)

\end{rbtex}

\end{document}
```
