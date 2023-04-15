# Basic WSL2 commands

-   `wsl --list`: List available distributions in WSL
-   `wsl --set-default <distribution_name>`: Set the default distribution
-   `wsl --set-version <distribution_name> 2`: Upgrade a WSL1 distribution to WSL2
-   `wsl --shutdown`: Shutdown all running distributions
-   `wsl --import <distribution_name> <import_directory> <installation_tar_file>`: Import a distribution from a tar file
-   `wsl --export <distribution_name> <export_tar_file>`: Export a distribution to a tar file

# Running and managing WSL2 distributions

-   `wsl`: Launch the default distribution
-   `wsl -d <distribution_name>`: Launch a specific distribution
-   `wsl -d <distribution_name> -u <username>`: Launch a specific distribution as a specific user
-   `wsl --terminate <distribution_name>`: Terminate a specific distribution
-   `wsl --install`: Install WSL2 on the current system (if not already installed)

# Networking in WSL2

-   `ip a`: Show the network interfaces and their IP addresses
-   `ping <hostname_or_IP_address>`: Test connectivity to a host
-   `ssh <username>@<hostname_or_IP_address>`: Connect to a remote host using SSH