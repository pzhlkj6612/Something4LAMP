# Something4LAMP

- [LAMP (software bundle) - Wikipedia](https://en.wikipedia.org/wiki/LAMP_(software_bundle))
- [HOME... Create a LAMP stack from source code - How to LAMP](http://howtolamp.com/)

<br/>

## Install & Configure

### Semi-Automatic

[teddysun/lamp: Install LAMP(Linux + Apache + MySQL/MariaDB/Percona Server + PHP ) for CentOS/Debian/Ubuntu](//github.com/teddysun/lamp)

- [linux 技巧：使用 screen 管理你的远程会话](https://www.ibm.com/developerworks/cn/linux/l-cn-screen/)

<br/>

### Automatic

No way.

<br/>

### Manual

1. **L**inux -> [Ubuntu]((//github.com/pzhlkj6612/Something4Ubuntu-Desktop-1604-LTS/tree/HEAD/Tweak-My-Own-Ubuntu))

<br/>

2. [**A**pache](./Configurations/apache.md)

```shell
sudo apt install -y apache2 && sudo apt install -y libapache2-mod-php
```

About libapache2-mod-auth-mysql:

- [php - Package libapache2-mod-auth-mysql is not available - Stack Overflow](https://stackoverflow.com/questions/20458641/package-libapache2-mod-auth-mysql-is-not-available)
- [apache2 - Ubuntu 13.10 gives &quot;Package &#39;libapache2-mod-auth-mysql&#39; has no installation candidate&quot; error - Ask Ubuntu](https://askubuntu.com/questions/365061/ubuntu-13-10-gives-package-libapache2-mod-auth-mysql-has-no-installation-cand)
- [apt - Unable to locate package libapache2-mod-auth-mysql - Ask Ubuntu](https://askubuntu.com/questions/716577/unable-to-locate-package-libapache2-mod-auth-mysql)

<br/>

3. [**M**ySQL](//github.com/pzhlkj6612/Something4SQL/tree/HEAD/MySQL)

```shell
sudo apt install -y mysql-server
```

```shell
mysql_secure_installation
```

[MySQL :: MySQL 5.7 Reference Manual :: 4.4.4 mysql_secure_installation — Improve MySQL Installation Security](https://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html)

If something goes wrong: [16.04 - Cannot reinstall mysql-server after its purge - Ask Ubuntu](https://askubuntu.com/questions/763534/cannot-reinstall-mysql-server-after-its-purge/763623)

<br/>

4. [**P**HP](./Configurations/php.md)

```shell
sudo apt install -y php && sudo apt install -y php-mysql
```

<br/>

5. **P**ython

...

<br/>

6. phpMyAdmin

```shell
sudo apt install -y phpmyadmin
```

<br/>

## Applications

- [#](./Applications/owncloud.md) | ownCloud
- [#](./Applications/mediawiki.md) | MediaWiki
