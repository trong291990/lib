Basic nginx site configuration

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
}
```
