# Commands
Crawl site aggressively
```bash
katana -u https://tesla.com -d 5 -jc -c 20 -p 20 -hl -kf all -v -output katana_urls.txt
# Remove nonsense from output file ([Img] https://)
sed 's/.*\[.*\]\s*//' katana_urls.txt > urls.txt   
```
