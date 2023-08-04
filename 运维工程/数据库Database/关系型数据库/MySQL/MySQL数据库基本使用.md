### 基本使用
```sql
#切换数据库
mysql> use mysql;

#刷新权限表
mysql> flush privileges;

#创建用户
mysql(database)> CREATE USER 'username'@'%' IDENTIFIED BY 'password';
#用户授权
mysql(database)> grant all privileges on *.* to 'username'@'localhost' ;
-- username //用户名称
-- localhost //Host。（localhost：本地）（%：所有地址可访问）

#修改密码
mysql(database)> alter user 'root'@'localhost' identified by 'root_password'; 
-- root 用户名
-- root_password替换成需要改的密码
```
```sql
#查看端口号
mysql(database)> show global variables like ‘port’; 

#查看所有数据库
mysql((database))> SHOW DATABASES; 

#查询数据库账户信息
mysql> select host,user,password from user; 
```
```sql
#删除用户
mysql> DROP USER 'username'@'localhost';
```
### 实例使用
场景一、**MySQL配置允许远程连接**
#### 方式一
1、进入mysql： 
```sql
mysql -uroot -p
```
2、运行切换mysql数据库： 
```sql
use mysql;
```
3、开启远程访问权限： 
```sql
GRANT ALL PRIVILEGES ON *.* TO 'username'@'%' IDENTIFIED BY 'password';
```
4、强制刷新权限： 
```sql
flush privileges;
```
5、关闭mysql： 
```sql
exit;
```
#### 方式二
1、进入mysql： 
```sql
mysql -uroot -p
```
2、运行切换mysql数据库： 
```sql
use mysql;
```
3、查看用户表： 
```sql
SELECT `Host`,`User` FROM user;
```
4、更新用户表： 
```sql
UPDATE user SET `Host` = '%' WHERE `User` = 'root' LIMIT 1;
```
5、强制刷新权限： 
```sql
flush privileges;
```
6、关闭mysql： 
```sql
exit;
```
场景二：**创建远程连接账户并授权**
```sql
-- 创建用户
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
-- 授权
grant all privileges on *.* to 'username'@'%' ;
```

- username #用户名称
- localhost #Host。（localhost：本地）（%：所有地址可访问）

场景三：**忘记密码**

1.找到Mysql配置文件：`my.cnf`或`mysqld.cnf`，添加`skip-grant-tables`跳过密码。
```sql
[mysqld]
skip-grant-tables
```
2.重启Mysql服务
```bash
$ sudo systemctl restart mysql
# 或者 sudo service mysql restart
```
3.登录Mysql，不用输入密码（如果提示输入密码，回车跳过即可）
```bash
$ mysql -uroot
```
4.清空root用户密码并退出数据库
```bash
mysql> use mysql
mysql> update user set authentication_string = '' where user = 'root';
mysql> quit
Bye
```
5.配置文件注释掉`skip-grant-tables`，重启Mysql
6.登录Mysql，不用输入密码（如果提示输入密码，回车跳过即可）
7.更新root密码并刷新权限。
```bash
mysql> use mysql #切换数据库
mysql> select user,host from user where user='root'; #查看root用户
mysql> alter user 'root'@'localhost' identified by 'root_password'; #root_password替换成需要改的密码
mysql> flush privileges; #刷新权限
mysql> quit
Bye
```
### 问题FAQ
问题一：**ERROR 1698 (28000): Access denied for user 'root'@'localhost'**#### Link

- [https://blog.csdn.net/jlu16/article/details/82809937](https://blog.csdn.net/jlu16/article/details/82809937)
- [https://stackoverflow.com/questions/39281594/error-1698-28000-access-denied-for-user-rootlocalhost](https://stackoverflow.com/questions/39281594/error-1698-28000-access-denied-for-user-rootlocalhost)
#### 原因
因为在安装中，MySQL默认使用了UNIX auth_socket plugin插件。简单来说这意味着当db_users使用数据库时，**将会通过系统用户认证表进行认证**。
#### 命令查看
就像你在查询语句中看到的那样，root用户在使用auth_socket插件。
```sql
$ sudo mysql -u root # I had to use "sudo" since is new installation

mysql> USE mysql;
mysql> SELECT User, Host, plugin FROM mysql.user;

+------------------+-----------------------+
| User             | plugin                |
+------------------+-----------------------+
| root             | auth_socket           |
| mysql.sys        | mysql_native_password |
| debian-sys-maint | mysql_native_password |
+------------------+-----------------------+
```
#### 解决方法
方法一：**设置你的root用户使用mysql_native_password插件**
```sql
$ sudo mysql -u root # I had to use "sudo" since is new installation

mysql> USE mysql;
mysql> UPDATE user SET plugin='mysql_native_password' WHERE User='root';
mysql> FLUSH PRIVILEGES;
mysql> exit;

$ service mysql restart
```
方法二：**可以创建一个与你的系统用户一致的新的数据库用户（推荐）**

- 用你的操作系统用户名代替YOUR_SYSTEM_USER
```sql
$ sudo mysql -u root # I had to use "sudo" since is new installation

mysql> USE mysql;
mysql> CREATE USER 'YOUR_SYSTEM_USER'@'localhost' IDENTIFIED BY '';
mysql> GRANT ALL PRIVILEGES ON *.* TO 'YOUR_SYSTEM_USER'@'localhost';
mysql> UPDATE user SET plugin='auth_socket' WHERE User='YOUR_SYSTEM_USER';
mysql> FLUSH PRIVILEGES;
mysql> exit;

$ service mysql restart
```
记住如果你选择使用方法2，你应该通过使用你的操作系统用户名来连接到MySQL（mysql -u YOUR_SYSTEM_USER）。
注意：在一些操作系统中（例如Debian系）‘auth_socket’插件被叫做’unix_socket’，所以相应的SQL命令语句应该为UPDATE user SET plugin=‘unix_socket’ WHERE User=‘YOUR_SYSTEM_USER’。
