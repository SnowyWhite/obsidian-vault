# Overview

Here I want to create a quick cheatsheet of scripts I could use for basically any machine.
Grouping it by topic (web, crypto, reverse engineering, etc.) probably wouldn't be bad...

BTW: These maps very kindly provided by John Hammond! 😏

## Nmap

```bash
sudo nmap -v -sC -sV -oN nmap/initial <IP>
```

## Nikto

```bash
nikto -h "http://<DOMAIN>"
```

## Gobuster

```bash
gobuster dir -u http://<IP> -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt | tee gobuster.log
```
