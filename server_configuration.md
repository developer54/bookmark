## Debian 7 Server Configuration
LAMP stands for Linux, Apache, MySQL, and PHP (P can be replaced with Perl Or Python). I’m going to show you how to install a standard full-featured LAMP server on Debian 7 Wheezy system. Apache is the most popular web server in the world which more than 50% of web servers in the world are running it. I will use a fresh installed Debian 7 Wheezy Linux server for this article.
Update your Debian 7 system
Before installing anything to your system, make sure your Debian 7 system is update to date.

```
apt-get && apt-get upgrade -y
```

Say Yes or Y to install apache2 package and other extra required packages. After you installed apache2 and the extra packages, apache2 web server will start automatically for you.

### Enable mod_rewrite for Apache 2 on Debian
```
a2enmod rewrite
```

### Restart Apache2 to activate mod_rewrite
```
service apache2 restart
```

### Creating user and setting up Virtual Hosts
If you host multiple websites or have multiple users, you will have to setup separate Virtual Hosts or each user or website.

To add new user on Debian Linux (replace yourusername to whatever you like)
```
adduser yourusername
```

To set password for new user (you will be asked to type in your password twice)
```
passwd yourusername
```

Now create a directory to store your website files, lets call that directory public_html, and logs directory to store logs files
```
cd /home/yourusername
mkdir public_html
mkdir logs
```

The next step is to setup directories permission and owner to your public_html directory
```
chown yourusername:www-data /home/yourusername/public_html
chown yourusername:www-data /home/yourusername/logs
chmod 755 /home/yourusername
```

### Configure Name-based Virtual Hosts
If you host multiple websites or have multiple users, you will have to setup separate Virtual Hosts or each user or website. There is no limit how many Virtual Hosts you can create. In debian, Virtual Hosts files will be stored in /etc/apache2/sites-availables/ directory, you can seperate each virtual host files by domain or subdomain or however you want. Each virtual host file should be saved with .conf file extension.

For this article, I will use “fuji” as a linux username. All of my website files will be stored in /home/fuji/public_html directory. Let’s say we are going to setup yourdomain.com and yourdomain.net under fuji username. We are going to create yourdomain.com and yourdomain.net in /etc/apache2/sites-available/ directory.

### configure yourdomain.com VirtualHost
Creating yourdomain.com.conf file
```
nano /etc/apache2/sites-available/yourdomain.com
```
with content
```
<VirtualHost *:80>
ServerAdmin webmaster@yourdomain.com
ServerName yourdomain.com
ServerAlias yourdomain.com
DocumentRoot /home/fuji/public_html/yourdomain.com/
ErrorLog /home/fuji/logs/yourdomain.com.error.log
CustomLog /home/fuji/logs/yourdomain.com.access.log combined
<Directory /home/fuji/public_html/yourdomain.com/>
Options Indexes FollowSymLinks MultiViews
AllowOverride All
Order allow,deny
allow from all
</Directory>
</VirtualHost>
```

Creating yourdomain.net.conf file
```
nano /etc/apache2/sites-available/yourdomain.net
```

```
<VirtualHost *:80>
ServerAdmin webmaster@yourdomain.net
ServerName yourdomain.net
ServerAlias yourdomain.net
DocumentRoot /home/fuji/public_html/yourdomain.net/
ErrorLog /home/fuji/logs/yourdomain.net.error.log
CustomLog /home/fuji/logs/yourdomain.net.access.log combined
<Directory /home/fuji/public_html/yourdomain.net/>
Options Indexes FollowSymLinks MultiViews
AllowOverride All
Order allow,deny
allow from all
</Directory>
</VirtualHost>
```

### Enable or Disable an apache2 site / virtual host
After you have your virtualhost files configured correctly, it’s time to enable them by using a2ensite command. In this article I have yourdomain.com and yourdomain.net virtualhost files. We are going to host two separate domains with the same user, we need to create two separate directories for those two domains.

```
mkdir /home/fuji/public_html/yourdomain.com
mkdir /home/fuji/public_html/yourdomain.net
```

Now we can enable two virtualhosts for two domains
```
a2ensite yourdomain.com
a2ensite yourdomain.net
```

To activate the new configuration, you need to run:
```
service apache2 reload
```

In case you want to disable an apache2 site / virtual host, you can use a2dissite command. For example we have yourdomain.com.conf and yourdomain.net.conf, but we no longer need yourdomain.net.conf virtualhost on your Apache web server and we are going to disable yourdomain.net.conf
```
a2dissite yourdomain.net
service apache2 reload
```

### Install and Configure MySQL Database Server
MySQL is a very popular databse system which is very fast, reliable and easy to use. Many popular website rely on MySQL like Google, Facebook… Most open source PHP scripts like WordPress, Movable Type, Drupal, Joomla, Mambo use MySQL.

To install MySQL databse server on Debian
```
apt-get install mysql-server mysql-client
```

Unlike installing MySQL server on Centos, during the installation MySQL server on Debian, you will be asked to input MySQL root user password, but you should use mysql_secure_installation to make your MySQL server more secure (remove remote access, remove anonymous user and more).
```
mysql_secure_installation
```

### Install and Configuring PHP
PHP is a server scripting language, it can handle business logic with conditionals, loops, arrays and object. PHP is great when you are working with a database, you can store all informatioin in a database and use PHP program/scipt to fetch the information details from the datbase to display them in the user browser. You have apache we server installed which can handle html, and MySQL database server, to make PHP works in your web server and mysql, you have to install few PHP packages.
```
apt-get install php5 php-pear php5-mysql php5-dev libapache2-mod-php5 php5-dev php5-curl php5-gd php5-imagick php5-mcrypt
```

To confirm PHP is working, create a test php file in one of your domain
```
nano /home/fuji/public_html/yourdomain.com/info.php
```
with the content
```php	
<?php phpinfo(); ?>
```

### Install phpMyAdmin
phpMyAdmin is a free software to manage MySQL databases. Written in PHP, you can create, drop, import, export, optimize tables, repair tables, even run queries with phpMyAdmin.
```
apt-get install phpmyadmin
```
after that you can use phpmyadmin via http://yourdomain.com/phpmyadmin

### To install Perl on Debian 7 wheezy
```
apt-get install install perl libapache2-mod-perl2
```

### To install Python on Debian 7 wheezy
```
apt-get install python libapache2-mod-python
```



