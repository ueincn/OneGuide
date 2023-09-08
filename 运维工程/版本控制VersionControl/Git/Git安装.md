## Linux
It is easiest to install Git on Linux using the preferred package manager of your Linux distribution. If you prefer to build from source, you can find tarballs on kernel.org. The latest version is 2.40.0.

```bash
#Debian/Ubuntu
#For the latest stable version for your release of Debian/Ubuntu
$ sudo apt-get install git

#For Ubuntu, this PPA provides the latest stable upstream Git version
$ sudo add-apt-repository ppa:git-core/ppa 
$ sudo apt update
$ sudo apt install git

#Fedora
$ sudo yum install git #(up to Fedora 21)
$ sudo dnf install git #(Fedora 22 and later)

#Gentoo
$ sudo emerge --ask --verbose dev-vcs/git

#Arch Linux
$ sudo pacman -S git

#openSUSE
$ sudo zypper install git

#Mageia
$ sudo urpmi git

#Nix/NixOS
$ sudo nix-env -i git

#FreeBSD
$ sudo pkg install git

#Solaris 9/10/11 (OpenCSW)
$ sudo pkgutil -i git

#Solaris 11 Express
$ sudo pkg install developer/versioning/git

#OpenBSD
$ sudo pkg_add git

#Alpine
$ apk add git

#Slitaz
$ tazpkg get-install git
```

## Windows
官网下载安装即可：https://git-scm.com/download/win

## 从源码安装
如果你想从源码安装 Git，需要安装 Git 依赖的库：`autotools`、`curl`、`zlib`、`openssl`、`expat` 和 `libiconv`。 如果你的系统上有 `dnf` （如 Fedora）或者 `apt`（如基于 Debian 的系统），可以使用对应的命令来安装最少的依赖以便编译并安装 Git 的二进制版：
```bash
$ sudo dnf install dh-autoreconf curl-devel expat-devel gettext-devel openssl-devel perl-devel zlib-devel
#或
$ sudo apt-get install dh-autoreconf libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev
```
为了添加文档的多种格式（doc、html、info），需要以下附加的依赖：
```bash
$ sudo dnf install asciidoc xmlto docbook2X
$ sudo apt-get install asciidoc xmlto docbook2x
```
如果你使用基于 Debian 的发行版（Debian/Ubuntu/Ubuntu-derivatives），你也需要 `install-info` 包：
```bash
$ sudo apt-get install install-info
```
如果你使用基于 RPM 的发行版（Fedora/RHEL/RHEL衍生版），你还需要`getopt`包 （它已经在基于 Debian的发行版中预装了）：
```
$ sudo dnf install getopt
```
此外，如果你使用 Fedora/RHEL/RHEL衍生版，那么你需要执行以下命令：
```bash
$ sudo ln -s /usr/bin/db2x_docbook2texi /usr/bin/docbook2x-texi
```
以此来解决二进制文件名的不同。
当你安装好所有的必要依赖，你可以继续从几个地方来取得最新发布版本的 tar 包。 你可以从 Kernel.org 网站获取，网址为 https://www.kernel.org/pub/software/scm/git， 或从 GitHub 网站上的镜像来获得，网址为https://github.com/git/git/releases。 通常在 GitHub 上的是最新版本，但 kernel.org 上包含有文件下载签名，如果你想验证下载正确性的话会用到。
接着，编译并安装：
```bash
$ tar -zxf git-2.8.0.tar.gz
$ cd git-2.8.0
$ make configure
$ ./configure --prefix=/usr
$ make all doc info
$ sudo make install install-doc install-html install-info
```
完成后，你可以使用 Git 来获取 Git 的更新：
```bash
$ git clone git://git.kernel.org/pub/scm/git/git.git
```