### How to configure PHP Phalcon Framework

Follow the guide from the installation home page. In case linux throw error package missing.

> curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | sudo bash  
> sudo apt-add-repository ppa:ondrej/php && sudo apt-get update  
> sudo apt-get install php7.0-phalcon

This should install the phalcon extension in `/usr/lib/php/20151012`


#### Manual compilation

The php dev extension is required

> git clone https://github.com/phalcon/cphalcon  
> sudo apt-get install php-dev libpcre3-dev gcc make  
> cd cphalcon/build  
> sudo ./install

Don't forget to activate extension and restart Apache.

> nano /etc/php/7.2/mods-available/phalcon.ini

    extension=phalcon.so
    
> phpenmod phalcon    
> service apache2 restart


#### Dev tool

Now the C-extension is ready. We need to generate a skeleton for the project.

This should be run as root and put in `/root`

    git clone git://github.com/phalcon/phalcon-devtools.git
    cd phalcon-devtools/
    . ./phalcon.sh
    ln -s ~/phalcon-devtools/phalcon.php /usr/bin/phalcon
    chmod ugo+x /usr/bin/phalcon

#### Apache configuration

    <VirtualHost *:80>
        ServerName myproject.com
        DocumentRoot /var/www/myproject/public

        <Directory "/var/www/myproject/public">
           Options       All
           AllowOverride All
           Require       all granted
        </Directory>
    </VirtualHost>


Setup [.htaccess](https://docs.phalconphp.com/en/3.2/webserver-setup)


Start a new project

> phalcon create-project test
