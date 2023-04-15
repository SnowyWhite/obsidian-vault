# Overview

[Virtualenv](https://pypi.org/project/virtualenv/) is a tool used to create an isolated Python environment. 
This environment has its own installation directories that do not share libraries with other virtualenv environments 
or the globally installed libraries on the server. 

Virtualenv is the easiest and recommended way to configure a custom Python environment.

## [[Installing Virtualenv]]
- [Difference between virtualenv and venv]
- [Installing virtualenv using pip3]

## [[Installing custom modules]]

-   [Using pip to install Python 2 modules](https://help.dreamhost.com/hc/en-us/articles/115000221112-Using-pip-to-install-Python-2-modules)


## Creating a virtual environment using a custom Python 2 version

When working with virtual environments in Python, it's recommended to use a custom version of Python rather than the server's version.

- [[Installing custom Python2 version]]

### Building the virtual environment

Follow these steps to create a new virtual environment using a custom Python2 version:

1. Navigate to the directory / project where the virtual environment should be created and run this command:


> [!Attention]
> Make sure you specify the path to your custom installation of Python 2. If you do not, you'll end up using the system version of Python.

```bash
virtualenv -p /home/username/opt/python-2.7.15/bin/python <name_for_venv> # or .
source <name_for_venv>/bin/activate
(venv)[server]$ python -V
# Python 2.7.15
```

From now on, any package that you install using pip is placed in the virtual environments project folder, isolated from the global Python installation.

### Upgrade pip

It's a good idea to upgrade the version of pip to ensure you can install current modules.

```bash
(venv)[server]$ python -m pip install --upgrade pip
# Check the version
(venv)[server]$ pip --version
```


### Deleting your virtual environment

To delete a virtual environment, just delete its project folder. In this case, it would be:

```bash
(venv)[server]$ rm -rf <name_for_venv>
```

