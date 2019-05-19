### How to configure Zephir PHP

Require `php-zephir-parser`

#### php-zephir-parser
> sudo apt-get install php-dev gcc make re2c autoconf  
> git clone git://github.com/phalcon/php-zephir-parser.git  
> cd php-zephir-parser  
> phpize  
> ./configure  
> make  
> sudo make install  

Enable Zephir parser module by adding `extension=zephir_parser.so`

> nano /etc/php/7.3/mods-available/zephir_parser.ini  
> phpenmod zephir_parser  

#### Zephir
Main GIT project
> git clone https://github.com/phalcon/zephir.git  
> cd zephir  
> composer install

Some extensions are required for composer install to work
