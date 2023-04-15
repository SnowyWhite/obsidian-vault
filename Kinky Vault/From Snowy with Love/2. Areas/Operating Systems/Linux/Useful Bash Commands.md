
## Add path to $PATH

```bash
export PATH=$PATH:<new>
```

## Get hardware info

There are several commands you can use to get information about the hardware on a Linux system. 
Here are some of the most commonly used ones:

**lscpu:** This command displays information about the CPU architecture, including the number of CPUs, sockets, cores, and threads.
  
**lshw:** This command provides detailed information about the system's hardware components, including the processor, memory, storage devices, and network interfaces.

**dmidecode:** This command reads the system DMI (Desktop Management Interface) table and provides information about the system's hardware components, including the processor, memory, and BIOS.
   
**hdparm:** This command is used to get information about hard disk drives and can be used to display the disk's parameters, such as its transfer mode, buffer size, and average seek time.

**lsblk:** This command displays information about the system's block devices, including their name, size, type, and whether they are mounted or not.

## Change keyboard layout

Enter the following command: 

```bash
sudo dpkg-reconfigure keyboard-configuration
```

The `configuring keyboard-configuration` selection screen will pop up with different keyboard models. 
Use the arrow-keys to select the layout of your choice and press **Enter** to make your selection.

To complete the process enter the command: 

```bash
sudo service keyboard-setup restart
```

The new keyboard layout will be used after a reboot.

## Increase the System Swap Size

```bash
sudo /etc/init.d/dphys-swapfile stop  
sudo nano /etc/dphys-swapfile  
CONF_SWAPSIZE=2048
sudo /etc/init.d/dphys-swapfile start
```

## Extract rows from CSV file

```bash
cut -d',' -f2 input.csv > output.txt # extracts the second rows
```

