When you have only one domain but want to use for both Frontend and Backend

``` 
server {

    listen 80;
    listen [::]:80;

    server_name typhlo.local;
    root /var/www/sites/typhlo/frontend/public;
    index  index.html index.htm;

    error_log /var/www/sites/typhlo/api/storage/logs/nginx.error.log;

    client_max_body_size 0;
    
    location ^~ /backend {
         alias /var/www/sites/typhlo/backend/public;
         index index.php;
         try_files $uri $uri/ @backend;
         location ~ \.php$ {
            #fastcgi_split_path_info ^(.+?\.php)(/.*)?$;
            fastcgi_pass unix:/run/php/php7.4-fpm.sock;
            fastcgi_index index.php;
            include fastcgi_params;
            fastcgi_param SCRIPT_FILENAME $request_filename;
        }
    }

    location @backend {
        rewrite /backend/(.*)$ /backend/index.php?/$1 last;
    }
    
}
```
