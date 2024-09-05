#draft

Cheat Sheet - https://vim.rtorr.com
# Add File
`vi newfile.txt` - creates if not exists

# Editing File

## General
- dw - delete word
- cw - change word
- yy - copy line
- yiw - copy current word
- ggVG (select file) + y (copy) - copy full document
- VG + y - copy from cursor down
- V - Enter visual mode. This will start highlighting lines, then click 'y' to copy to clipboard


## Add new line below existing
Press `o`

## Delete current line
Press `dd`

## Go to end of line
Press `Shift A`

## Undo previous change
Press `u`
Press `Ctrl + r` to redo change

## Copy and Paste line
When in reading mode:
	Copying a line - `yy`
	Paste line - `p`
	Edit 

## Search and Replace
- Searching - Press `/text` then use 'n' to move to next occurance, 'N' to move to previous occurance
- Search and Replace first occurance - `:s/old/new`
- Search and Replace all occurances  - `:%s/old/new/g`



# Exiting File
- Save and quit - `:wq`
- Quit - `:q`
- Quit without saving- `:q!`
- `:w` write to disk


# Linux
`[command] | less` - opens in Vim and can perform commands (in read-only)
