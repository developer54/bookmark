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
