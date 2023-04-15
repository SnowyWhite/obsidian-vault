## Search for file by name

### Description
This command lists the names of all files starting with `dumpbin` in the `c:\` directory and its subdirectories, in bare format.

```powershell
Get-ChildItem -Path c:\dumpbin* -Recurse -File | Select-Object -ExpandProperty FullName
```
  
### Explanation
- `Get-ChildItem`: Equivalent of `dir` in PowerShell.
- `-Path c:\dumpbin*`: Specifies the path to search for files. The `*` wildcard character matches any sequence of characters, just like in the `cmd` command.
- `-Recurse`: Specifies that the search should be done recursively in subdirectories.
- `-File`: Specifies that only files should be listed.
- `Select-Object -ExpandProperty FullName`: Selects the full name of each file. 
  The `-ExpandProperty` option is used to expand the value of the `FullName` property, which is an array, into a list of strings.

### See also
[[Useful CMD Commands#Search for file by name | CMD Version]]


