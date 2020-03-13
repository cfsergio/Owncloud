# Instrucciones básicas para la instalación y configuración de Owncloud

**Primer bloque de ejecución.**
```shell
apt update -y
apt install apache2 -y
apt install mysql-server -y
```

***

**Segundo bloque de ejecución.**
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

***

**Tercer bloque de ejecución.**
```shell
cd /tmp && wget https://download.owncloud.org/community/owncloud-10.0.8.zip 
apt -y install unzip
unzip owncloud-10.0.8.zip
mkdir -p /var/www/html/owncloud && mv owncloud /var/www/html/owncloud
chown -R www-data:www-data /var/www/html/owncloud
chmod -R 755 /var/www/html/owncloud
service apache2 restart
```

***

**Cuarto bloque de ejecución.**
```shell
vim /etc/apache2/sites-available/owncloud.conf
```

```vim
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

***

**Quinto bloque de ejecución.**
```shell
a2ensite owncloud.conf
service apache2 restart
a2enmod rewrite headers env dir mime
service apache2 restart
```

***

**Sexto bloque de ejecución.**
```shell
apt-get -y install libapache2-mod-php7.0 php7.0 php7.0-mysql php7.0-curl php7.0-gd php7.0-intl php-pear php-imagick php7.0-imap php7.0-mcrypt php-memcache  php7.0-pspell php7.0-recode php7.0-tidy php7.0-xmlrpc php7.0-xsl php7.0-mbstring php-gettext php7.0-zip
```

***

**Séptimo bloque de ejecución.**
```shell
service apache2 restart
```

***

**Paso final.** 
Acceder con un navegador a la siguiente dirección [http://direccionip/owncloud/owncloud](http://direccionip/owncloud/owncloud)
