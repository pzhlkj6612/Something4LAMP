## Applications

### ownCloud 10.0

#### pre-Install

##### Add the repository key to apt

```shell
wget -nv https://download.owncloud.org/download/repositories/10.0/Ubuntu_16.04/Release.key -O Release.key
sudo apt-key add - < Release.key
rm Release.key
```

```
OK
```

```shell
echo 'deb http://download.owncloud.org/download/repositories/10.0/Ubuntu_16.04/ /' | sudo tee --append /etc/apt/sources.list.d/owncloud.list > /dev/null
sudo apt update
sudo apt install owncloud-files
```

<br/>

Ref:

- [Install package owncloud-files](http://download.owncloud.org/download/repositories/10.0/owncloud/)

<br/>

#### Install

#### Configure

##### Warnings
