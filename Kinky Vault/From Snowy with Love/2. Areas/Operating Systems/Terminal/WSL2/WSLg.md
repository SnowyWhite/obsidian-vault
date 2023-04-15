## Install Gedit

Gedit is the default text editor of the GNOME desktop environment.

```bash
sudo apt install gedit -y
```

To launch your bashrc file in the editor, enter: `gedit ~/.bashrc`

## Install GIMP

GIMP is a free and open-source raster graphics editor used for image manipulation and image editing, free-form drawing, transcoding between different image file formats, and more specialized tasks.

```bash
sudo apt install gimp -y
```

To launch, enter: `gimp`

## Install Nautilus

Nautilus, also known as GNOME Files, is the file manager for the GNOME desktop. (Similar to Windows File Explorer).

```bash
sudo apt install nautilus -y
```

To launch, enter: `nautilus`

## Install VLC

VLC is a free and open source cross-platform multimedia player and framework that plays most multimedia files.

```bash
sudo apt install vlc -y
```

To launch, enter: `vlc`

## Install X11 apps

X11 is the Linux windowing system and this is a miscellaneous collection of apps and tools that ship with it, such as the xclock, xcalc calculator, xclipboard for cut and paste, xev for event testing, etc. See the [x.org docs](https://www.x.org/wiki/UserDocumentation/GettingStarted/) for more info.

```bash
sudo apt install x11-apps -y
```

To launch, enter the name of the tool you would like to use. For example:

-   `xcalc`, `xclock`, `xeyes`

## Install Google Chrome for Linux

To install the Google Chrome for Linux:

1.  Change directories into the temp folder: `cd /tmp`
2.  Use wget to download it: `sudo wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb`
3.  Get the current stable version: `sudo dpkg -i google-chrome-stable_current_amd64.deb`
4.  Fix the package: `sudo apt install --fix-broken -y`
5.  Configure the package: `sudo dpkg -i google-chrome-stable_current_amd64.deb`

To launch, enter: `google-chrome`