
## About

When working with virtual environments in Python, it's recommended to use a custom version of Python rather than the server's version.
As the EOL of Python2 is already reached it will no longer receive security updates and additionally, the Linux Kernel doesn't support versions of Python lower than 2.7.15, thus one has to make sure to install a version >= 2.7.15.


## Installation

The following commands will install Python-2.7.15 to `/home/username/opt/python-2.7.15`:

```bash
cd /tmp
wget https://www.python.org/ftp/python/2.7.15/Python-2.7.15.tgz
tar zxvf Python-2.7.15.tgz
cd Python-2.7.15.tgz
./configure --prefix=$HOME/opt/python-2.7.15.tgz --with-ensurepip=install
make
make install
```

Here's a brief explanation of what'shappening:

**./configure**:
This is the configuration script for the Python source code that you have downloaded.
Running this script will prepare the build environment for your custom Python installation.

**--prefix=$HOME/opt/python-2.7.15**:
The *--prefix* option specifies the directory where you want your custom Python installation to be placed. 
In this case, it will be installed in *$HOME/opt/python-2.7.15*.

**--with-ensurepip=install**:
The *--with-ensurepip* option tells the configuration script to include the pip package manager in your custom Python installation. 
The *=install* option tells the script to install pip when you build and install your custom Python version.

---

In order to use the new version of Python over the system default it needs to be added to the *$PATH* environment variable.
Add this line at the end of the *~/.bash_profile* config: 

```bash
$ export PATH=$HOME/opt/python-2.7.15/bin:$PATH
# Then save and close the file and restart the shell
$ . ~/.bash_profile
# Check the version of Python that is being used
$ which python
```

It should return */home/username/opt/python-2.7.15/bin/python*.
If the response is something like */usr/bin/python* then it means that the newly installed version isn't used.
In that case it's recommended to logout and login again as it most likely is due to the *.bash_profile* that is not properly updated.




