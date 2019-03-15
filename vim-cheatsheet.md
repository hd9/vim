# Vim Cheat Sheet  

## Navigating  
`h j k l` - move cursor left / downn / up / right  
`M L` - move to middle/bottom of screen  
`w W` - jump forwards to the start of a word (ponctuation)  
`e E` - jump forwards to the end of a word (ponctuation)  
`b` - jump backwards to the start of a word  
`B` - jump backwards to the start of a word (words can contain punctuation)  
`%` - move to matching character (default supported pairs: '()', '{}', '[]'. Use `:h matchpairs` for more info)  
`0` - jump to the start of the line  
`^` - jump to the first non-blank character of the line  
`$` - jump to the end of the line  
`g_` - jump to the last non-blank character of the line  
`gg` - go to the first line of the document  
`G` - go to the last line of the document  
`5G or 5gg` - go to line 5  
`fx` - jump to next occurrence of character x  
`tx` - jump to before next occurrence of character x  
`Fx` - jump to previous occurence of character x  
`Tx` - jump to after previous occurence of character x  
`;` - repeat previous f, t, F or T movement  
`,` - repeat previous f, t, F or T movement, backwards  
`'` - goes to previous position  
`}` - jump to next paragraph (or function/block, when editing code)  
`{` - jump to previous paragraph (or function/block, when editing code)  

## Marks  
`mx` - create mark x  
\`x - move to mark x  
`'x` - move to beginning of line of mark x  
`zz` - center cursor on screen  
`Ctrl + e` - move screen down one line (without moving cursor)  
`Ctrl + y` - move screen up one line (without moving cursor)  
`Ctrl + b` - move back one full screen  
`Ctrl + f` - move forward one full screen  
`Ctrl + d` - move forward 1/2 a screen  
`Ctrl + u` - move back 1/2 a screen. Tip Prefix a cursor movement command with a number to repeat it. For example, 4j moves down 4 lines.  

## Insert mode - inserting/appending text  
`i I` - insert before/after the cursor  
`a A` - append after the cursor / at the end of the line  
`o O` - append (open) a new line below/above the current line  
`ea` - insert (append) at the end of the word  

## Editing
`r` - replace a single character  
`J` - join line below to the current one with one space in between  
`gJ` - join line below to the current one without space in between  
`gwip` - reflow paragraph  
`cc` - change (replace) entire line  
`C` - change (replace) to the end of the line  
`c$` - change (replace) to the end of the line  
`ciw` - change (replace) entire word  
`cw` - change (replace) to the end of the word  
`s` - delete character and substitute text  
`S` - delete line and substitute text (same as cc)  
`xp` - transpose two letters (delete and paste)  
`u` - undo  
`Ctrl + r` - redo  
`.` - repeat last command  

## Marking text (visual mode)  
`v` - start visual char mode  
`V` - start linewise visual mode  
`o` - move to other end of marked area  
`Ctrl + v` - start visual block mode  
`O` - move to other corner of block  
`aw` - mark a word  
`ab` - a block with ()  
`aB` - a block with {}  
`ib` - inner block with ()  
`iB` - inner block with {}  
`Esc` - exit visual mode  
`>` - shift text right  
`<` - shift text left  
`d` - delete marked text  
`~` - switch case  

## Registers
`:reg` - show registers content  
`"xy` - yank into register x  
`"xp` - paste contents of register x  

Register Tips:
* Registers are being stored in ~/.viminfo, and will be loaded again on next restart of vim.  
* Register 0 contains always the value of the last yanked command.  

## Marks
`:marks` - list of marks  
`ma` - set current position for mark A  
\`a - jump to position of mark A  
y\`a - yank text to position of mark A  

## Macros  
`qa` - record macro a  
`q` - stop recording macro  
`@a` - run macro a  
`@@` - rerun last run macro  

## Cut, paste and delete  
`yy` - yank (copy) a line  
`yw` - yank (copy) the characters of the word from the cursor position to the start of the next word  
`y$` - yank (copy) to end of line  
`p` - put (paste) the clipboard after cursor  
`10p` - pastes 10 times  
`P` - put (paste) before cursor  
`dd` - delete (cut) a line  
`2dd` - delete (cut) 2 lines  
`dw` - delete (cut) the characters of the word from the cursor position to the start of the next word  
`D` - delete (cut) to the end of the line  
`d$` - delete (cut) to the end of the line  
`x` - delete (cut) character  
`"_d` - delete without copying (dump on the black hole register)  
`:8y` - yanks line 8  
`:-5y` - yanks 5th line above  
`:4,13y` - yanks lines 4 - 13  
`:%y` - yanks the entire buffer  
`:%d` - deletes the entire buffer (clean file)  
`:.,+3y` - The current line and the next 3  
`:-3,.y` - yanks the current line and the previous 3  
`:-3y` - yank 3rd line above the current  
`:4t.` - yanks line 4 and puts on line below  
`:4t.` - yanks line 4 and puts on currrent line below  

## Search and replace  
`/pattern` - search for pattern  
`?pattern` - search backward for pattern  
`\vpattern` - 'magic' pattern: non-alphanumeric characters are interpreted as special regex symbols (no escaping needed)  
`n` - repeat search in same direction  
`N` - repeat search in opposite direction  
`:%s/old/new/g` - replace all old with new throughout file  
`:%s/old/new/gc` - replace all old with new throughout file with confirmations  
`:21,$s/old/new/g` - replace line 21 - end  
`:.,$s/old/new/g` - current line to end  
`:.,.+5s/old/new/g` - current to current + 5  
`:g/old/list` - all lines matching old  
`:noh` - remove highlighting of search matches  

noh Options:  
* `%` - in all lines  
* `g` - all occunces in line  
* `i / I` - case in/sensitive  

### Regex ref
`\t` - tab, `\s` whitespace (space or tab)  
`\n` or `\r` newline  
Negate the collection with `[^` . For example `[^1a-c]`  

When replacing:
* `\r` newline
* `\n` is a null byte (0x00).  
* `\&` is ampersand (& is the text that matches the search pattern).  
* `\0` inserts the text matched by the entire pattern  
* `\1` inserts the text of the first backreference. `\2` inserts the second backreference, and so on.  

## Search in multiple files  
`:vim[grep] /pattern/ {file}` - search for pattern in multiple files. Examples:  
`:vim /foo/ **/*` - recursive search  
`:vim /pattern1/ find . -type f`
`:cn` - next match  
`:cp` - previous match  
`:copen` - open a window containing the list of matches  
`:colder / :cnewer` - navigates between previous searches  
`:grep pattern *.c` - grep can also be used (yay  

## Working with multiple files  
`:e file` - edit a file in a new buffer  
`:enew` - open one in the current window.  
`:bn or :bnext` - go to the next buffer  
`:bp or :bprev` - go to the previous buffer  
`:b #` - move to buffer # (where # = number)  
`:bd` - delete a buffer (close a file)  
`:ls` - list all open buffers  
`:sp file` - open a file in a new buffer and split window  
`:vsp file` - open a file in a new buffer and vertically split window  

## Opening buffers  
`:enew` open one in the current window.  
`:new` create a split window with an unnamed buffer.  
`:vnew` open one in a vertically split window.  
`:tabnew` open one in a new tab.  

## Window Commands  
`Ctrl + w + s` - split window  
`Ctrl + w + w` - switch windows  
`Ctrl + w + q` - quit a window  
`Ctrl + w + v` - split window vertically  
`Ctrl + w + n` - create new split window  
`Ctrl + w + hjkl` - moving between windows:  
`Ctrl + wt` - move the current split window into its own tab  
`<C-W>L` move the window  
`:split file.txt` opens file.txt on new h split  
`:vsplit file.txt` opens file.txt on new vertical split  

## Tabs  
`:tabnew` - open new tab  
`:tabnew file` - open a file in a new tab  
`gt` or `:tabnext` or `:tabn` - move to the next tab  
`gT` or `:tabprev` or `:tabp` - move to the previous tab  
`#gt` - move to tab number #  
`:tabmove #` - move current tab to the #th position (indexed from 0)  
`:tabclose` or `:tabc` - close the current tab and all its windows  
`:tabonly` or `:tabo` - close all other tabs  
`:tabdo command` - run the command on all tabs. Examples:  
`:tabdo q` - closes all opened tabs  
`:tabdo %s/bruno/hill/g` - replaces bruno by hill in all tabs  

## Ranges  
Format: `:line1,line2command`  
Examples:
`21` line 21 Ex: `:21s/old/new/g`  
`1` first line Ex: `:1s/old/new/g`  
`$` last line. Ex: `:$s/old/new/g`  
`.` current line. Ex: `:.w single.txt`  
`%` all lines (same as 1,$). Ex: `:%s/old/new/g`  
`21,25` lines 21 to 25 inclusive. Ex: `:21,25s/old/new/g`  
`21,$` lines 21 to end. Ex: `:21,$s/old/new/g`  
`.,$` current line to end. Ex: `:.,$s/old/new/g`  
`.+1,$` line after current line to end. Ex: `:.+1,$s/old/new/g`  
`.,.+5` six lines (current to current+5 inclusive). Ex: `:.,.+5s/old/new/g`  
`.,.5` same (.5 is interpreted as .+5). Ex: `:.,.5s/old/new/g`  

## Terminal  
`:term` - open terminal  
`:term tab` - open tab in a new terminal  

## VIM Tutorial  
`:help user-manual`  
`<C-]> ` - navigate hyperlink  
`<C-o> ` - go back
