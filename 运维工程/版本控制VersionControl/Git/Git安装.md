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