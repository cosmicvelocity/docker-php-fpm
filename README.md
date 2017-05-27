# docker-php-fpm
[php-fpm-alpine](https://hub.docker.com/_/php/) をカスタマイズした docker イメージです。
alpine linux を元に構築されているのでイメージサイズが軽量です。

## 5.6
php:5.6.30-fpm-alpine を元にしています。

### 導入済みモジュール
- apcu (4.0.11)
- curl
- exif
- gd
- iconv
- intl
- mbstring
- mcrypt
- memcached (2.2.0)
- mongodb (1.2.9)
- mysqli
- opcache
- pdo_mysql
- redis (3.1.2)
- xdebug (2.5.3)
- zip

### コンテナのビルド

    $ git clone https://github.com/cosmicvelocity/docker-php-fpm.git
    $ cd docker-php-fpm
    $ cd 5.6
    $ docker build -t cosmicvelocity/php-fpm:5.6 .

### 実行

    $ docker run -v $(pwd)/examples:/var/www/html --name php-fpm --rm cosmicvelocity/php-fpm:5.6

## 7.0
php:7.0.18-fpm-alpine を元にしています。

### 導入済みモジュール
- apcu (5.1.8)
- curl
- exif
- gd
- iconv
- intl
- mbstring
- mcrypt
- memcached (3.0.2)
- mongodb (1.2.9)
- mysqli
- opcache
- pdo_mysql
- redis (3.1.2)
- xdebug (2.5.3)
- zip

### コンテナのビルド

    $ git clone https://github.com/cosmicvelocity/docker-php-fpm.git
    $ cd docker-php-fpm
    $ cd 7.0
    $ docker build -t cosmicvelocity/php-fpm:7.0 .

### 実行

    $ docker run -v $(pwd)/examples:/var/www/html --name php-fpm --rm cosmicvelocity/php-fpm:7.0
