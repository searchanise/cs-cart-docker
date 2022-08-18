# CS-Cart Development Environment

Docker-based development environment:

* PHP versions: 7.3, 7.4, 8.0, 8.1
* MySQL 5.7 database server.
* Nginx web server.

## Installation

1. Follow [Standard Docker application installation instructions](https://github.com/searchanise/environment/tree/master/docs/Docker-application-installation.md), REPOSITORY_URL=git@github.com:searchanise/cs-cart-docker.git
2. (Optional) For speed up in the future, you can disable installation when a cs-cart Docker container starts via setting an env variable in a file .env to value:
```bash
CSCART_INSTALL="no"
```
When you want to reinstall the cs-cart, don't forget to set it to a "yes" back
3. Add new hosts files to /etc/hosts:

```
127.0.0.1 localhost php7.3.cs-cart.local php7.4.cs-cart.local php8.0.cs-cart.local php8.1.cs-cart.local
```
4. Add via the [storefronts admin panel](http://php7.4.cs-cart.local:8100/admin.php?dispatch=companies.manage) new storefronts with the following URLs:
```
php7.3.cs-cart.local:8100
php8.0.cs-cart.local:8100
php8.1.cs-cart.local:8100
```
5. After installation, CS-Cart is available at these links:

  * [http://localhost:8100](http://localhost:8100) - CS-Cart for PHP 7.4
  * [http://php7.3.cs-cart.local:8100](http://php7.3.cs-cart.local:8100) - CS-Cart for PHP 7.3 
  * [http://php8.0.cs-cart.local:8100](http://php8.0.cs-cart.local:8100) - CS-Cart for PHP 8.0
  * [http://php8.1.cs-cart.local:8100](http://php8.1.cs-cart.local:8100) - CS-Cart for PHP 8.1
## Usage
First, enter to admin panel by a path /admin.php.

### Licences
You can enter here a license for disabling a trial subscription:
[Test CS-Cart licenses](https://www.notion.so/searchanise-team/Test-CS-Cart-licenses-5a0346cde10944c09a056c7cf7dee42a)

### Switch a CS-Cart product edition
For switch:
1. Change variable `CSCART_PRODUCT_EDITION` inside .env file to
   1. `ULTIMATE` - for ultimate edition
   1. `MULTIVENDOR` - for multivendor edition
2. Clear database and recreate containers:
```shell
docker-compose down
sudo rm -Rf app/db/*
docker-compose up -d
```

### Switch a CS-Cart version
```shell
cd app/www
git checkout $REVISION
```

### MySQL connection

You can connect MySQL Client to a database via settings from the "SETTING MYSQL" section of file .env.

## Development

### Sending e-mails

PHP containers do not send actual e-mails when using the `mail()` function.

All sent emails will be caught and stored in the `app/log/sendmail` directory.

### Enabling xDebug for PHP containers

xDebug is already configured.

You can read about configuring PHPStorm to work with Docker and xDebug 3 in the [Debugging PHP](https://thecodingmachine.io/configuring-xdebug-phpstorm-docker) article.


## Information
### Directories structure
See [standard Docker application structure](https://github.com/searchanise/environment/blob/master/docs/Docker-application-installation.md#directories-structure)

Also, the application has additional directories:
* `app`
  * `db` - database data files
  * `log` - mail logs
  * `www` - CS-Cart source files