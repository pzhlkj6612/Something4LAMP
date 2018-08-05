## Applications

### MediaWiki

#### Install && Configure

##### Base

```shell
sudo apt install -y apache2 php mysql-server libapache2-mod-php php-apcu php-mysql php-intl
```

<br/>

##### Apache

```shell
sudo a2enmod rewrite
```

```shell
sudo systemctl restart apache2.service
```

<br/>

- [Apache configuration - MediaWiki](https://www.mediawiki.org/wiki/Apache_configuration)

<br/>

##### PHP

```shell
sudo apt install -y php-mbstring php-curl
```

If you want use ```ImageMagick```, don't install ```GD``` by following command,
```shell
sudo apt install -y php-gd
```

Check,

```shell
php -i | grep support
```

```
Calendar support => enabled
date/time support => enabled
fileinfo support => enabled
FTP support => enabled
FTPS support => enabled
hash support => enabled
MHASH support => Enabled
iconv support => enabled
Internationalization support => enabled
json support => enabled
libXML support => active
Multibyte (japanese) regex support => enabled
Compression => supported
core SSL => supported
extended SSL => supported
OpenSSL support => enabled
pcntl support => enabled
PDO support => enabled
Phar: PHP Archive support => enabled
Native OpenSSL support => enabled
shmop support => enabled
SPL support => enabled
sysvmsg support => enabled
```

<br/>

- [PHP # Manual:Installation requirements - MediaWiki](https://www.mediawiki.org/wiki/Manual:Installation_requirements#PHP)
- [apt - PHP OpenSSL extension has a package? - Ask Ubuntu](https://askubuntu.com/questions/323005/php-openssl-extension-has-a-package)
- [PHP: Installation - Manual](http://php.net/manual/en/pcre.installation.php)

<br/>

##### MySQL

Secure MySQL firstly,

```shell
mysql_secure_installation
```

Then, create user and database for mediawiki,

```mysql
CREATE DATABASE wikidb;
GRANT ALL PRIVILEGES ON wikidb.* TO 'wikiuser'@'localhost' IDENTIFIED BY 'password';
```

Delete ```.mysql_history``` to avoid leaking passwords,

```shell
rm ~/.mysql_history
```

<br/>

- [MariaDB/MySQL # Create a database # Manual:Installing MediaWiki - MediaWiki](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki#MariaDB/MySQL)
- [Disable MySQL History &#8211; Clear ~/.mysql_history and MYSQL_HISTFILE](https://www.thegeekstuff.com/2010/01/disable-mysql-history-clear-mysql_history-and-mysql_histfile/)

<br/>

#### Exception handling

##### Failed at ```make check``` caused by ```wandtest``` in ```ImageMagick``` installation process

0. Remove pre-compiled version of ```ImageMagick```

```shell
sudo apt purge imagemagick
```

<br/>

1. Install ```freetype2```

```shell
sudo add-apt-repository ppa:glasen/freetype2
sudo apt update
sudo apt install -y freetype2-demos
```

<br/>

2. Install ```GhostScript```

```shell
sudo apt install -y ghostscript
sudo apt install -y libgs-dev
```

<br/>

3. Clean your source of ```ImageMagick``` which has been configured and installed just now

```shell
sudo make uninstall
make distclean
```

<br/>

4. Start again

```shell
cd ImageMagick-7.0.8-x
./configure --with-gslib=yes
make
sudo make install
sudo ldconfig /usr/local/lib
make check
```

<br/>

PS:

- Download ```ImageMagick``` from these mirrors: [Mirror @ ImageMagick](http://www.imagemagick.org/script/mirror.php)

<br/>

Ref:

- [Image thumbnailing # Manual:Installing third-party tools - MediaWiki](https://www.mediawiki.org/wiki/Manual:Installing_third-party_tools#Image_thumbnailing)
- [Install from Source @ ImageMagick](http://www.imagemagick.org/script/install-source.php)
- [How to Install FreeType 2.8 in Ubuntu 16.04, 17.04 | UbuntuHandbook](http://ubuntuhandbook.org/index.php/2017/06/install-freetype-2-8-in-ubuntu-16-04-17-04/)
- [Installing ImageMagick &amp; Ghostscript on Ubuntu](https://gist.github.com/leomelzer/3949356)
- [Advanced Unix Source Installation @ ImageMagick](http://www.imagemagick.org/script/advanced-unix-installation.php)
