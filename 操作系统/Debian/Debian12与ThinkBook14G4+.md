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
- ### Vim
```bash
$ sudo apt-get install vim
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
#Pluma
$ sudo apt-get install pluma
``` 