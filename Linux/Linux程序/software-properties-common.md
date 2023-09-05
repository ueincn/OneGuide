# 软件包名
software-properties-common

该软件提供了所使用的apt存储库的抽象。它使您可以轻松管理发行版和独立软件供应商的软件源。

实际上，这意味着它提供了一些用于添加和删除PPA的有用脚本：
```bash
$ dpkg -L software-properties-common | grep 'bin/'
/usr/bin/add-apt-repository
/usr/bin/apt-add-repository
```
加上DBUS后端，即可通过“软件和更新” GUI进行相同的操作。

没有它，您将需要通过编辑/etc/apt/sources.list和/或其中的任何辅助文件来手动添加和删除存储库（例如PPA）。/etc/apt/sources.list.d