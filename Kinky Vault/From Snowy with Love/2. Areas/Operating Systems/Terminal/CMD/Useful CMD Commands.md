## Append path to $PATH

```bash
setx path "%PATH%;C:\Python310"
```


## Search for file by name

### Description
This command lists the names of all files starting with `dumpbin` in the `c:\` directory and its subdirectories, in bare format.

```bash
cmd /C dir /s/b c:\dumpbin*
```

### Explanation

- `cmd /C`: Runs the `dir` command and then terminates the `cmd` process.    
- `dir`: Lists the files and directories in a directory.    
- `/s`: Searches for files in the current directory and all subdirectories.    
- `/b`: Uses bare format (no heading information or summary).    
- `c:\dumpbin*`: The search pattern for the files to be listed. The `*` wildcard character matches any sequence of characters. 
   In this case, the command will search for files with names starting with `dumpbin` in the `c:\` directory and its subdirectories. 

### See also
[[Useful Powershell Commands#Search for file by name | Powershell Version ]] 