
## Difference between virtualenv and venv

[venv](https://docs.python.org/3/library/venv.html) is a package that comes with Python 3. Python 2 does not contain venv.

[virtualenv](https://virtualenv.pypa.io/en/stable/) is a library that offers more functionality than venv. 
View the following link for a list of features venv does not offer compared to virtualenv.

-   [https://virtualenv.pypa.io/en/stable/](https://virtualenv.pypa.io/en/stable/)


Although you can create a virtual environment using venv with Python3, it's recommended that you install and use virtualenv instead.


## [Installing virtualenv using pip3]

If you're working with Python 3, you must install virtualenv using pip3. You maybe also want to install a custom version of Python 3.

- [Installing a custom version of Python 3](https://help.dreamhost.com/hc/en-us/articles/115000702772-Installing-a-custom-version-of-Python-3). 

This custom installation of Python 3 will also contain pip3. After it's installed **and activated**, run the which python3 command as shown below. 
This should return the location of your custom version of Python 3. You should then upgrade pip3.

```bash
[server]$ python3 -m pip install --upgrade pip
```

Once upgraded, install virtualenv using pip3:

```bash
[server]$ pip3 install virtualenvCollecting virtualenv
  Downloading virtualenv-15.1.0-py2.py3-none-any.whl (1.8MB)
    100% |████████████████████████████████| 1.8MB 367kB/s
Installing collected packages: virtualenv
Successfully installed virtualenv-15.1.0
```

You'll need the full path to the Python 3 version of virtualenv, so run the following to view it:

```bash
which virtualenv
/home/username/opt/python-3.10.1/bin/virtualenv
```

---
## Creating a virtual environment using a custom Python version

Be aware that you may need to reinstall Python following a server operating system upgrade.

When working with virtual environments in Python, it's common to use a [custom version of Python](https://help.dreamhost.com/hc/en-us/articles/115000702772-Installing-a-custom-version-of-Python-3) rather than the server's version. 
To create a new virtual environment using your custom installed version of Python, follow these steps:

The following steps use Python version 3.10.1. Make sure to use the version you installed.

1. Make a note of the full file path to the custom version of Python you just installed. 
   If you've followed the instructions in the [installation article](https://help.dreamhost.com/hc/en-us/articles/115000702772-Installing-a-custom-version-of-Python-3), the full path is:

```bash
which python3
/home/username/opt/python-3.10.1/bin/python
```
   
2. Navigate to your [site's directory](https://help.dreamhost.com/hc/en-us/articles/360001219231#the-website-directory), where you'll create the new virtual environment:
 
```bash
cd ~/example.com
```

3. Update your .bash\_profile

```bash
. ~/.bash_profile
```

4. Create the virtual environment while you specify the version of Python you wish to use. 
   The following command creates a virtualenv named 'venv' and uses the `-p` flag to specify the full path to the Python3 version you just installed:

```bash
virtualenv -p /home/username/opt/python-3.10.1/bin/python3 venv

Running virtualenv with interpreter /home/username/opt/python-3.10.1/bin/python3
Using base prefix '/home/username/opt/python-3.10.1'
New python executable in /home/username/example.com/env/bin/python3
Also creating executable in /home/username/example.com/env/bin/python
Installing setuptools, pip, wheel...done.
```

- This command creates a local copy of your environment specific to your project. 
  While working on the project, you should activate the local environment in order to make sure you're working with the right versions of your tools and packages.

> [!Attention]
> You may see the following error when installing: **setuptools pip failed with error code 1 error**
> If so, run the following: **[user@localhost]$ pip3 install --upgrade setuptools**
> Try again and you should be able to install without an error.

5.  To activate the new virtual environment, run the following:

```bash
source venv/bin/activate
```

_The name of the current virtual environment appears to the left of the prompt. For example:_

```bash
(venv) [server]$ 
```

6. To verify the correct Python version, run the following:

```bash
python -V
# Python 3.10.1
```

Any package that you install using pip is now placed in the virtual environments project folder, isolated from the global Python installation.

## Deactivating your virtualenv

When finished working in the virtual environment, you can deactivate it by running the following:

```
[server]$ deactivate
```

-   This puts you back into your Shell user's default settings.

## Deleting your virtual environment

To delete a virtual environment, simply delete the project folder. Using the previous example, run the following command:

```
[server]$ rm -rf venv
```

## Installing custom modules

View the following article for information on how to use pip to install Python modules.

-   [Using pip to install Python 3 modules](https://help.dreamhost.com/hc/en-us/articles/115000699011-Using-pip3-to-install-Python3-modules)

## Troubleshooting

### Errors creating a virtualenv

You may see the following errors when attempting to create a virtualenv using Python 3.7.

**AttributeError: module 'importlib.\_bootstrap' has no attribute 'SourceFileLoader'**

**OSError: Command /home/username/venv/bin/python3 -c "import sys, pip; sys...d\\"\] + sys.argv\[1:\]))" setuptools pip failed with error code 1**

Adding the following line when [installing a custom version of OpenSSL](https://help.dreamhost.com/hc/en-us/articles/360001435926-Installing-OpenSSL-locally-under-your-username) to your .bash\_profile resolves this.

```
export LC_ALL="en_US.UTF-8"
```

### Use the full path to your custom virtualenv

It's also possible that when you run the virtualenv command, it's using a version outside of your custom installation. Try running this instead to confirm the full path to your Python3 virtualenv.

```
[server]$ which virtualenv    
/home/username/opt/python-3.8.0/bin/virtualenv
```

This should respond with the version in your custom Python3 directory. You can then create a virtualenv using the full path like this:

```
[server]$ /home/username/opt/python-3.8.0/bin/virtualenv -p /home/username/opt/python-3.8.0/bin/python3 venv
```
