## Step 1: Enable Container Features

The first step is to enable the Windows Server 2019 containers feature. Open PowerShell as Administrator:

```powershell
Install-Module -Name DockerMsftProvider -Repository PSGallery -Force
```

This will install the `Docker-Microsoft PackageManagement` Provider from the PowerShell Gallery. 

## Step 2: Install Docker

Once the Containers feature is enabled on Windows Server, install the latest Docker Engine and Client by running the command below in your PowerShell session:

```powershell
Install-Package -Name docker -ProviderName DockerMsftProvider
```

When the installation is complete, reboot the computer:

```powershell
Restart-Computer -Force
```

Installed Docker version can be checked with:

```powershell
Administrator> Get-Package -Name Docker -ProviderName DockerMsftProvider
 Name                           Version          Source                           ProviderName
 ----                           -------          ------                           ------------
 docker                         18.09.2          DockerDefault    
```

The same can be achieved with the `docker version` command:

```powershell
PS C:\Users\Administrator> docker version
 Client:
  Version:           18.09.2
  API version:       1.39
  Go version:        go1.10.6
  Git commit:        1ac774dfdd
  Built:             unknown-buildtime
  OS/Arch:           windows/amd64
  Experimental:      false
 error during connect: Get http://%2F%2F.%2Fpipe%2Fdocker_engine/v1.39/version: open //./pipe/docker_engine: The system cannot find the file specified. In the default daemon configuration on Windows, the docker client must be run elevated to connect. This error may also indicate that the docker daemon is not running.
```

Upgrade can be done anytime by running the following command on PowerShell:

```powershell
Install-Package -Name Docker -ProviderName DockerMsftProvider -Update -Force
```

## Step 3: Run Docker Container

Start the Docker Daemon:

```powershell
Start-Service Docker
```

After starting Docker Engine service, Download the pre-created .NET sample image from the Docker Hub registry:

```powershell
docker pull mcr.microsoft.com/dotnet/samples:dotnetapp-nanoserver-2009
```

You can retrieve a list of all available tags for dotnet/samples at https://mcr.microsoft.com/v2/dotnet/samples/tags/list

Then deploy a simple container running a `.Net Hello World` application:

```powershell
docker run mcr.microsoft.com/dotnet/samples:dotnetapp-nanoserver-2009
```

The container will start, print the hello world message, and then exit.

## Steop 4: Running Linux Containers

Out of the box, Docker on Windows only run Windows container. 
To use Linux containers on Windows Server, you need to use the Docker Enterprise Edition Preview which includes a full LinuxKit system for running Docker Linux containers.

Uninstall your current Docker CE:

```powershell
Uninstall-Package -Name docker -ProviderName DockerMSFTProvider
```

Enable Nested Virtualization if you’re running Docker Containers using Linux Virtual Machine running on Hyper-V.

```powershell
Get-VM WinContainerHost | Set-VMProcessor -ExposeVirtualizationExtensions $true
```

Then install the current preview build of Docker EE:

```powershell
Install-Module DockerProvider
Install-Package Docker -ProviderName DockerProvider -RequiredVersion preview
```

Enable LinuxKit system for running Linux containers:

```powershell
[Environment]::SetEnvironmentVariable("LCOW_SUPPORTED", "1", "Machine")
```

Restart Docker Service after the change:

```powershell
Restart-Service docker
```

Pull a test docker image:
```powershell
> docker run -it --rm ubuntu /bin/bash
 root@1440a7fef7e0:/# cat /etc/os-release 
 NAME="Ubuntu"
 VERSION="18.04.1 LTS (Bionic Beaver)"
 ID=ubuntu
 ID_LIKE=debian
 PRETTY_NAME="Ubuntu 18.04.1 LTS"
 VERSION_ID="18.04"
 HOME_URL="https://www.ubuntu.com/"
 SUPPORT_URL="https://help.ubuntu.com/"
 BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
 PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
 VERSION_CODENAME=bionic
 UBUNTU_CODENAME=bionic

 root@1440a7fef7e0:/# exit
 exit
```

To Switch back to running Windows containers, run:

```powershell
[Environment]::SetEnvironmentVariable("LCOW_SUPPORTED", "$null", "Machine")
```
