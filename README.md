[![MELPA](https://melpa.org/packages/key-assist-badge.svg)](https://melpa.org/#/key-assist)

# key-assist.el - keybinding cheatsheet / launcher

## Commentary:

### For Emacs *users*:

This package provides an interactive command to easily produce
a keybinding cheat-sheet "on-the-fly", and then to launch any
command on the cheat-sheet list. At its simplest, it gives the
user a list of keybindings for commands specific to the current
buffer's major-mode, but it's trivially simple to ask it to
build an alternative (see below, section 'Interactive operation').

:bulb: Think of the default-action as an improved `C-h m` summary.

:checkered_flag: Enter a command substring to see all related bindings.

Use this package to: learn keybindings; learn what commands are
available specifically for the current buffer; run a command
from a descriptive list; and afterwards return to work quickly.

### For Emacs *programmers*:

This package provides a simple, flexible way to produce custom
keybinding cheat-sheets and command launchers for sets of
commands, with each command being described, along with its direct
keybinding for direct use without the launcher (see below).

### For everyone:

If you've ever used packages such as `ivy` or `magit`, you've
probably benefited from each's custom combination keybinding
cheatsheet and launcher: `hydra` in the case of `ivy`, and
`transient` for `magit`. The current package `key-assist` offers
a generic and very simple alternative requiring only the
`completing-read` function commonly used in core vanilla Emacs.
`key-assist` is trivial to implement "on-the-fly" interactively
for any buffer, and programmatically much simpler to customize
that either `hydra` or `transient`. And it only requires the
Emacs core function `completing-read`.

## What it look likes

How `key-assist' output displays will largely depend on what you
use for your minibuffer completions. Here's an example of the
default output for an \*Occur\* buffer.

```
Select an item on the list to launch it:
  e     Major mode for editing *Occur* buffers.
> o     occur-mode-goto-occurrence-other-window (not documented)
  r     Rename the current *Occur* buffer to *Occur: original-buffer-name*.
  C-o   occur-mode-display-occurrence (not documented)
  M-n   Move to the Nth (default 1) next match in an Occur mode buffer.
  M-p   Move to the Nth (default 1) previous match in an Occur mode buffer.
  RET   Go to the occurrence on the current line.
  M-s o Drop-in replacement for `occur', but when called with a prefix
```

## Dependencies:

`cl-lib`: For `cl-member`,`cl-position`

## Installation:

1) Evaluate or load this file.

## Interactive operation:

Run M-x `key-assist` from the buffer of interest. Specify a
selection (or don't), press <TAB> to view the presentation, and
then either exit with your new-found knowledge of the command
keybindings, or use standard Emacs tab completion to select an
option, and press <RETURN> to perform the action.

If you choose not to respond to the initial prompt, a list of
keybindings and command descriptions will be generated based upon
the first word of the buffer's major mode. For, example, in a
`w3m` buffer, the list will be of all interactive functions
beginning `w3m-`. This works out to be great as a default, but
isn't always useful. For example, in an `emacs-lisp-mode` buffer
or a `lisp-interaction-mode`, what would you expect it to
usefully produce? At the other extreme might be a case of a
buffer with too many obscure keybindings of little use.

You can also respond to the prompt with your own regexp of
any set of commands to show, or with the name of a keymap of
your choice. For the purposes of `key-assist`, a regexp can be
just a substring, without REQUIRING any leading or trailing globs.

In all cases, note that the package can only present keybindings
currently active in the current buffer, so if a sub-package
hasn't been loaded yet, that package's keybindings would not be
presented. Also note that the commands are presented sorted by
keybinding length, alphabetically.

## Programmating example:

Here's a most simple example that presents all of the keybindings
for 'my-mode:

```emacs-lisp
(defun my-mode-keybinding-cheatsheet-launcher ()
  (interactive)
  (when (eq major-mode my-mode)
    (key-assist)))
(define-key my-mode-map "?"
            'my-mode-keybinding-cheatsheet-launcher)
```

See the docstrings for functions `key-assist` and
`key-assist--get-cmds` for the description of ARGS that can be
used to customize the output.

## Configuration:

Two variables are available to exclude items from the
presentation list: `key-assist-exclude-cmds` and
`key-assist-exclude-regexps`. See there for further information.

## Compatability

Tested with Emacs 26.1 and emacs-snapshot 28(~2020-09-16), both
in debian.

## Colophon

* Copyright © 2020, Boruch Baum <boruch_baum@gmx.com>

* License: GPLv3+

* Author/Maintainer: Boruch Baum <boruch_baum@gmx.com>

* Homepage: https://github.com/Boruch-Baum/emacs-key-assist

* Keywords: abbrev convenience docs help

* Package: key-assist

* Package-Version: 1.0

* Package-Requires:
  * emacs 24.3 for: `lexical-binding`, `user-error`, `cl-lib`
