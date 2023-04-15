# Check Installation
```python
# Python 2
python --version
# Python 3
python3 --version
```

# Launch Python
```python
# Launch Python 2 interpreter
python
# Launch Python 3 interpreter
python3
```

# Additional Packages
The most important packages are `pipenv` and `pip`.
Python2.7.9 and later and Python3.4 and later include pip by default.

## pip
To see if pip is installed, run this:
```shell
command -v pip
```
On some distributions, the `pip` command is meant for Python 2, while `pip3` is meant for Python 3:
```shell
command -v pip3
```

## pipenv
Use `pip` to install pipenv:
```shell
pip install --user pipenv
```

This does a user installation to prevent breaking any system-wide packages. 
If `pipenv` isn’t available in your shell after installation, you’ll need to add the user base‘s binary directory to your `PATH`.
On Linux and macOS you can find the user base binary directory by running `python -m site --user-base` and adding `bin` to the end. 
For example, this will typically print `~/.local` (with `~` expanded to the absolute path to your home directory) so you’ll need to add `~/.local/bin` to your `PATH`. 
You can set your `PATH` permanently by [modifying ~/.profile](https://stackoverflow.com/a/14638025).

# Installing packages for your project
Pipenv manages dependencies on a per-project basis. 
To install packages, change into your project’s directory (or just an empty directory for this tutorial) and run:

```bash
cd myproject
pipenv install requests
```

Pipenv will install the excellent [Requests](https://python-requests.org) library and create a `Pipfile` for you in your project’s directory. 
The [Pipfile](https://github.com/pypa/pipfile) is used to track which dependencies your project needs in case you need to re-install them, such as when you share your project with others.

## Using installed packages
NOw that Requests is installed you can create a simple `main.py` file to use it:
```python
import requests
response = requests.get('https://httpbin.org/ip')
print('Your IP is {0}'.format(response.json()['origin']))
```

Then you can run this script using `pipenv run`:
```shell
pipenv run python main.py
```

You should get output similar to this:
```Your IP is 8.8.8.8```

Using `$ pipenv run` ensures that your installed packages are available to your script. 
It’s also possible to spawn a new shell that ensures all commands have access to your installed packages with `$ pipenv shell`.