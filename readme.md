
## Flatpaks:
```
flatpak install ca.desrt.dconf-editor
flatpak install com.bitwarden.desktop
flatpak install com.github.tchx84.Flatseal
flatpak install com.visualstudio.code
flatpak install org.mozilla.firefox
flatpak override --user --env=MOZ_USE_XINPUT2=1 org.mozilla.firefox
```

## Apk Packages:
```
doas apk add zsh neovim keyd

# Configure zsh to use XDG base dir spec
echo "ZDOTDIR=$HOME/.config/zsh" | doas tee /etc/zsh/zshenv

cat << 'EOF' > ~/.config/zsh/.zshrc
HISTFILE="$XDG_STATE_HOME"/zsh/history
HISTSIZE=1000
SAVEHIST=1000
setopt autocd
bindkey -v
zstyle ':completion:*' cache-path $XDG_CACHE_HOME/zsh/zcompcache
autoload -Uz compinit
compinit -d $XDG_CACHE_HOME/zsh/zcompdump-$ZSH_VERSION
alias vim=nvim
PATH="$HOME/.local/bin:$PATH"
EOF
```

## VSCode Config:
```
cat << 'EOF' > ~/.var/app/com.visualstudio.code/config/Code/User/settings.json
{
    "workbench.colorTheme": "Default Dark Modern",
    "window.titleBarStyle": "custom",
    "amVim.useSystemClipboard": true,
    "amVim.bindCtrlCommands": false
}
EOF
```

## Gnome:
```
# Disable "Super" and replace with "Super+Space"
gsettings set org.gnome.mutter overlay-key ''
dconf write /org/gnome/shell/keybindings/toggle-overview "['<Super>space']"
```

## Gnome Extensions:
- [Dash to Dock](https://extensions.gnome.org/extension/307/dash-to-dock/)
- [V-Shell](https://extensions.gnome.org/extension/5177/vertical-workspaces/)

## Potential solutions to dotfiles in home dir

- [libetc](https://ordiluc.net/fs/libetc/README) intercepts file operations via `LD_PRELOAD`
- [boxxy](https://github.com/queer/boxxy) put each app in a box and configure its dotfiles
- [fakehome](https://tomwh.uk/blog/posts/2020/03/28/fake-home-prison/) modifies `$HOME` on a per-app basis

