Linux Debian systems, managing users can be done through the terminal using Bash commands. Below are some of the most important Bash commands for managing users:

### Adding a User

To add a new user to the system, use the `adduser` command followed by the username: ^2eff8f

```bash
sudo adduser username
```

This will prompt you to enter a password and additional user information.

### Deleting a User

To delete a user from the system, use the `deluser` command followed by the username:

```bash 
sudo deluser username
```

This will remove the user's home directory and any files associated with the user.

### Changing the Password

To modify a user's attributes such as their password, use the `passwd` command followed by the username:

```bash
sudo passwd username
```

This will prompt you to enter a new password for the user.

### Granting Sudo Privileges

To grant a user sudo privileges, add the user to the sudo group using the `usermod` command followed by the username:

```bash 
sudo usermod -aG sudo username
```

### Listing Users

To list all the users on the system, use the `cat` command to display the contents of the `/etc/passwd` file:

```bash
cat /etc/passwd
```

This will display a list of all users, their user ID, home directory, and default shell.

### Switching User Accounts

To switch to another user account, use the `su` command followed by the username:

```bash
su username
```

This will prompt you to enter the user's password and switch to their account.