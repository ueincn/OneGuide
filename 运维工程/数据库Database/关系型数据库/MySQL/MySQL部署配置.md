# 资源下载
**下载路径：**[MySQL :: Download MySQL Community Server (Archived Versions)](https://downloads.mysql.com/archives/community/)
> **DEB Bundle与DEB Package的区别**
> DEB Bundle是将deb文件全部打包成一个压缩包，解压出来全部都是deb文件，通过dkg命令进行安装即可。
> DEB Package本身就是deb文件，下载回来之后直接用dkg命令安装。
> tar.gz这些就是压缩吧，一般下载这个即可，解压之后需要自行处理。

# MySQL安装
```bash
$ mkdir mysql
$ cd mysql

$ wget https://downloads.mysql.com/archives/get/p/23/file/mysql-server_5.7.39-1debian10_amd64.deb-bundle.tar
$ tar -xvf mysql-server_5.7.39-1debian10_amd64.deb-bundle.tar

解压出来是这些包：
libmysqlclient20_5.7.39-1debian10_amd64.deb
libmysqlclient-dev_5.7.39-1debian10_amd64.deb
libmysqld-dev_5.7.39-1debian10_amd64.deb
mysql-client_5.7.39-1debian10_amd64.deb
mysql-common_5.7.39-1debian10_amd64.deb
mysql-community-client_5.7.39-1debian10_amd64.deb
mysql-community-server_5.7.39-1debian10_amd64.deb
mysql-community-source_5.7.39-1debian10_amd64.deb
mysql-community-test_5.7.39-1debian10_amd64.deb
mysql-server_5.7.39-1debian10_amd64.deb
mysql-testsuite_5.7.39-1debian10_amd64.deb

# 这里这些文件存在着依赖关系，如果一个一个安装，要安装顺序来安装：
$ sudo dpkg -i mysql-common_5.6.28-1ubuntu14.04_amd64.deb
$ sudo dpkg -i libmysqlclient18_5.6.28-1ubuntu14.04_amd64.deb
$ sudo dpkg -i libmysqlclient-dev_5.6.28-1ubuntu14.04_amd64.deb
$ sudo dpkg -i libmysqld-dev_5.6.28-1ubuntu14.04_amd64.deb
$ sudo dpkg -i mysql-community-server_5.6.28-1ubuntu14.04_amd64.deb 
# 注意在安装mysql-community-server会要求输入root账户密码

$ sudo dpkg -i mysql-server_5.6.28-1ubuntu14.04_amd64.deb 
$ sudo dpkg -i mysql-community-client_5.6.28-1ubuntu14.04_amd64.deb
$ sudo dpkg -i mysql-client_5.6.28-1ubuntu14.04_amd64.deb 
# 到这里，mysql的安装完成

还有几个文件没有用，用处现在不知道
mysql-community-bench_5.6.28-1ubuntu14.04_amd64.deb
mysql-community-source_5.6.28-1ubuntu14.04_amd64.deb
mysql-community-test_5.6.28-1ubuntu14.04_amd64.deb
mysql-testsuite_5.6.28-1ubuntu14.04_amd64.deb

$ service mysql start # 启动MySQL
$ service mysql status # 查看MySQL状态
```
# MySQL配置文件
```bash
$ ps aux | grep mysql | grep 'my.cnf'
# 若使用ps aux | grep mysql | grep 'my.cnf'命令之后没有任何输出，
# 则表示没有设置使用指定目录下的my.cnf文件。

$ mysql --help | grep 'my.cnf'
# 查看MySQL启动时读取配置文件的默认目录。
# MySQL启动时默认会依次读取的配置文件，并且顺序排前的优先。
```
# MySQL运行相关
```bash
$ service mysql status # 查看MySQL状态
$ service mysql stop # 停止MySQL
$ service mysql restart # 重载MySQL
$ service mysql start # 启动MySQL


# 卸载（参考)
$ sudo apt-get --purge remove mysql-server
$ sudo apt-get --purge remove mysql-client
$ sudo apt-get --purge remove mysql-common

最后再通过下面的命令清理残余
$ sudo apt-get autoremove
$ sudo apt-get autoclean
$ sudo rm /etc/mysql/ -R
$ sudo rm /var/lib/mysql/ -R
```
# MySQL配置端口访问规则
```bash
$ netstat -tnpl #查看端口监听情况
$ netstat -nalp | grep 3306 #查看端口
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN

$ vim /etc/mysql/my.cnf
bind-address  = 0.0.0.0 #配置0.0.0.0允许外网访问
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN

$ service mysql restart # 重载MySQL

【以上为解决可尝试下面方法】
1、改表法
$ mysql -uroot -pdbaroot #登录数据库

$ mysql>use mysql; #切换数据库
$ mysql>update user set host = '%' where user = 'root';
$ mysql>select host, user from user;
$ mysql>flush privileges; #刷新权限
# 登入mysql后，更改 "mysql" 数据库里的 "user" 表里的 "host" 项，从"localhost"改称"%"

2、授权法

$ mysql -uroot -pdbaroot #登录数据库

# 添加远程ip访问权限，admin  连接用户名，123456  连接密码
$ mysql>GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' IDENTIFIED BY '123456' WITH GRANT OPTION;
$ mysql>flush privileges; #刷新权限
```
