## Apache

### .htaccess

Ref++:

- [25 Useful Apache &#039;.htaccess&#039; Tricks to Secure and Customize Websites](https://www.tecmint.com/apache-htaccess-tricks/)

<br/>

#### Prerequisite - ```AllowOverride```

In ```/etc/apache2/apache2.conf``` or ```/etc/apache2/sites-availables/bala.conf```'s ```<VirtualHost/>``` block,

```xml
<Directory /dir/to/your/documentRoot>
  ...
  AllowOverride All
  ...
</Directory>
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

Ref:

- [How To Set Up Mod_Rewrite | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-set-up-mod_rewrite)

<br/>

##### Syntax

###### RewriteBase

Ref:

- [mod rewrite - How does RewriteBase work in .htaccess - Stack Overflow](https://stackoverflow.com/questions/704102/how-does-rewritebase-work-in-htaccess)

<br/>

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
- [ServerAlias Directive # core - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/mod/core.html#serveralias)
- [What is the difference between ServerName and ServerAlias in apache2 configuration? - Stack Overflow](https://stackoverflow.com/questions/18362166/what-is-the-difference-between-servername-and-serveralias-in-apache2-configurati)
- [ubuntu 10.04 - Multiple &quot;ServerName&quot; per VHost? - Server Fault](https://serverfault.com/questions/294423/multiple-servername-per-vhost)

Ref++:

- [Configuring Apache Virtual Hosts | Servers for Hackers](https://serversforhackers.com/c/configuring-apache-virtual-hosts)
- [\<VirtualHost\> Directive # core - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/mod/core.html#virtualhost)

<br/>

### Pending

#### AH00558

```
AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using ::1. Set the 'ServerName' directive globally to suppress this message
```

<br/>

#### Authentication and Authorization

- [Authentication and Authorization - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/howto/auth.html)
- [Require Directive # mod_authz_core - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html#require)
- [Order Directive # mod_access_compat - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html#order)
- [Apache的Order Allow,Deny 详解 - 与时俱进 - 博客园](https://www.cnblogs.com/top5/archive/2009/09/22/1571709.html)
