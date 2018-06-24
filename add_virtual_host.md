### Add a virtual host

Note: All the steps require `sudo su` access

Edit host file to point the website to our localhost

> nano /etc/hosts

Add line

> 127.0.0.1	dev.project.com

Add project if not exist

> mkdir /var/www/dev.project.com

Create a virtual host conf

> nano /etc/apache2/sites-available/dev.project.conf

    <VirtualHost *:80>
        ServerName dev.project.com
        DocumentRoot /var/www/dev.project.com
        
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        
        #allow .htaccess override
        <Directory "/var/www/dev.project.com">
            AllowOverride All
        </Directory>
    </VirtualHost>

This is the minimal configuration, without security.

Enable site

> a2ensite dev.project.conf

Reload apache

> /etc/init.d/apache2 reload
