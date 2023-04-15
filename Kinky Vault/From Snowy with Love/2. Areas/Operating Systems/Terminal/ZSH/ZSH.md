# Overview
 
```ccard
type: folder_brief_live
```

# Installing Oh-My-Zsh on Debian-Based Systems
To start, let’s install Zsh:

```bash
$ sudo apt-get install zsh
$ zsh --version
```

You may see a version equal or greater than 5.1.1. The next step is the installation of Oh-My-Zsh:
```bash
$ sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

When the installation script finishes the command prompt is probably different from before. 
It means Oh-My-Zsh was successfully installed. 
If the prompt looks too minimalistic for you, don’t panic. Oh-My-Zsh accepts themes and this is just the default one: **robbyrussell**. 
To change it, go to the home folder, edit the hidden file `.zshrc`, and change the variable `ZSH_THEME` to **bureau**, which is my favorite theme:

```bash
$ cd ~
$ vim .zshrc
  ...
  ZSH_THEME="bureau"
  ...
$ source .zshrc
```

For a complete list of themes, checkout the [theme catalog](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes). 
Make sure you have some time to spare because trying new themes is addictive.

Oh-My-Zsh won’t start by default. To activate it we have to type `$ zsh` every time we open a new terminal.
To replace the default shell: `chsh -s /bin/zsh`