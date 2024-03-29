## Server
Loadbalancer below

#### Basic server config
```
server {
    listen 80;
    server_name example.org www.example.org;
    
    location / {
        root /data/www;
    }

    location /images/ {
        root /data/images;
    }
}

server {
    listen 443 ssl;
    server_name example2.org www.example2.org;
    
    ssl_certificate /etc/letsencrypt/live/domainname.com/fullchain.pem
    ssl_certificate_key /etc/letsencrypt/live/domainname.com/privkey.pem


    location / {
        root /data/www;
    }

}

```

#### Symlink from site-available conf to site-enabled conf (otherwise it won't work)
```
ln -s /etc/nginx/sites-available/yourdomain.org.conf /etc/nginx/sites-enabled/yourdomain.org.conf
```

#### Reload (eg after config changes)
```
sudo nginx -s reload

# Stopping
nginx -s quit
nginx -s stop

```


## Loadblancer

#### Basic config

```
http {
  upstream www {
        server 10.0.0.100:80 weight=3;
        #server 127.0.0.1:8001;
        #server 127.0.0.1:8002;
        #server 127.0.0.1:8003;
  }

  server {
        listen 443 ssl;
        server_name *.yourdomain.org;

        ssl_certificate /etc/letsencrypt/live/yourdomain.org/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/yourdomain.org/privkey.pem;
        location / {
                proxy_pass http://www;

                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
  }
}
```


#### Set the original IP when offloading ssl
```
proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

# Other commands
proxy_set_header Host $nginx;

```


## Let's encrypt Certbot

#### Manual
You get a TXT record to paste into your DNS zone
```
# both wildcard and root
certbot -d domain.org -d *.domain.org --manual --preferred-challenges dns certonly

# Only one domain (eg root)
certbot -d domain.org --manual --preferred-challenges dns certonly
# only wildcard
certbot -d *.domain.org --manual --preferred-challenges dns certonly
```

#### Manual renewal
```
# Check certs
sudo certbot certificates
# Go to your home library (or maybe anywhere), and run the same command as when creating the cert
certbot -d domain.org -d *.domain.org  --manual --preferred-challenges dns certonly
```


#### Check your TXT field
```
dig TXT _acme-challenge.yourdomain.org +short
```


#### Automatic
```
sudo apt install certbot
sudo apt install python3-certbot-nginx
sudo certbot --nginx -d domain.org -d www.domain.org

```


#### Some SSL parameters (choose carefully, probably not below)
```
server {
    ...
    ssl_session_cache shared:SSL:20m;
    ssl_session_timeout 10m;
	
    ssl_prefer_server_ciphers       on;
    ssl_protocols                   TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers                     ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5:!DSS;
	
    add_header Strict-Transport-Security "max-age=31536000";
    
    ...
}

```


## PHP

```
location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php-fpm.sock;
}
# OR maybe (not tested)
location ~ \.php$ {
  fastcgi_split_path_info ^(.+\.php)(/.+)$;
  fastcgi_pass 127.0.0.1:9000;
  fastcgi_index index.php;
  include fastcgi_params;
}

```

#### Allow larger uploads (eg POST), with php
Config all 3:
- Nginx
- php
- permission on the upload foled
Then do
sudo nginx -s reload
```
# Nginx (/etc/nginx/sites-availible/XYZ.conf)
# in http, server or location (0 unrestricted)
client_max_body_size 48M;
client_max_body_size 0;

# php (/etc/php/X.X/fpm/php.ini)
  # Filesize
  upload_max_filesize = 1G
  post_max_size = 1G
  memory_limit = 128M

  # php time restrictions
  max_input_time = 1800
  max_execution_time = 30

# permission to a folder for uploads
# check which user is used for the nginx
ps aux | grep -E '[a]pache|[h]ttpd|[_]www|[w]ww-data|[n]ginx' | grep -v root | head -1 | cut -d\  -f1
# Set persmission
chown -R www-data:www-data /yourfolder/
chmod -R g+rw /yourolder/
  # to the group (g), add (+) read and write (rw) permissions on folder your/folder/, recursively (-R)
```


## Installation


#### Installation
```
sudo apt install nginx

# Default web library
/var/www/html

```


#### Installation PHP
```
sudo apt install php-fpm
# Maybe
sudo apt install php-cli
reboot
# Check status
systemctl status php*-fpm.service
ls /run/php

# conf files not needed to be update
/etc/nginx/php_fastcgi.conf
/etc/php/*/fpm/pool.d/www.conf
ls /run/php/

/etc/nginx/nginx.conf
/etc/nginx/sites-available/
/etc/nginx/sites-enabled/
/etc/nginx/snippets

```


#### Security
Evaluate <br>
<br>
https://geekflare.com/nginx-webserver-security-hardening-guide/
<br>
https://geekflare.com/nginx-production-configuration/
```
```

#### Config pitfalls
Evaluate
<br>
https://www.nginx.com/resources/wiki/start/topics/tutorials/config_pitfalls/
<br>
https://www.nginx.com/blog/avoiding-top-10-nginx-configuration-mistakes/
```
```

#### Config info and such
```
# Where is the config file
nginx -V 2>&1 | grep -o '\-\-conf-path=\(.*conf\)' | cut -d '=' -f2
# OR (not tested)
ps aux | grep "[c]onf" | awk '{print $(NF)}' /app/nginx.conf

# Check if compiled with a module
nginx -V 2>&1 | egrep --color -o 'http_realip_module'
nginx -V 2>&1 | egrep --color -o 'realip_module' 

# Show the config file
nginx -T

# Dump the config from memory
# https://serverfault.com/questions/361421/dump-nginx-config-from-running-process
# and https://serverfault.com/questions/361421/dump-nginx-config-from-running-process/1090838#1090838
# Set pid of nginx master process here
pid=8192
# generate gdb commands from the process's memory mappings using awk
cat /proc/$pid/maps | awk '$6 !~ "^/" {split ($1,addrs,"-"); print "dump memory mem_" addrs[1] " 0x" addrs[1] " 0x" addrs[2] ;}END{print "quit"}' > gdb-commands
# use gdb with the -x option to dump these memory regions to mem_* files
gdb -p $pid -x gdb-commands
# look for some (any) nginx.conf text
grep worker_connections mem_*
grep server_name mem_*
# You should get something like "Binary file mem_086cb000 matches". Open this file in editor, search for config (e.g. "worker_connections" directive), copy&paste.

```


## Check headers through tcpdump

#### tcpdump to console
```
# Check available interfaces
tcpdump -D
# Do the dump (c limits the number of packets, without c it continues till ctrl break)
sudo tcpdump -i ens0 -c 30 -vv -nl

```
#### Other tcpdump commands
```
sudo tcpdump src 172.18.10.105 && -n port 80 -c 5
sudo tcpdump dst 172.9.1.10
```



## Not working yet

#### Write headers to a file
```
# save to file
client_body_in_file_only on;

# where to store them
client_body_temp_path /tmp/nginx_rbf; 
# OR
client_body_temp_path temp 1 2 4;

# don't save these adresses
set_real_ip_from 192.168.0.0/24;


```

