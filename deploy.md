# Configure

[Secure Nginx with Let's Encrypt](https://linuxize.com/post/secure-nginx-with-let-s-encrypt-on-ubuntu-20-04/)

```
$ sudo openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
$ sudo mkdir -p /var/lib/letsencrypt/.well-known
$ sudo chgrp www-data /var/lib/letsencrypt
$ sudo chmod g+s /var/lib/letsencrypt
$ sudo vi /etc/nginx/snippets/letsencrypt.conf

```


終於在這篇
https://www.odoo.com/forum/help-1/what-does-config-setting-proxy-mode-do-14164
看到 Nginx 設定檔內容 location 段落有一串 proxy_ 開頭的設定值是自己缺少的

# Backup Script

```
#!/bin/bash

BACKUP_DIR=~/backup
ODOO_DATABASE=mydb
MASTER_PASS=mypass

mkdir -p ${BACKUP_DIR}

curl -X POST \
        -F "master_pwd=${MASTER_PASS}" \
        -F "name=${ODOO_DATABASE}" \
        -F "backup_format=zip" \
        -o ${BACKUP_DIR}/${ODOO_DATABASE}-$(date +%F).zip \
        http://localhost:8069/web/database/backup

# MASTER_PASS can be copied from /etc/odoo-server.conf
# date +%Y_%m%d_%H%M
# find ${BACKUP_DIR} -type f -mtime +14 -name "${ODOO_DATABASE}-*.zip" -delete
```

