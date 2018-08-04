## Applications

### MediaWiki

...

<br/>

#### Failed at ```make check``` caused by ```wandtest``` in ```ImageMagick``` installation process

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
