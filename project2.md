# Documentation for Project 2 (LEMP)

## Install Apache and updating firewall:

`sudo apt update`

`sudo apt install apache2`

`sudo systemctl status apache2`

![apache status](./images/apache-status.png)

Updating Firewall 

![firewall](./images/inbound-rules.png)

Default Page

![default page](./images/apache-default-page.png)

## Installing MYSQL:

`sudo apt install mysql-server`

`sudo mysql`

![mysql status](./images/mysql-status.png)

`sudo mysql_secure_installation`

`sudo mysql -p`

![mysql password](./images/sql-password.png)

## Installing PHP

`sudo apt install php libapache2-mod-php php-mysql`

`php -v`

![php version](./images/php-version.png)

## Creating a virtual host

`sudo mkdir /var/www/projectlamp`

`sudo chown -R $USER:$USER /var/www/projectlamp`

`sudo vi /etc/apache2/sites-available/projectlamp.conf`

Config file:

`<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>`

`sudo ls /etc/apache2/sites-available`

![sites dir](./images/config-file.png)

`sudo a2ensite projectlamp`

`sudo a2dissite 000-default`

`sudo apache2ctl configtest`

`sudo systemctl reload apache2`

`sudo echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

![index page](./images/index-page.png)

## Enable PHP on website

`sudo vim /etc/apache2/mods-enabled/dir.conf`

`<IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>`

`sudo systemctl reload apache2`

`vim /var/www/projectlamp/index.php`

`<?php
phpinfo();`

![index.php](./images/index-php.png)

`sudo rm /var/www/projectlamp/index.php`




