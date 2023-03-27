
#### Basic config
```

server {

    listen 80;
    server_name example.org www.example.org;
    
    location / {
        root /data/www;
    }

    location /images/ {
        root /data;
    }
}

server {

    listen 443;
    server_name example2.org www.example2.org;
    
    location / {
        root /data/www;
    }

    location /images/ {
        root /data;
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


