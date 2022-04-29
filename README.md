# Navi Cheatsheet

This is my [navi](https://github.com/denisidoro/navi) cheatsheet collection.

Once you ran the install script below you should find a subfolder named `FullByte__navi-cheatsheet` in your navi config-path. Run ```navi info config-path``` to get your local navi path e.g. `~/.local/share/navi/cheats`. Navi should now be ready to use.

To use navi press `control`+`g` or type `navi`.

## Install Navi + This cheatsheet

Make sure to have the latest udpates: ```sudo apt update && sudo apt -y upgrade```

The following script will install and configure navi for bash and zsh add this repository and update the local cheatsheet on every boot:

```sh
# Install Navi
sudo apt -y install cargo ftf
cargo install --locked navi

# Config bash
bashrc=~/.bashrc
if [ -f "$bashrc" ];
then
    echo '\n### NAVI ###' >> ~/.bashrc
    echo 'alias navi="~/.cargo/bin/navi"' >> ~/.bashrc
    echo 'eval "\$(navi widget bash)"' >> ~/.bashrc
else
    echo "$bashrc file does not exist. Skipped."
fi

# Config zsh
zshrc=~/.zshrc
if [ -f "$zshrc" ];
then
    echo '\n### NAVI ###' >> ~/.zshrc
    echo 'alias navi="~/.cargo/bin/navi"' >> ~/.zshrc
    echo 'eval "\$(navi widget zsh)"' >> ~/.zshrc
else
    echo "$zshrc file does not exist. Skipped."
fi

# Install own cheatsheet and update on each boot
git clone "https://github.com/FullByte/navi-cheatsheet" "$(navi info cheats-path)/FullByte__navi-cheatsheet"
(crontab -l 2>/dev/null; echo "@reboot sleep 22 && cd \"$(navi info cheats-path)/FullByte__navi-cheatsheet\" && git pull") | crontab -
```
