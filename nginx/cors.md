CORS configuration

``` 
server {

    listen 80;
    listen [::]:80;

    server_name api.typhlo.local;
    root /var/www/sites/typhlo/api/public;
    index index.php index.html index.htm;

    error_log /var/www/sites/typhlo/api/storage/logs/nginx.error.log;

    client_max_body_size 0;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ [^/]\.php(/|$) {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.4-fpm.sock;
    }
    
    add_header 'Access-Control-Allow-Origin' "*" always;
    add_header 'Access-Control-Max-Age' 259200; # allows preflight request for 3 days
    add_header 'Access-Control-Allow-Credentials' 'true' always;
    add_header 'Access-Control-Allow-Methods' 'GET, POST, PUT, DELETE, OPTIONS' always;
    add_header 'Access-Control-Allow-Headers' 'X-Signature,Accept,Authorization,Cache-Control,Content-Type,DNT,If-Modified-Since,Keep-Alive,Origin,User-Agent,X-Requested-With,Language' always;
    add_header 'Access-Control-Expose-Headers' 'Authorization'  always;
}
```
