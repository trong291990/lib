### Permission for nginx and linux user
sudo usermod -a -G www-data ubuntu
sudo chown -R ubuntu:www-data /var/www/dia_server
sudo find PROJECT_DIR -type f -exec chmod 664 {} \;    
sudo find PROJECT_DIR -type d -exec chmod 775 {} \;
sudo chgrp -R www-data storage bootstrap/cache
sudo chmod -R ug+rwx storage bootstrap/cache
