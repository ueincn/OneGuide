### 安装教程
- Debian：[OpenStack Docs: OpenStack Installation Tutorial for Debian](https://docs.openstack.org/newton/zh_CN/install-guide-debian/)
### 实例安装

- **环境准备**
```bash
#! /bin/bash
hostanamectl set-hostname controllernode


#chrony install and configure
apt-get install chrony
echo "server ntp.aliyun.com iburst" >> /etc/chrony/chrony.conf
echo "allow 172.16.0.0/16" >> /etc/chrony/chrony.conf
service chrony restart
echo 'chronyc sources'

#install openstack client
apt install python-openstackclient
```
```bash
#! /bin/bash
hostanamectl set-hostname computenode


#chrony install and configure
apt-get install chrony
echo "server controllernode iburst" >> /etc/chrony/chrony.conf
service chrony restart
echo 'chronyc sources'

#install openstack client
apt install python-openstackclient
```
```bash
apt install mysql-server python-pymysql

vim /etc/mysql/conf.d/openstack.cnf

[mysqld]
bind-address = 10.0.0.11

default-storage-engine = innodb
innodb_file_per_table
max_connections = 4096
collation-server = utf8_general_ci
character-set-server = utf8

service mysql restart
```
```bash
apt install rabbitmq-server #安装包

rabbitmqctl add_user openstack RABBIT_PASS #添加 openstack 用户,用合适的密码替换 RABBIT_DBPASS.

rabbitmqctl set_permissions openstack ".*" ".*" ".*" #给``openstack``用户配置写和读权限
```
```bash
apt install memcached python-memcache

vim /etc/memcached.conf 
#修改包含了“-l 127.0.0.1”的那一行,配置这个服务使用控制节点的管理地址。这是为了让其它节点可以通过管理网络进行访
-l 10.0.0.11

service memcached restart
```

- **组件安装**
```bash
#datebase
#用数据库连接客户端以 root 用户连接到数据库服务器
mysql -u root -p
#创建 keystone 数据库
mysql> CREATE DATABASE keystone;
#对``keystone``数据库授予恰当的权限（用合适的密码替换 KEYSTONE_DBPASS）
mysql> GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'localhost' \
  IDENTIFIED BY 'KEYSTONE_DBPASS';
mysql> GRANT ALL PRIVILEGES ON keystone.* TO 'keystone'@'%' \
  IDENTIFIED BY 'KEYSTONE_DBPASS';

apt install keystone
vim /etc/keystone/keystone.conf

[database]
...
connection = mysql+pymysql://keystone:KEYSTONE_DBPASS@controller/keystone

#将``KEYSTONE_DBPASS``替换为你为数据库选择的密码。
#注释或删除``[database]``部分除``connection`以外的所有内容
```

