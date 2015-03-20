# dirtree.el -- Directory tree views for Emacs

Original here:
* [Google Code (deprecated)](http://code.google.com/p/ywb-codes/source/browse/trunk/emacs/site-lisp/contrib/dirtree.el).
* [EmacsWiki](http://www.emacswiki.org/emacs/dirtree.el)

## Installation

2. Download `tree-mode.el`, `windata.el`, and `dirtree.el` to `DIRECTORY`.
3. Add to your Emacs init file (`.emacs`, `init.el`, etc.):

       `(add-to-list 'load-path "DIRECTORY"` 
       `(require 'dirtree)`

4. Optionally, see [Additional Customization][customize] below.

## Requires

* [tree-mode](http://www.emacswiki.org/emacs/tree-mode.el)
* [windata](http://www.emacswiki.org/emacs/windata.el)

## Usage

* `M-x dirtree RET`
* `M-x dirtree-in-buffer RET` -- Opens dirtree in a buffer in the current
   window.

## Default keybindings

### From `tree-mode.el`
	
        <space>    scroll-up
        <ctrl> ?   scroll-down
        D          tree-mode-delete-tree
        p          tree-mode-previous-node
        n          tree-mode-next-node
        j          tree-mode-next-sib
        k          tree-mode-previous-sib
        u          tree-mode-goto-parent
        r          tree-mode-goto-root
        g          tree-mode-refresh
        E          tree-mode-expand-level
        e          tree-mode-toggle-expand
        s          tree-mode-sort-by-tag
        /          tree-mode-keep-match
        !          tree-mode-collapse-other-except

### From `dirtree.el`

        o          dirtree-open-file
        <ctrl> o   dirtree-open-file-other-window
	    q          close buffer and kill window

The `<return>` key is also bound to act as a "smart click."  If the
cursor is on a folder icon, `<return>` toggles or untoggles the display
of the directory contents (`tree-mode-toggle-expand`).  If the cursor
is on a file icon, `<return>` opens the file in another window
(`dirtree-open-file-other-window`).

You can also use the cursor keys or mouse for navigation.


[customize]: #customize

## Additional Customization

### Eproject Integration

Opens dirtree with the root pointing at the current eproject root.

    (defun ep-dirtree ()
      (interactive)
      (dirtree-in-buffer eproject-root t))

### Cursor Key / Return Navigation

The following code makes navigation with the cursor keys and
`<return>` as described above under **Default Keybindings** work
better, since the cursor will always stay on the folder/file icon:

	(add-hook 'dirtree-mode-hook
			  (lambda ()
				(add-hook 'post-command-hook
						  (lambda ()
							(ignore-errors
							  (beginning-of-line)
							  (while (not (widget-at)) (forward-char 1))))
						  "at-end" "local-to-buffer")))

## License

Copyright (C) 2010 Free Software Foundation, Inc.

Author: Ye Wenbin <wenbinye@gmail.com>

Maintainer: Ye Wenbin <wenbinye@gmail.com>

Created: 09 Jan 2010

Version: 0.01

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2, or (at your option)
any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Suite 500, Boston, MA 02110.

