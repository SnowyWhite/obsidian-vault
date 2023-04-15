# Extract URLs from junk data
```js
cat file | grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*"*
# Example
curl http://host.xx/file.js | grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*"*
```

# Find unauthorized API Endpoints
This one-liner runs a series of subdomain discovery and analysis tools (`katana`, `subjs`, `python3 /opt/JSA/jsa.py`, and `goverview`) and then sorts and filters the output to return a list of unique subdomains. The final output is a list of subdomains, with each subdomain on a separate line.

```bash
katana -u $url -hl -nos -jc -silent -aff -kf all,robotstxt,sitemapxml -c 150 -fs fqdn | subjs | python3 /opt/JSA/jsa.py | goverview probe -N -c 500 | sort -u -t';' -k2,14 | cut -d ';' -f1
```

## Description
1. It runs the `katana` tool with several options: (https://github.com/projectdiscovery/katana)
-   `-u $url` specifies the URL to scan. The value of `$url` is a variable that is expected to be defined elsewhere in the script.
-   `-hl` enables host-level scans
-   `-nos` disables screenshotting
-   `-jc` enables JavaScript analysis
-   `-silent` runs the tool in silent mode, without producing any output to the console
-   `-aff` enables directory traversal
-   `-kf all,robotstxt,sitemapxml` specifies the files to look for during the scan
-   `-c 150` sets the concurrency level to 150
-   `-fs fqdn` specifies that the output should include only the fully qualified domain names

2.  `| subjs` (https://github.com/lc/subjs)
The output of the `katana` command is piped to the `subjs` tool. 
`subjs` is a subdomain discovery tool that uses various search engines and web archives to find subdomains.

3.  `| python3 /opt/JSA/jsa.py` (https://github.com/w9w/JSA)
The output of `subjs` is piped to `python3 /opt/JSA/jsa.py`. 
This script is likely a custom script that takes the output of `subjs` and performs some additional processing on it.

4.  `| goverview probe -N -c 500` (https://github.com/j3ssie/goverview)
The output of the Python script is piped to `goverview probe -N -c 500`. `goverview` is a tool for subdomain enumeration and takeover analysis. 
This command instructs `goverview` to probe the discovered subdomains, with a maximum concurrency level of 500.

5.  `| sort -u -t';' -k2,14`
The output of `goverview` is piped to `sort`, which is instructed to sort the output in ascending order (`-u` option ensures only unique values are returned). 
The `-t';'` option specifies that the fields are separated by a semicolon (;) character, and `-k2,14` specifies that the sorting should be done based on fields 2 to 14 (inclusive).

6.  `| cut -d ';' -f1`
The final command in the pipeline is `cut`, which is instructed to cut the output based on the semicolon delimiter (`-d ';'`) and return only the first field (`-f1`).