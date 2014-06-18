### Nginx Server Configuration
### Install Linux, nginx, MySQL, PHP on Debian 7
Update OS
```
sudo apt-get update
```

Install nginx
```
sudo apt-get install nginx
```

Install MySQL server
```
apt-get install mysql-server
```
Configure MySQL Server
```
mysql_install_db
```
Run security script for MySQL Server
```
mysql_secure_installation
```

Install PHP5(php5-fpm) for processing 
```
apt-get install php5-fpm php5-mysql
```

Configure PHP
```
nano /etc/php5/fpm/php.ini
```
What we are looking for in this file is the parameter that sets cgi.fix_pathinfo. This will be commented out with a semi-colon (;) and set to "1" by default.
This is an extremely insecure setting because it tells PHP to attempt to execute the closest file it can find if a PHP file does not match exactly. This basically would allow users to craft PHP requests in a way that would allow them to execute scripts that they shouldn't be allowed to execute.
We will change both of these conditions by uncommenting the line and setting it to "0" like this:

```
cgi.fix_pathinfo=0
```
Save and close the file when you are finished.
Now, we just need to restart our PHP processor by typing:
```
service php5-fpm restart
```

### Configure nginx to use PHP
```
nano /etc/nginx/sites-available/default
```

replace with


```
server {
    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /usr/share/nginx/html;
    index index.php index.html index.htm;

    server_name server_domain_name_or_IP;

    location / {
        try_files $uri $uri/ =404;
    }

    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
    }
}
```

To add Vhost
Just create
```
nano /etc/nginx/site-available/your_domain.com
```
edit nginx conf file
```
server {
    listen 80 default_server;
    listen [::]:80 default_server ipv6only=on;

    root /usr/share/nginx/html;
    index index.php index.html index.htm;

    server_name server_domain_name_or_IP;

    location / {
        try_files $uri $uri/ =404;
    }

    error_page 404 /404.html;
    error_page 500 502 503 504 /50x.html;
    location = /50x.html {
        root /usr/share/nginx/html;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
    }
}
```

then symlink to
```
ln -s /etc/nginx/site-available/your_domain.com /etc/nginx/site-enables
```

restart nginx
```
/etc/init.d/nginx restart
```

for sec reason, you can create new user for every domain
```
adduser your_user_name
```
then link your vhost to your user_name /home dir

### Installing mcrypt
```
apt-get install php5-mcrypt
```
restart php-fpm
```
/etc/init.d/php5-fpm restart
```

### Convert apache .htaccess to nginx conf file
[http://winginx.com/en/htaccess](http://winginx.com/en/htaccess)
