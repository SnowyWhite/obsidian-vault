Follow these steps to change the hostname:

1. Add or edit the file `/etc/wsl.conf` with following content:

```bash
[network]
hostname = HOST
generateHosts = false
```

2. Change the all occurence of the old hostname in the file `/etc/hosts`.
3. Then log out and wait for ~8 seconds for WSL to reboot
4. Or just type `wsl --shutdown` and then start it again
