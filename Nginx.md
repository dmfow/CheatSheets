
#### Basic config
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

#### Reload (eg after confgi changes)
```
sudo nginx -s reload

# Stopping
nginx -s quit
nginx -s stop

```







## Installation


#### Installation
```
sudo apt install nginx
```
## Let's encrypt Certbot

#### Manual
```
# You get a TXT record to paste into your DNS zone
certbot -d domain.org --manual --preferred-challenges dns certonly
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

#### Some SSL parameters (choose carefully, probably not below)
Evaluate <br>
https://geekflare.com/nginx-webserver-security-hardening-guide/
```
```
