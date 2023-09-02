#### 软件安装
```bash
#Debian/Ubuntu
$ sudo apt-get install targetcli-fb

#CentOS
$ yum -y install targetcli
```
#### 软件使用

配置程序：`targetcli`
相关服务：`targetclid.server`
配置文件目录：`/etc/rtslib-fb-target/`

```bash
o- / .................................. [...]  #根目录路径
o- backstores ......................... [...]  #根目录路径下的backstores目录
| o- block ............................ [Storage Objects: 0]   #根目录路径下backstores目录下的目录文件block文件路径，显示当前系统上的磁盘设备
| o- fileio ........................... [Storage Objects: 0]
| o- pscsi ............................ [Storage Objects: 0]
| o- ramdisk .......................... [Storage Objects: 0]
o- iscsi .............................. [Targets: 0]   #根目录下的iscsi目录，跟backstores同级别目录
o- loopback ........................... [Targets: 0]   #根目录下的loopbak目录，跟backstores和iscsi目录同级别
```