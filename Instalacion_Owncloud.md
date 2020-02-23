### Intrucciones básicas para la instalación y configuración de Owncloud

```shell
apt update -y
apt install apache2 -y
apt install mysql-server -y
```

```shell
mysql -u root -p
```
```sql
CREATE DATABASE owncloud;
CREATE USER owncloud@localhost IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON owncloud.* TO owncloud@localhost;
flush privileges;
exit
```

```shell
cd /tmp && wget https://download.owncloud.org/community/owncloud-10.0.8.zip 
apt -y install unzip
unzip owncloud-10.0.8.zip
mkdir -p /var/www/html/owncloud && mv owncloud /var/www/html/owncloud
chown -R www-data:www-data /var/www/html/owncloud
chmod -R 755 /var/www/html/owncloud
service apache2 restart
```

```shell
vim /etc/apache2/sites-available/owncloud.conf
```

```html
Alias /owncloud "/var/www/html/owncloud/"

<Directory /var/www/html/owncloud/>
        Options +FollowSymlinks
        AllowOverride All

<IfModule mod_dav.c>
        Dav off
</IfModule>

SetEnv HOME /var/www/html/owncloud
SetEnv HTTP_HOME /var/www/html/owncloud
</Directory>
```

```shell
a2ensite owncloud.conf
service apache2 restart
a2enmod rewrite headers env dir mime
service apache2 restart
```

```shell
apt-get -y install libapache2-mod-php7.0 php7.0 php7.0-mysql php7.0-curl php7.0-gd php7.0-intl php-pear php-imagick php7.0-imap php7.0-mcrypt php-memcache  php7.0-pspell php7.0-recode php7.0-tidy php7.0-xmlrpc php7.0-xsl php7.0-mbstring php-gettext php7.0-zip
```

```shell
service apache2 restart
```

Acceder con un navegador a:
http://direccionip/owncloud/owncloud