## Applications

### MediaWiki

#### Install && Configure

First of all, read [Manual:Running MediaWiki on Debian or Ubuntu - MediaWiki](https://www.mediawiki.org/wiki/Manual:Running_MediaWiki_on_Debian_or_Ubuntu) if you use Debian/**Ubuntu**.

And, what you have to know is that the following are all shit :)

---

- [Main installation guide # Manual:Installation guide - MediaWiki](https://www.mediawiki.org/wiki/Manual:Installation_guide#Main_installation_guide)
  - Before installation
    - [Read what MediaWiki is](https://www.mediawiki.org/wiki/Manual:What_is_MediaWiki%3F)
    - [Check the MediaWiki feature list](https://www.mediawiki.org/wiki/Manual:MediaWiki_feature_list)
    - [Installation requirements](https://www.mediawiki.org/wiki/Manual:Installation_requirements) - Check these before going any further!
  - [Installing MediaWiki](https://www.mediawiki.org/wiki/Manual:Installing_MediaWiki)
  - Configuring MediaWiki
    - [Initial configuration](https://www.mediawiki.org/wiki/Manual:Config_script) (using the configuration script)
    - [Further configuration](https://www.mediawiki.org/wiki/Manual:System_administration)
    - [Installing extensions](https://www.mediawiki.org/wiki/Manual:Extensions)

---

##### Base

```shell
sudo apt install -y apache2 php mysql-server libapache2-mod-php php-apcu php-mysql php-intl
```

<br/>

##### Apache

Enable ```rewrite``` module,

```shell
sudo a2enmod rewrite
```

Make it effective,

```shell
sudo systemctl restart apache2.service
```

<br/>

- [Apache configuration - MediaWiki](https://www.mediawiki.org/wiki/Apache_configuration)

<br/>

##### PHP

Install extensions ```php-mbstring```, ```php-xml``` and ```php-curl```,

```shell
sudo apt install -y php-mbstring php-xml php-curl
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

#### Tweaking

##### [Short URL](https://www.mediawiki.org/wiki/Manual:Short_URL)

- [MediaWiki ShortURL Builder - Redwerks](https://shorturls.redwerks.org/)
- \*[$wgScriptExtension *was removed completely in version 1.27.0*](https://www.mediawiki.org/wiki/Manual:$wgScriptExtension).

<br/>

#### Security issues

[Manual:Security - MediaWiki](https://www.mediawiki.org/wiki/Manual:Security)

[Manual:Configuring file uploads - MediaWiki](https://www.mediawiki.org/wiki/Manual:Configuring_file_uploads)

<br/>

##### For binary

Prevent ```www-data``` destroying the wiki,

```shell
chown -R user-I-use:group-I-stay-in MediaWiki/
```

If File-upload enabled,

```shell
chown -R www-data:www-data MediaWiki/images/
```

*Staff Only*

```shell
chmod -R go-w MediaWiki/
```

Sensitive data in ```LocalSettings.php``` should be protected(More consideration needed),

```shell
chown www-data:group-I-stay-in MediaWiki/LocalSettings.php
chmod 660 MediaWiki/LocalSettings.php
```

<br/>

##### For visitor

- ```.htaccess``` in ```MediaWiki/images``` folder(if File-upload enabled)

```
# Serve HTML as plaintext, don't execute SHTML
AddType text/plain .html .htm .shtml .phtml .php .php3 .php4 .php5 .php7

# Old way of registering php with AddHandler
RemoveHandler .php

# Recent way of registering php with SetHandler
<FilesMatch "\.ph(p[3457]?s?|tml)$">
   SetHandler None
</FilesMatch>

php_flag engine off
```

- ```.htaccess``` in ```MediaWiki/mw-config``` folder(optional)

```
order deny,allow
deny from all
```

- ```.htaccess``` in ```MediaWiki/``` folder

```
options -indexes
```

<br/>

#### Extensions

- [Extension:Math - MediaWiki](https://www.mediawiki.org/wiki/Extension:Math)

<br/>

- [Extension:UploadWizard - MediaWiki](https://www.mediawiki.org/wiki/Extension:UploadWizard)
- [Extension:MsUpload - MediaWiki](https://www.mediawiki.org/wiki/Extension:MsUpload)

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

<br/>

#### Pending

- [Uploading directly from a URL ("Sideloading") # Manual:Configuring file uploads - MediaWiki](https://www.mediawiki.org/wiki/Manual:Configuring_file_uploads#Uploading_directly_from_a_URL_("Sideloading"))
- [Configuring the upload form # Manual:Configuring file uploads - MediaWiki](https://www.mediawiki.org/wiki/Manual:Configuring_file_uploads#Configuring_the_upload_form)

<br/>

#### Something complicated

- [Manual:Image administration - MediaWiki](https://www.mediawiki.org/wiki/Manual:Image_administration)
- [Manual:thumb.php - MediaWiki](https://www.mediawiki.org/wiki/Manual:Thumb.php)

<br/>

#### [FAQ](https://www.mediawiki.org/wiki/Manual:FAQ)
