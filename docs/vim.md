[back to home](../README.md)

# VIM NOTE

Collection of Vim commands with `spf13` plugin.

**Note** Some commands may need `spf13` installed.

Keys | description
----- | -----
`i` | insert before the cursor
`I` | insert at start of line
`a` | insert after the cursor
`A` | insert at start of line
`o` | insert line below
`O` | insert line above
`u` | undo
`C-r` | redo
`v` | visual mode
`C-v` | visual block
`V` | visual line
`enter` | enter visual line with block selected
`y` | yank
`esc` / `C-c` | back to normal mode
`h` | move cursor to the left
`j` | move cursor down
`k` | move cursor up
`l` | move cursor to the left
`d` / `x`| delete
`p` | paste
`r` | replace char at cursor
`s` | replace and continue insert
`/` | search forward
`?` | search backward

Windows | description
----- | -----
`:vsplit` / `C-w` `v` | split window vertically
`:split` / `C-w` `s` | split window horizontally
`C-w` `C-w` | cycle through windows
`:q` | quit window
`:b` `number` | open buffer `number`
`:bn` | move to next buffer
`:bp` | move to previous buffer
`:bd` | delete current buffer
`:bw` | wipe out buffer (clean store)
<code>:bp&#124;bd #</code> / <code>:bn&#124;bd #</code> | delete buffer without closing window

Combos | description
----- | -----
`ggVG` | select all
`ggVGy` | yank all
`ggguG` | make all text lowercase

Commands | description
----- | -----
`:noh` | clear highlighted
`:%y+` | yank all
`:e filename` | openfile
`,` `e` | open **NERDTree**


> - `⌃` - `&#x2303;` - Control Key symbol
- `⌘` - `&#x2318;` – Command Key symbol
- `⌥` – `&#x2325;` – Option Key symbol
- `⇧` – `&#x21E7;` – Shift Key symbol
