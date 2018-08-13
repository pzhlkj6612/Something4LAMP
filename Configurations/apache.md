## Apache

### .htaccess

#### ```AllowOverride```

In ```/etc/apache2/apache2.conf``` or ```/etc/apache2/sites-availables/bala.conf```'s ```<VirtualHost/>``` block,

```xml
<Directory /dir/to/your/documentRoot>
  ...
  AllowOverride All
  ...
<Directory>
```

<br/>

#### Rewrite

##### Prepare

```rewrite``` mod need to be enabled,

```shell
sudo a2enmod rewrite
```

...

<br/>

### Virtual Host

#### ```ServerName```/```ServerAlias``` in name-based virtual host

Edit ```/etc/apache2/sites-availables/bala.conf``` to accept request which "name" is *example.com* or *\*.example.com*,

```xml
<VirtualHost *:80>
  ...
  ServerName example.com
  ServerAlias *.example.com
  ...
</VirtualHost>
```

or,

```xml
<VirtualHost *:80>
  ...
  ServerName www.example.com
  ServerAlias example.com *.example.com
  ...
</VirtualHost>
```

<br/>

Ref:

- [Name-based Virtual Host Support - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)
- [VirtualHost Examples - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/vhosts/examples.html)
- [What is the difference between ServerName and ServerAlias in apache2 configuration? - Stack Overflow](https://stackoverflow.com/questions/18362166/what-is-the-difference-between-servername-and-serveralias-in-apache2-configurati)
- [ubuntu 10.04 - Multiple &quot;ServerName&quot; per VHost? - Server Fault](https://serverfault.com/questions/294423/multiple-servername-per-vhost)
