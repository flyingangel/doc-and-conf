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

    <VirtualHost dev.project.com>
        ServerName dev.project.com
        DocumentRoot /var/www/dev.project.com
    </VirtualHost>

This is the minimal configuration, without security.

Enable site

> a2ensite dev.project.conf

Reload apache

> /etc/init.d/apache2 reload
