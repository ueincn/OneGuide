# 安装
# 配置
当MariaDB安装完成后，你可能会想运行命令mysql -u root -p登录到MariaDB服务器。

如果你登录到Debian的用户不是root用户你将不能访问MariaDB服务器。如果你尝试使用密码登录也将被拒绝连接，因为在安装的过程我们并没有设置密码。


你将会收到类似于这样的消息(28000): Access denied for user 'root'@'localhost' (using password: YES)或者ERROR 1045 (28000): Access denied for user 'root'@'localhost'。

这意味着您无法通过提供密码来以root用户连接到MariaDB服务器。但你可以通过命令sudo mysql连接到MariaDB服务器。
```bash
sudo mysql
Welcome to the MySQL monitor.  Commands end with ; or \g.
mysql>
```
如果您要使用外部程序，例如phpMyAdmin。以root用户连接到MariaDB服务器，则需要创建一个新的专用管理用户，该用户可以访问所有数据库。
```sql
GRANT ALL ON *.* TO 'admin'@'localhost' IDENTIFIED BY '你的密码' WITH GRANT OPTION;

FLUSH PRIVILEGES;
```
当创建新的专用用户后，你可以通过新的管理用户使用密码的方式登录，你可以在本地计算机上运行命令mysql -u admin -p进行测试。