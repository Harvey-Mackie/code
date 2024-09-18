---
id: NeoVim
aliases: []
tags: []
---

Note - Repo used for dotfiles https://github.com/Harvey-Mackie/dotfiles

Aim - Curious about NeoVim, get it working and document how it works.

# Useful Videos
Customise zshrc - https://www.youtube.com/watch?v=wNQpDWLs4To
- instead of using terminal, I will now use iterm

Setting up neovim - https://www.youtube.com/watch?v=4zyZ3sw_ulc&list=PLsz00TDipIffreIaUNk64KxTIkQaGguqn&index=2

# Notes
Getting started
- Run brew install Neovim
- Create .config/nvim
	- Clone repo - https://github.com/LazyVim/starter into nvim
- Run nvim to get started

Unsorted
- Started watching - https://www.youtube.com/watch?v=N93cTbtLCIM
- Can get to the file UI by typing `SPACE + e`

##### Commands
- [space] + [f] - search for files in current folder space
- space + space - search for files in root directory (home) 
- Lazy sync - sync config files/plugins

#### tinkering

##### java integration 
http://www.lazyvim.org/extras/lang/java
You can use Java - I'm working on getting this working, appears to be a bit tricky due to the `jdtls`



##### plugins

###### telescope
Used for 'find files' and the 'grep' feature. Displays a UI of all the files which match your filter.

Useful Commands:
- When searching for a file, use CTRL + D | U to scroll the file in the preview


###### lazygit

Commands
- space + g - lazygit
```
brew install lazygit
```
```
```

###### neo-tree
Add to lua/plugins, they are automatically generated, here is an example of how I displayed hidden files in neo-tree.

Commands
- space + e - open neo-tree
- space + a - add new file or directoy in neo-tree
- 'k (copy), p (paste) move file/directory 

```
return {
  "nvim-neo-tree/neo-tree.nvim",
  opts = {
    filesystem = {
      filtered_items = {
        visible = true,
      },
    },
  },
}
```
