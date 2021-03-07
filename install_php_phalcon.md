# How to configure PHP Phalcon Framework

This follow the online guide of version 4 of the [Fhalcon Framework](https://docs.phalcon.io/4.0/en/installation)

## Requirements

> For this guide we'll use PHP 7.3. For default latest PHP, use without a prefix version i.e. `php-xxx`.

    sudo apt install build-essential gcc make automake autoconf
    sudo apt install libpcre3-dev php7.3-dev php7.3-common php7.3-gettext php7.3-json php7.3-mbstring php7.3-psr

More info on the [PSR extension](https://github.com/jbboehr/php-psr.git).

## Install Phalcon extension

    curl -s https://packagecloud.io/install/repositories/phalcon/stable/script.deb.sh | sudo bash
    sudo apt install php7.3-phalcon
    systemctl restart php7.3-fpm

The Phalcon Framework is now ready to use.

> You can check for installed extension in: /usr/lib/php/20180731/

> For optimized machine code, see the [compilation guide](https://docs.phalcon.io/4.0/en/installation#compilation)

## Create a bare project

We can generate a skeleton for the project using an external project called [Phalcon DevTools](https://github.com/phalcon/phalcon-devtools.git).

    composer global require --dev phalcon/devtools
    sudo ln -s ~/.config/composer/vendor/bin/phalcon /usr/local/bin/
    phalcon create-project myproject --type=[cli|micro|simple|modules]

The easiest way to test is to use the PHP built-in server

    cd myproject
    php -S localhost:8000 -t public .htrouter.php

## Setup Nginx

If we want to test like a real site, we must use nginx virtual host.

    cat <<'EOF' >> /etc/nginx/sites-available/myproject
    server {
        listen 80;
        listen [::]:80;

        server_name myproject.com;

        root /var/www/myproject/public;

        index index.php index.html index.htm;

        charset utf-8;
        client_max_body_size 10M;

        location / {
            try_files $uri $uri/ /index.php?_url=$uri&$args;
        }

        location ~ [^/]\.php(/|$) {
            fastcgi_pass unix:/run/php/php7.3-fpm.sock;
            fastcgi_index index.php;

            include fastcgi_params;

            fastcgi_split_path_info ^(.+?\.php)(/.*)$;

            if (!-f $document_root$fastcgi_script_name) {
                return 404;
            }

            fastcgi_param PATH_INFO $fastcgi_path_info;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }

        location ~ /\.ht {
            deny all;
        }

        location ~* \.(js|css|png|jpg|jpeg|gif|ico)$ {
            expires       604800;
            log_not_found off;
            access_log    off;
        }
    }
    EOF
    ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled/
    systemctl restart nginx

> In localhost, we must edit `/etc/hosts` and bind `myproject.com` to `127.0.0.1`
