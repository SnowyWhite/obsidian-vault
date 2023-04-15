# Overview

These are just some notes that I use when setting up a new server or VM.

## Adding SSH keys

On the local machine a SSH key pair can be generated as follows:

```bash
ssh-keygen -t rsa -b 4096
```

It has to be stored under the `~/.ssh` directory but can have any name.
There are two ways to copy the public key to the server:
- `ssh-copy-id`: Just type in `ssh-copy-id user@server` and it will automatically place the last created public key at the right directory
- Going nuts: `cat id_rsa.pub | ssh user@server "mkdir -p ~/.ssh && touch ~/.ssh/authorized_keys && chmod -R go= ~/.ssh && cat >> ~/.ssh/authorized_keys"`

These 2 commands are important to remove any  unwanted permissions from the `~/.ssh` folder and the files inside:

```bash
chmod -R go= ~/.ssh
chown -R user:usergroup /home/user/.ssh # Only necessary if the root account was used to create the keys
```


## Disabling password authentication

To enhance the security, password-based logins can be disabled.
Run these commands as root:

````bash
vim /etc/ssh/sshd_config
# Set PasswordAuthentication to No

systemctl restart ssh
````


## Adding a new user

Run these two commands to add a new [[User Management|user]] :

```bash
adduser user
usermod -aG sudo user
```


## Setting up basic firewall

Install ufw if it isn't installed yet:

```bash
sudo apt install ufw
```

Firewall profiles allow UFW to manage named sets of firewall rules for installed applications. 
Profiles for some common software are bundled with UFW by default and packages can register additional profiles with UFW during the installation process. 
OpenSSH, the service allowing us to connect to our server now, has a firewall profile that we can use.

You can list all available application profiles by typing:

```bash
sudo ufw app list

OutputAvailable applications:
 . . .
 OpenSSH
 . . .
```

We need to make sure that the firewall allows SSH connections so that we can log back in next time.
Run this command to allow SSH:

```bash
sudo ufw allow OpenSSH
```

Afterwards,  enable the firewall by typing:

``` bash
sudo ufw enable
```

You can verify that SSH connections are still allowed by typing:

```bash
sudo ufw status

OutputStatus: active

To             Action   From
--             ------   ----
OpenSSH          ALLOW    Anywhere
OpenSSH (v6)     ALLOW    Anywhere (v6)
```

**As the firewall is currently blocking all connections except for SSH**, if you install and configure additional services, you will need to adjust the firewall settings to allow acceptable traffic in.

## Change the language

The first step is to configure environment variables such as `LANG`, `LANGUAGE`, `LC_CTYPE`, `LC_MESSAGES` to your local language. 
Usually `LANG` (or `LC_ALL`) is sufficient.

Check with this command which variables are already set:

```bash
env | grep LANG
```

Then you can add a new one like this:

```bash
export LANG=en_US.UTF-8
export LANGUAGE=en_US.UTF-8
export LC_CTYPE=en_US.UTF-8
export LC_MESSAGES=en_US.UTF-8
export LC_ALL=en_US.UTF-8
```

Run this as last step to set the desired language:

```bash
dpkg-reconfigure locales
```

It will open a TUI where you can select the language.

>[!note]
> Do not forget to reboot afterwards.


