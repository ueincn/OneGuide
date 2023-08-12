在确认mariadb数据库软件程序安装完毕并成功启动后请不要立即使用。为了确保数据库的安全性和正常运转，需要先对数据库程序进行初始化操作。这个初始化操作涉及下面5个步骤。
> 设置root管理员在数据库中的密码值（注意，该密码并非root管理员在系统中的密码，这里的密码值默认应该为空，可直接按回车键）。
> 
> 设置root管理员在数据库中的专有密码。
> 
> 删除匿名用户，并使用root管理员从远程登录数据库，以确保数据库上运行的业务的安全性。
> 
> 删除默认的测试数据库，取消测试数据库的一系列访问权限。
> 
> 刷新授权列表，让初始化的设定立即生效。

#### 使用`mysql_secure_installation`进行初始化设置。
```bash
[root@hostname ~]# mysql_secure_installation 

NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none): 输入管理员原始密码，默认为空值，直接回车即可
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] y（设置管理员密码）
New password: 输入新的密码
Re-enter new password: 再次输入密码
Password updated successfully!
Reloading privilege tables..
 ... Success!


By default, a MariaDB installation has an anonymous user, allowing anyone
to log into MariaDB without having to have a user account created for
them.  This is intended only for testing, and to make the installation
go a bit smoother.  You should remove them before moving into a
production environment.

Remove anonymous users? [Y/n] y（删除匿名账户）
 ... Success!

Normally, root should only be allowed to connect from 'localhost'.  This
ensures that someone cannot guess at the root password from the network.

Disallow root login remotely? [Y/n] y（禁止管理员从远程登录）
 ... Success!

By default, MariaDB comes with a database named 'test' that anyone can
access.  This is also intended only for testing, and should be removed
before moving into a production environment.

Remove test database and access to it? [Y/n] y（删除测试数据库及其访问权限）
 - Dropping test database...
 ... Success!
 - Removing privileges on test database...
 ... Success!

Reloading the privilege tables will ensure that all changes made so far
will take effect immediately.

Reload privilege tables now? [Y/n] y（刷新授权表，让初始化后的设定立即生效）
 ... Success!

Cleaning up...

All done!  If you've completed all of the above steps, your MariaDB
installation should now be secure.

Thanks for using MariaDB!
```
在很多生产环境中都需要使用站库分离的技术（即网站和数据库不在同一个服务器上），如果需要让root管理员远程访问数据库，可在上面的初始化操作中设置策略，以允许root管理员从远程访问。然后还需要设置防火墙，使其放行对数据库服务程序的访问请求。数据库服务程序默认会占用3306端口，在防火墙策略中服务名称统一叫作mysql：
```bash
[root@hostname ~]# firewall-cmd --permanent --add-service=mysql
success
[root@hostname ~]# firewall-cmd --reload
success
```
一切准备就绪。现在我们将首次登录MariaDB数据库。管理数据库的命令为mysql，其中，-u参数用来指定以root管理员的身份登录，而-p参数用来验证该用户在数据库中的密码值。
```bash
[root@hostname ~]# mysql -u root -p
Enter password: 输入刚才设置的管理员密码后敲击回车
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 16
Server version: 10.3.11-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```
初次使用数据库管理工具的读者，可以输入help命令查看mariadb服务能做的操作，语句的用法与MySQL一模一样：
```bash
MariaDB [(none)]> help

General information about MariaDB can be found at http://mariadb.org

List of all MySQL commands:
Note that all text commands must be first on line and end with ';'
?         (\?) Synonym for `help'.
clear     (\c) Clear the current input statement.
connect   (\r) Reconnect to the server. Optional arguments are db and host.
delimiter (\d) Set statement delimiter.
edit      (\e) Edit command with $EDITOR.
ego       (\G) Send command to mysql server, display result vertically.
exit      (\q) Exit mysql. Same as quit.
go        (\g) Send command to mysql server.
help      (\h) Display this help.
nopager   (\n) Disable pager, print to stdout.
notee     (\t) Don't write into outfile.
pager     (\P) Set PAGER [to_pager]. Print the query results via PAGER.
print     (\p) Print current command.
prompt    (\R) Change your mysql prompt.
quit      (\q) Quit mysql.
rehash    (\#) Rebuild completion hash.
source    (\.) Execute an SQL script file. Takes a file name as an argument.
status    (\s) Get status information from the server.
system    (\!) Execute a system shell command.
tee       (\T) Set outfile [to_outfile]. Append everything into given outfile.
use       (\u) Use another database. Takes database name as argument.
charset   (\C) Switch to another charset. Might be needed for processing binlog with multi-byte charsets.
warnings  (\W) Show warnings after every statement.
nowarning (\w) Don't show warnings after every statement.

For server side help, type 'help contents'
```
在登录MariaDB数据库后执行数据库命令时，都需要在命令后面用分号（;）结尾，这也是与Linux命令最显著的区别。