# Installation

```bash
sudo apt install zsh
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

## Must-Have Plugins

https://github.com/sharkdp/bat
https://github.com/ogham/exa


# Commands

<table>  
  <tr>  
    <th>Command</th>  
    <th>Description</th>  
  </tr>  
  <tr>  
    <td>alias</td>  
    <td>List all aliases</td>  
  </tr>  
  <tr>  
    <td>mkcd</td>  
    <td>Create a new directory and change to it, will create intermediate directories as required.</td>  
  </tr>
  <tr>  
    <td>mkcd</td>  
    <td>Like <code>mkcd</code>, but also knows how to handle remote URLs.<br>
When given an argument that looks like a URL (something that ends in <code>.git</code> or <code>.tar.gz|bz2|xz)</code>),<br>
download the remote resource and extract it (if necessary) into the current directory.<br>
When change to the newly extracted/downloaded/cloned directory.
    </td>  
  </tr>
  <tr>  
    <td>zsh_stats</td>  
    <td>Get a list of the top 20 commands and how many times they have been run.</td>  
  </tr>
</table>


# Aliases

<table role="table">
	<tr>
		<th align="left">Alias</th>
		<th align="left">Command</th>
	</tr>
	<tr>
		<td align="left">md</td>   
		<td align="left">mkdir -p</td>   
	</tr>  
	<tr>   
		<td align="left">rd</td>    
		<td align="left">rmdir</td> 
	</tr> 
	<tr>    
		<td align="left">cd / ~</td>      
		<td align="left">cd to your home directory</td>
	</tr>
	<tr>    
		<td align="left">..</td>   
		<td align="left">cd ..</td> 
	</tr> 
	<tr>     
		<td align="left">...</td>       
		<td align="left">cd ../..</td> 
	</tr>  
	<tr>    
		<td align="left">....</td> 
		<td align="left">cd ../../..</td> 
	</tr> 
	<tr> 
		<td align="left">.....</td>  
		<td align="left">cd ../../../..</td> 
	</tr>   
	<tr> 
		<td align="left">/</td> 
		<td align="left">cd /</td>  
	</tr>
	<tr>   
		<td align="left">d</td>      
		<td align="left">dirs -v (lists last visited directories)</td> 
	</tr>
	<tr>
		<td align="left">cd + n</td>  
		<td align="left">Switch to directory number n</td>  
	</tr>  
	<tr> 
		<td align="left">-</td>
		<td align="left">cd to last visited directory</td> 
	</tr>
	<tr>  
		<td align="left">1</td>     
		<td align="left">cd -1</td>
	</tr>
	<tr>
		<td align="left">2</td>
		<td align="left">cd -2</td>
	</tr>
	<tr>      
		<td align="left">3</td>    
		<td align="left">cd -3</td>
	</tr>
	<tr>   
		<td align="left">4</td>  
		<td align="left">cd -4</td>
	</tr>
	<tr>      
		<td align="left">5</td>      
		<td align="left">cd -5</td>   
	</tr>
	<tr>     
		<td align="left">6</td>     
		<td align="left">cd -6</td>
	</tr>
	<tr>   
		<td align="left">7</td>     
		<td align="left">cd -7</td>
	</tr>
	<tr>    
		<td align="left">8</td>      
		<td align="left">cd -8</td>
	</tr>
	<tr>     
		<td align="left">9</td>       
		<td align="left">cd -9</td>
	</tr>
</table>


# Config
```bash
plugins=(git aliases colorize)

source $ZSH/oh-my-zsh.sh

# User configuration

export ZSH_COLORIZE_TOOL="chroma"
export ZSH_COLORIZE_STYLE="colorful"
export ZSH_COLORIZE_CHROMA_FORMATTER="terminal256"

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
alias zshconfig="vim ~/.zshrc"
alias ohmyzsh="vim ~/.oh-my-zsh"


# map exa commands to normal ls commands
alias ll="exa -l -g --icons"
alias ls="exa --icons"
alias lt="exa --tree --icons -a -I '.git|__pycache__|.mypy_cache|.ipynb_checkpoints'"
alias la="exa -lhaGF --icons"
# show file previews for fzf using bat
# alias fp="fzf --preview 'bat --style=numbers --color=always --line-range :500 {}'"
```