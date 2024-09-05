Repo - https://github.com/Harvey-Mackie/dotfiles

Aim - storing dot files can be a challenge. Without using Git, you risk losing your files.

Solution - Use a dotfiles repo and then add symbolic links to the desired location 

Example

   Create Links

    #zshrc
    ln -s .zshrc ~/.zshrc

    #nvim
    ln -s ~/dotfiles/nvim/init.lua ~/.config/nvim/init.lua
    ln -s ~/dotfiles/nvim/config ~/.config/nvim/config
    ln -s ~/dotfiles/nvim/lua ~/.config/nvim/lua

    #vim
    ln -s .vimrc ~/.vimrc


   Undo Links

     rm ~/.config/nvim
