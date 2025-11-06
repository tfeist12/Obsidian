Potentially create a script to set everything I can up all at once

[Windows Terminal Preview](https://github.com/microsoft/terminal)
[Terminal Config](https://gist.github.com/tfeist12/ffe213f28092049a66465beff35a638c)
[CaskaydiaCove Nerd Font](https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/CascadiaCode.zip)


WSL 2:
Debian 12 Bookworm
```
wsl --install -d Debian
```

[Neovim Install](https://github.com/neovim/neovim/blob/master/INSTALL.md):
```
curl -LO https://github.com/neovim/neovim/releases/download/v0.11.5/nvim-linux-x86_64.tar.gz
sudo rm -rf /usr/local/nvim-linux64.tar.gz
sudo tar -C /usr/local -xzf nvim-linux64.tar.gz
```
[Nvim Config](https://github.com/tfeist12/NvChad)

[Tmux](https://github.com/tmux/tmux) :
```
wget tmux-*.tar.gz (Must use > 3.3a to avoid clipboard issues)
tar -zxf tmux-*.tar.gz
cd tmux-*/
./configure
make && sudo make install
```
[Tmux Autocomplete](https://russellparker.me/post/2018/02/16/tmux-bash-autocomplete/)
```
curl https://raw.githubusercontent.com/imomaliev/tmux-bash-completion/master/completions/tmux > /usr/share/bash-completion/completions
```
[Tmux Config](https://gist.github.com/tfeist12/824b8663b3f5d33a576723e0d57730aa)

[Install Cargo:](https://doc.rust-lang.org/cargo/getting-started/installation.html)
```
curl https://sh.rustup.rs -sSf | sh
```

[Fuzzy Finding using fzf:](https://github.com/junegunn/fzf)
```
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

[Install Vivid:](https://github.com/sharkdp/vivid)
```
cargo install vivid
```

[Starship:](https://starship.rs/)
```
curl -sS https://starship.rs/install.sh | sh
```
[Starship Config](https://gist.github.com/tfeist12/559f7953d8302dbf3d9f2951de57915b)

Bash Setup:
[.bashrc](https://gist.github.com/tfeist12/a802180a77d0837a5381f4e3dc4ba2cc)
[.inputrc](https://gist.github.com/tfeist12/a802180a77d0837a5381f4e3dc4ba2cc)