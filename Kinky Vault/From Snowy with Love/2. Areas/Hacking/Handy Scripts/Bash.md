# Find Subdomains 
#amass #subfinder #script
```bash
#!/bin/bash

if [ $# -eq 0 ]
  then
    echo "Usage: ./subdomains.sh domain.com [e.g. tesla.com]"
    exit 1
fi

CYAN='\033[0;36m' 
NC='\033[0m'    # No Color

printf "Running ${CYAN}amass${NC}...\n"
amass enum --passive -d $1 -o assetfinder_$1
printf "Running ${CYAN}assetfinder${NC}...\n"
assetfinder --subs-only $1 | tee -a assetfinder_$1

printf "Running ${CYAN}subfinder${NC}...\n"
subfinder -d $1 -o subfinder_$1
cat subfinder_$1 | tee -a found_domains_$1

printf "Filtering out alive ${CYAN}subdomains${NC}...\n"
# Filtering the domains
sort -u found_domains_$1 -o found_domains_$1
cat found_domains_$1 | filter-resolved | tee -a subdomains_$1.txt
```

## Tools

- https://github.com/OWASP/Amass
- https://github.com/projectdiscovery/subfinder
- https://github.com/tomnomnom/hacks/tree/master/filter-resolved
- https://github.com/tomnomnom/hacks/tree/master/assetfinder


# Find SQL injections
#subfinder #httpx #sqlmap
```bash
#!/bin/bash
# $1 => example.domain

if [ $# -eq 0 ]
  then
    echo "Usage: ./sqli.sh domain.com [e.g. tesla.com]"
    exit 1
fi

CYAN='\033[0;36m'
NC='\033[0m'    # No Color

printf "Running ${CYAN}subfinder${NC}...\n"
subfinder -d $1 | tee -a domains_$1

printf "Checking with ${CYAN}httpx${NC}...\n"
cat domains_$1 | httpx | tee -a alive_$1

printf "Scanning with ${CYAN}waybackurls${NC}...\n"
cat alive_$1 | waybackurls | tee -a urls_$1

printf "Preparing ${CYAN}urls${NC}...\n"
gf sqli urls_$1 >> sqli_$1
printf "Running ${CYAN}sqlmap${NC}...\n"
sqlmap -m sqli_$1 --dbs --batch
```

## Tools

- https://github.com/projectdiscovery/subfinder 
	`go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest`
- https://github.com/projectdiscovery/httpx 
	`go install -v github.com/projectdiscovery/httpx/cmd/httpx@latest`
- https://github.com/tomnomnom/hacks/waybackurls 
	`go install -v github.com/tomnomnom/hacks/waybackurls@latest`
- https://github.com/tomnomnom/gf 
	`go install -v github.com/tomnomnom/gf@latest`

## Installation
When `gf` is installed:
```bash
mkdir ~/.gf
cp -r ~/go/pkg/mod/github.com/tomnomnom/gf@v0.0.0-20200618134122-dcd4c361f9f5/examples/ ~/.gf
git clone https://github.com/1ndianl33t/Gf-Patterns
mv Gf-Patterns/*.json ~/.gf
```

# Generate custom wordlist from domain

```bash
#!/bin/bash
# Create a custom wordlist from any domain

echo "bugcrowd.com" | subfinder -silent | hakrawler -plain -usewayback -scope yolo | sed $'s/[:./?=:]/\\\n/g' | anew
```

## Tools for the script

- https://github.com/hakluke/hakrawler
	`go install github.com/hakluke/hakrawler@latest`
 - https://github.com/tomnomnom/anew
	 `go install -v github.com/tomnomnom/anew@latest`


# Install Tools

```bash
#!/bin/bash
# Installs common tools

# Fancy colors
CYAN='\033[0;36m'
NC='\033[0m'    # No Color

# List of all tools to install
TOOLS=(
github.com/projectdiscovery/subfinder/v2/cmd/subfinder
github.com/projectdiscovery/httpx/cmd/httpx
github.com/tomnomnom/hacks/waybackurls
github.com/tomnomnom/hacks/filter-resolved
github.com/tomnomnom/gf
)

apt-get install amass

# Log file to record the script activity
LOG_FILE=/var/log/toolinstaller.log

# Check if each tool is already installed and install otherwise
if command -v "$(basename "amass")" &> /dev/null; then
echo "${CYAN}amass${NC} is already installed, skipping..." | tee -a "$LOG_FILE"

echo "Installing ${CYAN}amass${NC}..." | tee -a "$LOG_FILE"
apt install amass

for tool in "${TOOLS[@]}"; do
if command -v "$(basename "$tool")" &> /dev/null; then
echo "${CYAN}$tool${NC} is already installed, skipping..." | tee -a "$LOG_FILE"
else
echo "Installing ${CYAN}$tool${NC}..." | tee -a "$LOG_FILE"
go install -v "$tool@latest" 2>&1 | tee -a "$LOG_FILE"
if [ $? -eq 0 ]; then
echo "Successfully installed ${CYAN}$tool${NC}" | tee -a "$LOG_FILE"
if [$tool -eq "github.com/tomnomnom/gf" ]; then
echo "Creating directory for ${CYAN}$tool${NC} and moving example patterns there..." | tee -a "$LOG_FILE"
mkdir ~/.gf
cp -r ~/go/pkg/mod/github.com/tomnomnom/gf@v0.0.0-20200618134122-dcd4c361f9f5/examples/ ~/.gf

echo "Clone ${CYAN}github.com/1ndianl335/Gf-Patterns${NC} for additional patterns..." | tee -a "$LOG_FILE"
git clone https://github.com/1ndianl33t/Gf-Patterns
mv Gf-Patterns/*.json ~/.gf

else
echo "Error while installing ${CYAN}$tool${NC}" | tee -a "$LOG_FILE"
fi
fi
done
```