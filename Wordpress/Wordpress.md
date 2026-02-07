# Update system
```
sudo apt update
sudo apt upgrade -y
```
# Install Apache
```
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

# Install MySQL
```
sudo apt install mysql-server -y
sudo mysql_secure_installation
```
# Install PHP
```
sudo apt install php libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip -y
```
# Setup MySQL
```
sudo mysql -u root -p

CREATE DATABASE wordpress_db;
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'كلمة_مرور_قوية';
GRANT ALL PRIVILEGES ON wordpress_db.* TO 'wordpress_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```
# Install Wordpress
```
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xzvf latest.tar.gz
sudo mv wordpress /var/www/html/
```
# Setup Permissions 
```
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo chmod -R 755 /var/www/html/wordpress
```
# Setup Wordpress
```
cd /var/www/html/wordpress
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php
define('DB_NAME', 'wordpress_db');
define('DB_USER', 'wordpress_user');
define('DB_PASSWORD', 'كلمة_المرور_التي_أنشأتها');
define('DB_HOST', 'localhost');
```
# Setup Apache
```
sudo nano /etc/apache2/sites-available/wordpress.conf
<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/wordpress
    ServerName example.com
    Redirect permanent / https:/exsample.com/
    <Directory /var/www/html/wordpress>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```
# Setup Firewall
```
sudo ufw allow 'Apache Full'
sudo ufw enable
```

# Install SSL
```
sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache -d example.com
sudo certbot renew --dry-run
```

# Setup PHP
```
sudo nano /etc/php/8.1/apache2/php.ini
upload_max_filesize = 64M
post_max_size = 64M
sudo systemctl restart ap
```
