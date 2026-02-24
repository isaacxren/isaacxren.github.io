---
layout: with-nav
title: (La)TeX style guide
---

{::options toc_levels="1..3" syntax_highlighter_opts="{default_lang: 'TeX'\}" /}

These are my personal style guidelines for writing `.tex` files. These notes are built on my personal experience. You can also find elements of style guidelines in Knuth's ***The TeXbook***, in particular {% include hidden-message.html text="Chapters 16 through 19" message="16. Typing Math Formulas&#10;17. More about Math&#10;18. Fine Points of Mathematics Typing&#10;19. Displayed Equations"%}.

* table of contents here
{:toc}

[~ ˆ ~](# "Top of the page"){:.to-top}

Document structure
------------------

A `.tex` file is divided into two parts: the **preamble** and the **body**.
The file is formatted as follows:

```TeX
<preamble>

\begin{document}

<body>

\end{document}
```

Note that the body is not indented (see [Nesting & environments](#nesting--environments)).

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

See [Nesting & environments](#nesting--environments) for details about formatting environments.

[~ ˆ ~](# "Top of the page"){:.to-top}

Commands
--------

### Naming conventions

I don't have any suggestions for naming commands. Typically they are `UpperCamelCase` or `lowerCamelCase` in packages, but I tend to keep macros `lowercase`.

### Common macros

When defining math operators, use `\DeclareMathOperator` (from the library `amsopn`, which is loaded automatically by `amsmath`).

### Usage

Commands that are used outside of the regular flow of text should preferably be on their own line, but sometimes it is more meaningful to have several commands on the same line.

By default, use curly braces around command arguments. Exceptions:
* Any command with nonstandard syntax (e.g. `^` and `_`, when the braces are not needed). When the argument is a command with arguments, use braces (it probably would not compile, anyways).
* 0-argument commands are only followed by `{}` if needed (e.g. to not take the next token as argument).
* `\left` and `\right`, as the curly braces can be confusing when the argument is a delimiter itself.

*Example:*
```TeX
$2^n$, but $2^{\mathbb{N}}$.

You can write \LaTeX. But using \LaTeX{} in the middle of a sentence requires curly braces.

\[
  \left\{
    \sum_{i = 1}^n x_i
  \right\}
\]
```

### Long and multiple arguments

If a command has a long argument, the long argument should be put on its own indented block: see [Nesting & environments](#nesting--environments) for details about formatting code blocks.

If a command has multiple arguments, then each argument is enclosed by curly braces and there is no space between consecutive arguments. Use `%` to remove unwanted whitespace (see [Whitespace](#whitespace)).

*Example:*
```TeX
\title[%
  short title that is still somewhat long%
]{%- raw %}{%{%endraw %}
  long title that is even longer than the short title, so long that even the
  short title is somewhat long%
}
```

If an argument has a key-value syntax, then they should be formatted like function arguments in a programming language. Pick a programming language style guide and stick to it: see, for instance, the [Google C++ style guide](https://google.github.io/styleguide/cppguide.html#Function_Declarations_and_Definitions). I suggest writing key-value pairs as `<key>=<value>`, i.e., with no space around the equals sign. This is [PEP 8's recommendation](https://peps.python.org/pep-0008/#other-recommendations) for keyword arguments in Python.

[~ ˆ ~](# "Top of the page"){:.to-top}

Text & general formatting
-------------------------

### Whitespace

* I recommend using indentations, and this style guide will refer to indentation. However, you may also follow this style guide while ignoring all rules about indentation.
* Tabs should be 2 spaces, except on Overleaf, where they should be 4 spaces because the indentation guidelines are fixed at 4 spaces. Do not use tabs to indent.
* Remove trailing whitespace. Remove redundant spaces unless they are there for a good reason (such as formatting content in a table).
* Line breaks sometimes create whitespace. Use `%` to remove unwanted whitespace.

### Line wrapping

There are two options for line wrapping. Either you respect an 79 character limit, or you do not. In the latter case, do not insert newlines in the middle of a sentence (unless the sentence is broken up by, say, an equation). You may go to a new line at the end of a sentence, even if you are not starting a new paragraph, but this is not required.

### Punctuation

* Use ``` ``...''``` for quotes, never `"..."`.
* Trailing punctuation should be kept outside of inline math: write `Let $x = 0$.`, not `Let $x = 0.$`. **Do** use punctuation at the end of displayed math, when appropriate.

[~ ˆ ~](# "Top of the page"){:.to-top}

Math
----

Air out math expressions, but keep the code similar to the expected output. General rules:
* Ensure a single space around binary relations (e.g. arithmetic operations), after commas, between macros.
* Ensure a single space around a math symbol with its superscripts, subscripts, and functional arguments.
* No space between an operator (e.g. a function) and the following open delimiter (parenthesis, curly brace, etc.).
* No space between negative sign and following expression.
* Prefer no space between brackets and their inside content. This can be ignored for more complex content, see [Nesting & environments](#nesting--environments) for more guidelines.
* For displayed math, never use `$$`: use `\[ ... \]` instead.

Regarding `$ ... $` versus `\( ... \)` for inline math:
* In general, stick to one. The most proper would be the parentheses, but there's a lot of bias towards the dollar signs, from myself included.
* When using the parentheses inline, separate the inner content from the delimiters by a space on both sides.
* If you chose to use `$`, you should still use parentheses for complex inline math expressions that require their own nesting. In this case, format the math as you would displayed math.

*Example:*
```TeX
Write math expressions, both inline $e^{i \pi} + 1 = 0$, and display
\[
  \operatorname{li}(x) \coloneq \int_0^x \frac{\textnormal{d} t}{\ln t}
  \qquad \textnormal{and} \qquad
  \Pi_0(x) \coloneqq \frac{1}{2} \left(
    \sum_{p, n : p^n < x} \frac{1}{n} + \sum_{p, n : p^n \leq x} \frac{1}{n}
  \right).
\]
```

### Line breaks

Sometimes, mathematical expressions are too long to fit legibly on a single line: we then use line breaks. Line breaks in math content should prioritize symbols in the same order as syntax precedence: for example, break at the equals sign (`=`) before breaking at a plus sign (`+`) in one of the expressions.
This also applies to grid symbols: break at a line break command (`\\`) before breaking at an ampersand (`&`) (see [Arrays & grids](#arrays--grids)).
The order of priority could be as follows:

> `\\` > `&` > `=` > `\cdot` (multiplication) > `+` and so on.

Line breaks come before the breaking symbol, except for line break commands (e.g. `\\`, `\cr`), where the line break comes after.
Essentially, having the breaking symbol at the beginning of the line tells the reader that the line is not over. When starting a new line, formatting commands like `\\`, `\cr`, and `&` do not increase the indentation, while visible elements like `\cdot`, `+`, and so on, do.

*Example:*

```TeX
\begin{align*}
  \sum_{k = 1}^10 k & = \frac{1}{2} (1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9 + 10
    + 10 + 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1) \\
  & = \frac{1}{2} (11 + 11 + 11 + 11 + 11 + 11 + 11 + 11 + 11 + 11) \\
  & = \frac{1}{2} 10 \cdot 11 \\
  & = 55.
\end{align*}
```

Symbols at line breaks should not be placed on their own line. An exception is for binary relations surrounded by whitespace commands. These can be on their own line:

```TeX
\[
  ...
  \quad \text{and} \quad
  ...
\]
```

Another way to break a line is to move content in brackets into an indented block: see [Nesting & environments](#nesting--environments).

### Equivalent macros

Sometimes there are several ways to write the same thing that are either identical or very similar. Some rules:
* Use `\colon` instead of `:` when notating functions, but not when using a colon as a binary relation.
* Use `\coloneq` instead of `\coloneqq`.
* Use `\mid` instead of `|` when defining a set with conditions (e.g. `\{ x \in X \mid x > 0 \}`).
* Place semantically closer super/subscripts closer to the symbol: for instance, the square of an indexed variable `x_i` should be written `x_i^2`, and not `x^2_i`. Ideally, you should be able to put parentheses around the first attachment: `(x_i)^2` makes sense, while `(x^2)_i` does not.

[~ ˆ ~](# "Top of the page"){:.to-top}

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

*Example:*
```TeX
\begin{equation}
  \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}
\end{equation}
```

Delimiters on their own line should have the same indentation level. Delimiters do not need to be symmetrical in their outer formatting.

When inner content is on its own line, it should be indented once more than the delimiters. As an exception, consecutively nested delimiters are allowed to be on the same indentation level. They can also share the same line (separated by a space) if that is more meaningful.

*Example:*
```TeX
\[
  f \colon \left\{ \begin{array}{ccc}
    X & \to & Y \\
    x & \mapsto & f(x).
  \end{array} \right.
\]
```

### Environment options

Sometimes an environment allows for extra arguments. These should be formatted as a regular command with multiple arguments (see [Long and multiple arguments](#long-and-multiple-arguments)):

```TeX
\[
  \begin{tikzpicture}[scale=1, ...]
    ...
  \end{tikzpicture}
\]
```

### Local commands

Sometimes, we need to call some commands inside of an environment. The typical example of this is giving a label. These commands are placed after the opening delimiter, at the same indentation level. These commands most likely do not directly produce visual content, and should be each given their own line.

*Example:*
```TeX
\begin{equation}
\label{E:linear-system}
  A x = b
\end{equation}
```

See [Labels](#labels) for more guidelines about label names.

An exception to the rule of placing local commands immediately after the opening delimiter is captions (and their labels) in figures. If you wish to put a caption at the bottom of a figure, and label it, then your code should look like this:

```TeX
\begin{figure}
  ...
  \caption{...}
  \label{F:label}
\end{figure}
```

### Lists

Lists and enumerations have some special rules.

* Each item of the list gets its own line.
* If the item content is on the same line as the `\item` command, the whole line is indented (as for all inner content).
* Optionally (such as when the item content or the `\item` command is long), the `\item` command is on its own line, at the same indentatation level as the list environment. The item content is on a new line, with an extra indentation.

*Example:*
```TeX
A smaller list:
\begin{itemize}
  \item Item 1
  \item Item 2
\end{itemize}
and larger list:
\begin{itemize}
\item[\bullet] \label{I:1}
  Use this formatting when the item is quite long, say over 79 characters, or
  when it starts wrapping in your editor.
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

[~ ˆ ~](# "Top of the page"){:.to-top}

Labels
------

Labels should be of the form `<envir>:<name>`, where
* `<envir>` is a code for the type of environment that the label is attached to. Two possible conventions are using initials and using abbreviations:

  | Environment | Initials | Abbreviation |
  |:-|:-|:-|
  | part | `Pt` | `part` |
  | chapter | `Ch` | `chap` |
  | section | `S` | `sec` |
  | subsection | `SS` | `subsec` |
  | subsubsection | `SSS` | `subsubsec` |
  | theorem | `T` | `thm` |
  | proposition | `P` | `prop` |
  | corollary | `C` | `cor` |
  | lemma | `L` | `lem` |
  | conjecture | `Conj` | `conj` |
  | definition | `D` | `def` |
  | remark | `R` | `rem` |
  | example | `Ex` | `ex` |
  | equation | `E` | `eq` |
  | figure | `F` | `fig` |
  | table | `T` or `Tab` | `tab` |
  | algorithm | `A` | `alg` |

  These are merely suggestions, you may pick your own convention.
* `<name>` briefly describes the labeled content. Use words, abbreviated or not. I suggest using `kebab-case` when using several words, although you may choose another convention: just be consistent!

See [Local commands](#local-commands) for an example of a labeled environment.

Comments
--------

Comments are normally introduced by a single `%`. This can be ignored when separating parts of the code with a long comment (e.g. a line of 80 `%`'s).

* One space after `%`.
* End-of-line comments are preceeded by two spaces, unless they also serve to remove the trailing whitespace that the TeX compiler would insert, in which case they are preceeded by no space.