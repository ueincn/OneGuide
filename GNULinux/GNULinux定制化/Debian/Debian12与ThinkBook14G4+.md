[TOC]

## 实际环境
> 设备：ThinkBook 14 G4+
> 配置：8C16G
> 系统：Debian GNU/Linux 12 (bookworm)
> 内核: Linux 6.1.0-10-amd64

## 系统镜像
> 镜像版本：debian-12.1.0-amd64-DVD-1.iso

> 镜像源：
> deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
> deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm main contrib non-free non-free-firmware
> deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
> deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-updates main contrib non-free non-free-firmware
> deb https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware
> deb-src https://mirrors.tuna.tsinghua.edu.cn/debian/ bookworm-backports main contrib non-free non-free-firmware

> 桌面环境：Xfce 4.18

## WIFI驱动安装
1.基础环境安装
```bash
$ sudo apt-get install build-essential linux-headers-$(uname -r) git
```
2.下载驱动并安装
```bash
$ git clone https://github.com/lwfinger/rtw89.git
$ cd rtw89
$ sudo make
$ sudo make install
```
3.加载驱动模块
```bash
$ sudo modprobe -rv rtw_8852ae
```
4.重启系统
```bash
$ sudo reboot
```
## 软件安装
- ### 开发编译环境
```bash
$ sudo apt-get install build-essential linux-headers-$(uname -r)
```

- ### Gimp
```bash
$ sudo apt-get install gimp
#启动
$ gimp
```
- ### Git
```bash
$ sudo apt-get install git
```
- ### VSCode
```bash
$ wget https://az764295.vo.msecnd.net/stable/660393deaaa6d1996740ff4880f1bad43768c814/code_1.80.2-1690491597_amd64.deb
$ sudo chmod 777 code_1.80.2-1690491597_amd64.deb
$ sudo apt-get install -f ./code_1.80.2-1690491597_amd64.deb

#启动
$ code
```
### 微软浏览器 Edge
```bash
$ wget https://packages.microsoft.com/repos/edge/pool/main/m/microsoft-edge-stable/microsoft-edge-stable_115.0.1901.188-1_amd64.deb
$ sudo chmod 777 microsoft-edge-stable_115.0.1901.188-1_amd64.deb
$ sudo apt-get install ./microsoft-edge-stable_115.0.1901.188-1_amd64.deb

#启动
$ microsoft-edge-stable
```
### 谷歌浏览器 Chrome
```bash
$ wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
$ sudo chmod 777 google-chrome-stable_current_amd64.deb
$ sudo apt-get install ./google-chrome-stable_current_amd64.deb

#启动
$ google-chrome-stable
```
### Pycharm
```bash
$ wget https://download.jetbrains.com.cn/python/pycharm-community-2023.2.tar.gz
$ tar -xvf pycharm-community-2023.2.tar.gz && sudo mv pycharm-community-2023.2 /opt/pycharm
$ sudo chmod -R 777 /opt/pycharm/
$ sudo cp /opt/pycharm/bin/pycharm.png /usr/share/icons/hicolor/128x128/apps/
$ sudo cat /usr/share/applications/pycharm.desktop << EOF
[Desktop Entry]
Name=Pycharm
Exec=/opt/pycharm/bin/pycharm.sh %U
StartupNotify=true
Terminal=false
Icon=pycharm
Type=Application
Categories=TextEditor;Development;IDE;
EOF

#更新图标缓存
$ gtk-update-icon-cache /usr/share/icons/hicolor
```
### 文本处理器
```bash
# Pluma
$ sudo apt-get install pluma

# Vim
$ sudo apt-get install vim
``` 

### Fcitx5 中文輸入法
Debian 12 中文安装Xfce4桌面环境时默认已经安装Fcitx5
官网：[https://fcitx-im.org/wiki/Install_Fcitx_5/zh-cn](https://fcitx-im.org/wiki/Install_Fcitx_5/zh-cn)
```bash
$ sudo apt install --install-recommends fcitx5 fcitx5-chinese-addons
$ fcitx5-configtool #配置中文 - 拼音
```

### wps
```bash
$ wget https://wps-linux-personal.wpscdn.cn/wps/download/ep/Linux2019/11698/wps-office_11.1.0.11698_amd64.deb
$ sudo dpkg -i wps-office_11.1.0.11698_amd64.deb
$ git clone https://github.com/dv-anomaly/ttf-wps-fonts.git
$ sudo mkdir /usr/share/fonts/wps-fonts
$ sudo mv ttf-wps-fonts/* /usr/share/fonts/wps-fonts
$ sudo chmod 644 /usr/share/fonts/wps-fonts/*
$ sudo fc-cache -vfs
$ rm -rf ttf-wps-fonts/
```

### Clash
```bash
$ wget https://github.com/Fndroid/clash_for_windows_pkg/releases/download/0.20.30/Clash.for.Windows-0.20.30-x64-linux.tar.gz
$ wget https://cdn.jsdelivr.net/gh/Dreamacro/clash@master/docs/logo.png
$ sudo mkdir -p /opt/Clash
$ sudo tar -xvf Clash.for.Windows-0.20.30-x64-linux.tar.gz
$ sudo cp -r Clash\ for\ Windows-0.20.30-x64-linux/* /opt/Clash/
$ sudo cp logo.png /opt/Clash
$ sudo chmod -R +x /opt/Clash

#创建快捷方式
sudo vim /usr/share/applications/clash.desktop
    [Desktop Entry]
    Name=Clash
    Comment=A Windows/macOS/Linux GUI based on Clash and Electron.
    Exec=/opt/Clash/cfw
    Icon=/opt/Clash/logo.png
    Type=Application
    Categories=Development;
    StartupNotify=true
    NoDisplay=false
```

### Wine
```bash
#64
$ sudo apt-get install wine
$ export WINEARCH=win64
$ export WINEPREFIX=~/.wine64
$ wincfg

#32
$ sudo apt upgrade && sudo apt update
$ sudo dpkg --add-architecture i386
$ sudo apt-get update
$ sudo apt-get install wine32
$ export WINEARCH=win32
$ export WINEPREFIX=~/.wine32
$ wincfg

#安装程序
$ wine xxx.exe

```
## KVM环境
### 1.系统虚拟化环境检测
```bash
$ egrep "(svm|vmx)" /proc/cpuinfo
#注：
#vmx 对应Inter 的cpu
#svm 对应Amd 的cpu
#需在主板Bios 打开虚拟化选项，多数计算机默认处于打开状态
```
### 2.KVM 模块检测
```bash
$ lsmod | grep kvm
kvm_amd               102400  0
kvm                   782336  1 kvm_amd
```
```bash
$ modinfo kvm
filename:       /lib/modules/5.10.0-5-generic/kernel/arch/x86/kvm/kvm.ko
license:        GPL
author:         Qumranet
srcversion:     D9AD71CCC4F7B26584E70EB
depends:        
retpoline:      Y
intree:         Y
name:           kvm
vermagic:       5.10.0-5-generic SMP mod_unload modversions 
sig_id:         PKCS#7
signer:         Build time autogenerated kernel key
sig_key:        74:73:26:3D:9C:19:20:92:02:53:05:CF:F5:62:EC:C5:CA:58:66:9E
sig_hashalgo:   sha512
signature:      0E:A4:27:4F:06:36:D6:7F:F3:5E:C4:0F:73:B2:EB:C0:C7:A1:35:D2:
	        FF:E3:4B:00:E0:C5:25:37:0C:B7:5F:AF:56:CD:B5:D7:E6:6D:47:A5:
                ......
```
### 3.KVM 相关软件安装
```bash
$ sudo apt-get install libvirt-daemon-system \
libvirt-clients \
virtinst \
qemu-system \
qemu-system-gui \
bridge-utils \
virt-manager

#备注
#libvirt-daemon-system >> libvirtd
#libvirt-clients >> virsh
#virtinst >> virt-install/virt-viewer
#qemu-system >> qemu-system-x86_64
#qemu-system-gui >> gtk
#bridge-utils >> bridge
#virt-manager >> graphical KVM
```
### 4.KVM启动并加入开机自启
```bash
$ sudo systemctl restart libvirtd.service #启动libvirtd
$ sudo systemctl enable libvirtd.service #开机自启

$ sudo systemctl status libvirtd.service #查看启动状态
```

## Docker环境
### 1.Docker安装
```bash
$ sudo apt-get install docker.io docker-compose
```
### 2.Dcoker启动
```bash
$ sudo systemctl start docker.service
$ sudo systemctl enable docker.service
$ sudo systemctl start docker.socket
$ sudo systemctl enable docker.socket
```
### 3.Docker关闭
```bash
$ sudo systemctl stop docker.socket
$ sudo systemctl disable docker.socket
$ sudo systemctl stop docker.service
$ sudo systemctl disable docker.service
```
## VNC环境
### VNC客户端
#### tigervnc-viewer
```bash
#安装
$ sudo apt-get install tigervnc-viewer

#启动
$ vncviewer
```
### VNC服务端


## 数据库MySQL环境
```bash
$ sudo apt-get install mariadb-server

# dpkg -l | grep mariadb
#ii  libdbd-mariadb-perl                   1.22-1+b1                            amd64        Perl5 database interface to the MariaDB/MySQL databases
#ii  libmariadb3:amd64                     1:10.11.3-1                          amd64        MariaDB database client library
#ii  mariadb-client                        1:10.11.3-1                          amd64        MariaDB database client binaries
#ii  mariadb-client-core                   1:10.11.3-1                          amd64        MariaDB database core client binaries
#ii  mariadb-common                        1:10.11.3-1                          all          MariaDB common configuration files
#ii  mariadb-plugin-provider-bzip2         1:10.11.3-1                          amd64        BZip2 compression support in the server and storage engines
#ii  mariadb-plugin-provider-lz4           1:10.11.3-1                          amd64        LZ4 compression support in the server and storage engines
#ii  mariadb-plugin-provider-lzma          1:10.11.3-1                          amd64        LZMA compression support in the server and storage engines
#ii  mariadb-plugin-provider-lzo           1:10.11.3-1                          amd64        LZO compression support in the server and storage engines
#ii  mariadb-plugin-provider-snappy        1:10.11.3-1                          amd64        Snappy compression support in the server and storage engines
#ii  mariadb-server                        1:10.11.3-1                          amd64        MariaDB database server binaries
#ii  mariadb-server-core                   1:10.11.3-1                          amd64        MariaDB database core server files

```

## 微信
```bash
$ wget https://archive.ubuntukylin.com/ubuntukylin/pool/partner/weixin_2.1.4_amd64.deb
$ sudo dpkg -i wget weixin_2.1.4_amd64.deb

#
```