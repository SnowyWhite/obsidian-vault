## Installing ZSH

Installing the ZSH shell on a debian based distro is as simple as:

```bash
sudo apt install zsh
# Verify that it is installed
zsh --version
```

To change the default shell from bash to ZSH you can use following command.
Relaunch the terminal (e.g. by logging out and in again) to make sure the changes take effect.

```bash
# May requires sudo privilueges
chsh -s $(which zsh)
```

## Installing an additional framework

ZSH in its pure form is already amazing, but using a framework on top of it really unleashes the full power and customability.

### Oh My ZSH

Oh My ZSH is an open source, community-driven framework that helps managing your ZSH configuration.
It comes with a ton of themes, plugins and functions that can easily be further configured.

Get more information here: https://ohmyz.sh/
Official Github repository: https://github.com/ohmyzsh/ohmyzsh

#### Installation

Run this command to directly install Oh My ZSH:

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Explanation of the command:
- **curl** => Just one possible tool for downloading web content, alternatives are for example `wget` or `fetch`
`f`$\quad$Aborts immediatly if an error occurs and doesn't show output in such case
`s`$\quad$Silent mode, thus no additional output in the console
`S`$\quad$Shows errors anyway when `s` is used
`L`$\quad$Follows redirections
<br>  
- **"$()"** => The content in between the brackets will be evaluated before the rest of the line is evaluated. 
The evaluated content is then put in between quotation marks.
So summarized, this will build a string of the file content  and pass it to `sh`.
<br>
- **sh** => That's `dash`, the standard command interpreter of your system, used to execute the commands in the script
`c`$\quad$Used to read the commands from a string instead of from the standard input
  
It's always good practice to inspect a script before blindly running it.
The `install.sh` script also contains some additional notes you can take into consideration before you run it.
To download the script and inspect it, run this commands:

```bash
curl -O install.sh https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh
cat install.sh
```

To verify that the installation was successful you can run this command:

```bash
echo $SHELL
```

It should print `usr/bin/zsh`.

### Powerlevel10k

This is a theme for ZSH that can be either installed manually on top of a basic ZSH installation or on top of a Oh My ZSH installation.
Have a look at their comprehensive Github repository to learn more: https://github.com/romkatv/powerlevel10k

#### Installation

Run these commands if you want to just use it together with ZSH:

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

To use it in combination with Oh My ZSH:

1. Install the theme in the oh-my-zsh themes directory:

```bash 
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

2. Tell ZSH to use the theme by appending this line in your `~/.zshrc` config:

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

3. Reload the shell by entering following command:

```bash
omz reload
```

(`omz` stands for oh-my-zsh and provides some other nice features.)

## Installing nerdfonts

Some themes require special fonts to work properly.
They enable the usage of icons, for example to indicate when the current directory you are in is a git repository.

You can find a great selection of these fonts here:
- https://github.com/ryanoasis/nerd-fonts
- https://fontawesome.com/
- https://github.com/powerline/fonts

As an example I'll show how to install the [Hack Font](https://github.com/powerline/fonts/tree/master/Hack) as it is one of my favorite fonts.
Just replace the download link with one of your choice.

<img src="https://raw.githubusercontent.com/powerline/fonts/master/Hack/hack-specimen-for-Powerline.png" alt="hackfont" width="200px">

1. Add the font (`-O` is to set the name of the output file)

```bash
wget -O font.ttf https://github.com/powerline/fonts/raw/master/Hack/Hack-Regular.ttf  
```

2. Unzip the archive and move the font files to the fonts directory

```bash
unzip Hack-v3.003-ttf.zip -d ~/.local/share/fonts/
```

3. Refresh the font cache to load the new font

```bash
fc-cache -fv
```

- `f`$\quad$Scans any directory that usually serves as a valid font cache
- `v`$\quad$Displays all the fonts that are loaded into the cache

The final step is to configure your terminal to use it,  I won't go into details for this step, just use Google as there are plenty of resources for all common terminals available.

## Set a theme

To change the theme for `zsh` you can edit following line in the `~/.zshrc` config:

```bash
ZSH_THEME="xiong-chiamiov"
```

If you set it to `random` it will use a different theme for each terminal session.
You can get a list of available themes by entering this command:

```bash 
omz theme list
```

And to change it from the command line:

```
omz theme set <name>
```

>[!note]
> These are some themes I like:
> - amuse
> - frisk
> - jispwoso


### Edit prebuilt theme

You can configure every theme to your liking by editing its config file.

- For example if you have `powerlevel10k` installed, open this file with your favorite text editor: 
 `~/.oh-my-zsh/custom/themes/powerlevel10k/powerlevel10k.zsh-theme` 
 
- Scroll to the `prompt_powerlevel10k` function and customize the prompt to your liking.
- Save the file and reload your `~/.zshrc` file by entering the following command:

```bash
omz reload
```

## Installing plugins

There are so many cool plugins available that I can only limit myself to my personal favorites.

### Official Plugins

Oh My ZSH already comes bundled with plugins which you can immediatly use by editing the `~/.zshrc` config.
Search the line that looks like `plugins=()`, in between the brackets you can add the plugins with a space inbetween them.
Check out the [Github Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins) to get an overview of the sheer amount of official plugins.

Personally I always have at least these 2 plugins enabled:

```bash
plugins=(aliases colorize)
```
- `aliases`$\quad$Lists all the aliases (shortcuts) provided by plugins that you can currently use by running `acs`
- `colorize`$\quad$Enables syntax highlighting of file contents for over 300 supported languages and other text formats

Please note that `colorize` requires an additional tool to work, either `pygments` or `chroma`.
I use `chroma` and you can install it with:

```bash
sudo apt install chroma
```

Please refer to the Github repos for more details:
- aliases: https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/aliases
- colorize: https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/colorize

### Additional Plugins

There are a few plugins I use in addition to the official plugins for which I describe the installation steps here.

#### FZF 
say yes to each option during installation.

```bash
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
```

Then update the `~/.zshrc` config:

```bash
# update your ~/.zshrc file
FZF_BASE="$HOME/.fzf"

plugins=(fzf)
```

You can now activate the fuzzy finder by either typing `fzf` as a command to your terminal or pressing `CTRL`+`T`. 

#### exa

`exa` aims to be replacement for `ls`.
The detailed documentation can be found here: https://the.exa.website
It provides colored output as well as icons for better distinction of different file formats and directories as well as extended types of views.

1. Install it with this command

```bash
sudo apt install exa
```

2. Replace `ls` 
For me the best thing to do is adding aliaes to it that at the same time replace the built-in `ls` command.
Add these lines at the bottom of your `~/.zshrc`  config to get 4 handy shortcuts:
```bash
# map exa commands to normal ls commands
alias ll="exa -l -g --icons"
alias ls="exa --icons"
alias lt="exa --tree --icons -a -I '.git|__pycache__|.mypy_cache|.ipynb_checkpoints'"
alias la="exa -lhaGF --icons"
 ```

#### [[bat]]

I use `bat` as a better version of `cat`. It provides syntax-highlighting, automatic paging, showing line numbers, git changes and much more.

1. Install it with this command:

```bash
sudo apt install bat
```

2. Sometimes the tool is called `batcat` when you install it with `apt` due to some naming conflicts.
If that's the case you can create a symlink in order to use it with the original name.

```bash
mdkir -p ~/.local/bin
ln -s /usr/bin/batcat ~/.local/bin/bat
```

3. To use it as replacement for `cat` with some neat features enabled, add this to your `~/.zshrc` config:

```bash
# map bat commands to normal cat commands
alias cat="batcat --paging=never --color=always"
alias bathelp="cat --plain --language=help"
help() {
	"$@" --help 2>&1 | bathelp
}
```

--- 

>[!attention] Plugins / Tool below were just pasted to not forget it
#### brew

```bash
# Installation
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# Add Homebrew to PATH
(echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> /home/USER/.profile  
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
# Install dependencies
sudo apt-get install build-essential
```

#### FZF

```bash
brew install fzf
$(brew --prefix)/opt/fzf/install
```


#### Nmap

<b>Aliases</b>
-   `nmap_open_ports`: scan for open ports on target.
-   `nmap_list_interfaces`: list all network interfaces on host where the command runs.
-   `nmap_slow`: slow scan that avoids to spam the targets logs.
-   `nmap_fin`: scan to see if hosts are up with TCP FIN scan.
-   `nmap_full`: aggressive full scan that scans all ports, tries to determine OS and service versions.
-   `nmap_check_for_firewall`: TCP ACK scan to check for firewall existence.
-   `nmap_ping_through_firewall`: host discovery with SYN and ACK probes instead of just pings to avoid firewall restrictions.
-   `nmap_fast`: fast scan of the top 300 popular ports.
-   `nmap_detect_versions`: detects versions of services and OS, runs on all ports.
-   `nmap_check_for_vulns`: uses vulscan script to check target services for vulnerabilities.
-   `nmap_full_udp`: same as full but via UDP.
-   `nmap_traceroute`: try to traceroute using the most common ports.
-   `nmap_full_with_scripts`: same as nmap_full but also runs all the scripts.
-   `nmap_web_safe_osscan`: little "safer" scan for OS version as connecting to only HTTP and HTTPS ports doesn't look so attacking.
-   `nmap_ping_scan`: ICMP scan for active hosts.

#### Aliases
-   `acs`: show all aliases by group    
-   `acs -h/--help`: print help mesage    
-   `acs <keyword(s)>`: filter and highlight aliases by `<keyword>`    
-   `acs -g <group>/--group <group>`: show only aliases for group `<group>`. Multiple uses of the flag show all groups
-  `acs --groups`: show only group names


## Config tweaks

These are just some snippets you can add to your `~/.zshrc` config to enhance the functionality.

### Aliases

```bash
# Get your current public IP address
alias myip="curl ipinfo.io/ip"
alias myipv="curl ipinfo.io"

# Shows the processes using the most CPU resources
alias topcpu="ps -eo pid,user,%cpu,%mem,args --sort=-%cpu | head"

# Shows the weather forecast for your location in the terminal
alias weather='curl wttr.in'

# Enable syntax highlighting in less command
alias less='less -R'

# Open current directory in a new tab in the same terminal window
alias t='gnome-terminal --tab --working-directory="$PWD"'

# Search history with fzf
alias h='history | fzf'

# Open nvim with files and directories selected in fzf
alias v='nvim $(fzf --multi)'
```

### Functions

This  function iterates through all the themes in the `~/.oh-my-zsh/custom/themes` directory and sources each one to preview them. 
You can then use the arrow keys to move up and down through the themes.

```bash
function themes() { 
	for theme in ~/.oh-my-zsh/custom/themes/*(.); 
	do 
		echo "\n$theme\n"; 
		omz theme set $theme; 
	done
}
```

this simple generates a random password:

```bash 
function randpasswd() {
  tr -dc 'A-Za-z0-9!"#$%&\047()*+,-./:;<=>?@[\]^_`{|}~' </dev/urandom | head -c "${1:-32}";
  echo '';
}
```

### Exports and flags

Add these lines to change settings of ZSH or some previous mentioned plugins.

```bash
# Adding GOPATH environment variable
export GOROOT=/usr/lib/go
export GOPATH=$HOME/go
# Adding everything to path
export PATH=$PATH:$GOROOT/bin:$GOPATH/bin

# Open man pages in fzf preview window
export FZF_DEFAULT_OPTS='--preview "man {}"'

# Change color settings
export ZSH_COLORIZE_TOOL="chroma"
export ZSH_COLORIZE_STYLE="colorful"
export ZSH_COLORIZE_CHROMA_FORMATTER="terminal256"

setopt autocd              # change directory just by typing its name
setopt correct            # auto correct mistakes
setopt interactivecomments # allow comments in interactive mode
setopt magicequalsubst     # enable filename expansion for arguments of the form ‘anything=expression’
setopt nonomatch           # hide error message if there is no match for the pattern
setopt notify              # report the status of background jobs immediately
setopt numericglobsort     # sort filenames numerically when it makes sense
setopt promptsubst         # enable command substitution in prompt

# enable completion features
autoload -Uz compinit
compinit -d ~/.cache/zcompdump
zstyle ':completion:*:*:*:*:*' menu select
zstyle ':completion:*' auto-description 'specify: %d'
zstyle ':completion:*' completer _expand _complete
zstyle ':completion:*' format 'Completing %d'
zstyle ':completion:*' group-name ''
zstyle ':completion:*' list-colors ''
zstyle ':completion:*' list-prompt %SAt %p: Hit TAB for more, or the character to insert%s
zstyle ':completion:*' matcher-list 'm:{a-zA-Z}={A-Za-z}'
zstyle ':completion:*' rehash true
zstyle ':completion:*' select-prompt %SScrolling active: current selection at %p%s
zstyle ':completion:*' use-compctl false
zstyle ':completion:*' verbose true
zstyle ':completion:*:kill:*' command 'ps -u $USER -o pid,%cpu,tty,cputime,cmd'

# History configurations
HISTFILE=~/.zsh_history
HISTSIZE=1000
SAVEHIST=2000
setopt hist_expire_dups_first # delete duplicates first when HISTFILE size exceeds HISTSIZE
setopt hist_ignore_dups       # ignore duplicated commands history list
setopt hist_ignore_space      # ignore commands that start with space
setopt hist_verify            # show command with history expansion to user before running it
#setopt share_history         # share command history data

# force zsh to show the complete history
alias history="history 0"

# enable auto-suggestions based on the history
if [ -f /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh ]; then
        . /usr/share/zsh-autosuggestions/zsh-autosuggestions.zsh
        # change suggestion color
        ZSH_AUTOSUGGEST_HIGHLIGHT_STYLE='fg=#999'
fi

# enable command-not-found if installed
if [ -f /etc/zsh_command_not_found ]; then
        . /etc/zsh_command_not_found
fi

# set variable identifying the chroot you work in (used in the prompt below)
if [ -z "${debian_chroot:-}" ] && [ -r /etc/debian_chroot ]; then
        debian_chroot=$(cat /etc/debian_chroot)
fi

# Take advantage of $LS_COLORS for completion as well
zstyle ':completion:*' list-colors "${(s.:.)LS_COLORS}"
zstyle ':completion:*:*:kill:*:processes' list-colors '=(#b) #([0-9]#)*=0=01;31'

# Shortcuts to edit the config files
alias zshconfig="vim ~/.zshrc"
alias ohmyzsh="vim ~/.oh-my-zsh"

```


### ZSH Custom Theme
