---
layout: with-nav
title: (La)TeX styleguide
---

{::options toc_levels="1..3" syntax_highlighter_opts="{default_lang: 'TeX'\}" /}

These are my personal style guidelines for writing `.tex` files.

* hi
{:toc}


{% include to-top.html %}

Document structure
------------------

A `.tex` file is divided into two parts: the **preamble** and the **body**.
They are formatted as follows:

```TeX
% <preamble>

\begin{document}

% <body>

\end{document}
```

Note that the body is not indented (see [Nesting and environments](#nesting--environments)).

### Preamble

The preamble is divided into three parts: loading the document class, loading packages, and running commands. The preamble should look like this:

```TeX
% Loading the document class
\documentclass{...}

% Loading packages
\usepackage{...}
...

% Run commands
\MyCommand{...}
...
```

While `\documentclass` and `\usepackage` are commands, we distinguish them due to their special role. Exceptions apply to the above partition:
* Sometimes, it is necessary to run commands before loading packages.
* Loading subpackages (e.g. for `tikzpicture`) or setting up options for a package via a command should be done right after loading the package.
* I'm not sure how to feel about loading a package to run a single command, for example, loading `enumitem` to set enumerate settings immediately after. Maybe it is better to group the commands with the package.

Packages and commands should be loaded and run in a reasonable order. Try to maintain order by grouping related commands together. My suggestions:
* Common groupings for packages are (suggested order): layout, fonts, math, referencing.
* Common groupings for commands are (suggested order): layout, theorems, custom macros, metadata (title, author, etc.).

Note that packages may need to be loaded in specific orders in order to work properly.

### Body

The body consists of sections, paragraphs, and environments (text and math). The content can be regular text, math content, labels, or commands.

Commands declaring new sections, paragraphs, and environments that create paragraphs are preceded and followed by a single blank line:
```TeX
... <content>

\section{<title>}

Lorem ipsum dolor sit amet, consectetur adipiscing elit.

\begin{theorem}
  ...
\end{theorem}

<more content> ...
```

See [Nesting and environments](#nesting--environments) for details about formatting environments.

{% include to-top.html %}

Commands
--------

### Naming conventions

I don't have any suggestions for naming commands. Typically they are `UpperCamelCase` or `lowerCamelCase`.

### Common macros

When defining math operators, use `\DeclareMathOperator` (from the library `amsopn`, which is loaded automatically by `amsmath`).

### Usage

Commands that are used outside of the regular flow of text should preferably be on their own line:
* Commands that **do not** directly produce visible elements should be given their own line.
* Commands that **do** produce visible elements should preferably be on their own line, but sometimes it is more meaningful to have several commands on the same line.

By default, use curly braces around command arguments. Exceptions:
* Any command with nonstandard syntax (e.g. `^` and `_`, when the braces are not needed). When the argument is a command with arguments, use braces (it probably would not compile, anyways).
* 0-argument commands are only followed by `{}` if needed (e.g. to not take the next token as argument).
* `\left` and `\right`, as the curly braces can be confusing when the argument is a delimiter itself.

```TeX
$2^n$, but $2^{\mathbb{N}}$.

You can write \LaTeX. But using \LaTeX{} in the middle of a sentence requires curly braces.

\[
  \left\{
    \sum_{i = 1}^n x_i
  \right\}
\]
```

{% include to-top.html %}

Text & general formatting
-------------------------

### Whitespace

* I recommend using indentations, and this style guide will refer to indentation. However, you may also follow this style guide while ignoring any rules about indentation.
* Tabs should be 2 spaces, except on Overleaf, where they should be 4 spaces because the indenation guidelines are fixed at 4 spaces. Do not use tabs to indent.
* Remove trailing whitespace. Remove redundant spaces unless they are there for a good reason (such as formatting content in a table).

### Line wrapping

There are two options for line wrapping. Either you respect an 80 character limit, or you do not. In the latter case, do not insert newlines in the middle of a sentence (unless the sentence is broken up by, say, an equation). You may go to a new line at the end of a sentence, even if you are not starting a new paragraph, but this is not required.

### Miscellaneous

Use ``` ``...''``` for quotes, never `"..."`.

{% include to-top.html %}

Math
----

Air out math expressions, but keep the code similar to the expected output. General rules:
* Ensure a single space around binary relations (e.g. arithmetic operations), after commas, between macros.
* Ensure a signle space around a math symbol with its superscripts, subscripts, and functional arguments.
* No space between an operator (e.g. a function) and the following open delimiter (parenthesis, curly brace, etc.).
* No space between negative sign and following expression.
* Prefer no space between brackets and their inside content. This can be ignored for more complex content, see [Nesting and environments](#nesting--environments) for more guidelines.
* For displayed math, never use `$$`: use `\[ ... \]` instead.

Regarding `$ ... $` versus `\( ... \)` for inline math:
* In general, stick to one. The most proper would be the parentheses, but there's a lot of bias towards the dollar signs, from myself included.
* When using the parentheses inline, separate the inner content from the delimiters by a space on both sides.
* If you chose to use `$`, you should still use parentheses for complex inline math expressions that require their own nesting. In this case, format the math as you would displayed math.

```TeX
Some example mathematics: inline $e^{i \pi} + 1 = 0$, and display
\[
  \operatorname{li}(x) \coloneq \int_0^x \frac{\textnormal{d} t}{\ln t}
  \qquad \textnormal{and} \qquad
  \Pi_0(x) \coloneqq \frac{1}{2} \left( \sum_{p, n : p^n < x} \frac{1}{n} + \sum_{p, n : p^n \leq x} \frac{1}{n} \right).
\]
```

### Line breaks

Sometimes, mathematical expressions are too long to fit legibly on a single line: we then use line breaks. Line breaks in math content should prioritize symbols in the same order as syntax precedence: for example, break at the equals sign (`=`) before breaking at a plus sign (`+`) in one of the expressions.
This also applies to grid symbols: break at a line break (`\\`) before breaking at an ampersand (`&`) (see [Arrays & grids](#arrays--grids)).
The order of priority could be as follows:

> `\\` > `&` > `=` > `␣` (multiplication) > `+` and so on.

Line breaks come before the breaking symbol, except for line break commands (e.g. `\\`, `\cr`), where the line break comes after.
Essentially, having the breaking symbol at the beginning of the line tells the reader that the line is not over.

Symbols at line breaks should not be placed on their own line. An is for binary relations surrounded by whitespace commands: this can be on its own line:

```TeX
\[
  ...
  \quad \text{and} \quad
  ...
\]
```

Another way to break a line is to move content in brackets into an indented block.

### Equivalent macros

Sometimes there are several ways to write the same thing that are either identical or very similar. Some rules:
* Use `\colon` instead of `:` when notating functions, but not when using a colon as a binary relation.
* Use `\coloneq` instead of `\coloneqq`.
* Use `\mid` instead of `|` when defining a set with conditions (e.g. `\{ x \in X \mid x > 0 \}`).

{% include to-top.html %}

Nesting & environments
----------------------

Most complex TeX code comes in the form of nested blocks: this includes environments, but also the arguments of commands and math expressions inside brackets.

### Code blocks & block delimiters

A **code block** consists of an opening block delimiter, followed by inner content, followed by a closing block delimiter. (**Block**) **delimiters** include:
* the `\begin{...}` and `\end{...}` commands for environments,
* the curly braces around a command argument,
* brackets around a math expression.

Importantly, code blocks can and will be **nested**. In general, the inner content of a code block is indented once relative to the delimiters.

The formatting of delimiters is separated into the *inner* and *outer* formatting. Delimiters should be symmetrical in their inner formatting. Examples:
* If the opening delimiter is followed by a line break, then the closing delimiter should be preceded by a line break.
* If you put a space between one delimiter and the inner content, then there should be a space between the other delimiter and the content.

If the code block is written on a single line, include a space between the delimiters and the inner content. Exception: brackets, when the inner content is simple (see [Math](#math)).

```TeX
\begin{equation}
  \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}
\end{equation}
```

Delimiters on their own line should have the same indentation level. Delimiters do not need to be symmetrical in their outer formatting.

When inner content is on its own line, it should be indented once more than the delimiters. As an exception, consecutively nested delimiters are allowed to be on the same indentation level. They can also share the same line (separated by a space) if that is more meaningful.

```TeX
\[
  f \colon \left\{ \begin{array}{ccc}
    X & \to & Y \\
    x & \mapsto & f(x).
  \end{array} \right.
\]
```

### Local commands

Sometimes, we need to call some commands inside of an environment. The typical example of this is giving a label. These commands are placed after the opening delimiter, at the same indentation level. These commands most likely do not directly produce visual content, and should be each given their own line.

```TeX
\begin{equation}
\label{E:equation-1}
  A x = b
\end{equation}
```

See [Labels](#labels) for more guidelines about label names.

### Lists

Lists and enumerations have some special rules.

* Each item of the list gets its own line.
* If the item content is on the same line as the `\item` command, the whole line is indented (as for all inner content).
* Optionally (such as when the item content or the `\item` command is long), the `\item` command is on its own line, at the same indentatation level as the list environment. The item content is on a new line, with an extra indentation.

```TeX
A smaller list:
\begin{itemize}
  \item Item 1
  \item Item 2
\end{itemize}
and larger list:
\begin{itemize}
\item[\bullet] \label{I:1}
  Use this formatting when the item is quite long, say over 80 characters, or when it starts wrapping in your editor.
\item
  Be consistent in each list!
\end{itemize}
```

### Arrays & tables

Arrays and tables are a special kind of code block that encode two-dimensional grid layouts in one-dimensional code. This complexity requires some special attention. The inner content of these code blocks is typically broken up into several lines. In its simplest form, each line corresponds to an outputted row. See [Line breaks](#line-breaks) for details about how to format multiple-line code blocks.

While in general, symbols at line breaks should not be on their own line, we allow an exception for blocks where the items of each row are already on their own lines, in which case the line break can be on its own line, but with one less indentation:

```TeX
\[
  \begin{array}
    ...
    & ...
    & ...
  \\
    ...
    & ...
    & ...
  \end{array}
\]
```

{% include to-top.html %}

Labels
------

Labels should be of the form `<envir>:<name>`, where
* `<envir>` is an abbreviation of the type of environment that the label is attached to. My suggestions are

  | Environment | Abbreviation |
  |:-:|:-:|
  | section, subsection, etc. | `S`, `SS`, ... |
  | theorem, proposition, corollary, lemma | `T`, `P`, `C`, `L` |
  | definition, remark, example | `R`, `D`, `Ex` |
  | equation, or any displayed math | `E` |
  | figure, table, algorithm | `F`, `T` or `Tab`, `A` |
* `<name>` briefly describes the labeled content. Use words, abbreviated or not. I suggest using `kebab-case` when using several words, although you may choose another convention: just be consistent!

Comments
--------

Comments are normally introduced by a single `%`. This can be ignored when separating parts of the code with a long comment (e.g. a line of 80 `%`'s).

* One space after `%`.
* End-of-line comments are preceeded by two spaces, unless they also serve to remove the trailing whitespace that the TeX compiler would insert, in which case they are preceeded by no space.