默认情况下，MySQL服务器仅监听来自本地主机的连接，这意味着它只能由运行在同一主机上的应用程序访问。

但是，在某些情况下，有必要从远程位置访问MySQL服务器。例如，当您想从本地系统连接到远程MySQL服务器时。

或者当使用多服务器部署时，应用程序与数据库服务器不在同一台计算机上运行。

一种选择是[通过SSH隧道访问MySQL服务器](https://www.myfreax.com/mysql-ssh-tunnel/)，另一种是将MySQL服务器配置为接受远程连接。

## 配置MySQL服务器

第一步是设置MySQL服务器监听计算机所有IP地址。如果MySQL服务器和客户端可以通过专用网络相互通信，那么最好的选择是将MySQL服务器设置为仅在指定IP上监听。

如果要通过公共网络连接到MySQL服务器，请将MySQL服务器设置为监听计算机上的所有IP地址。

因此，您需要编辑MySQL配置文件并添加或更改`bind-address`选项的值。您可以设置一个IP地址和IP范围。

如果地址为`0.0.0.0`，则MySQL服务器接受所有远程主机IPv4接口上的连接。如果你需要使用IPv6，请使用`::`代替`0.0.0.0`。

MySQL配置文件的位置因Linux发行版而异。在Ubuntu和Debian中，文件位于`/etc/mysql/mysql.conf.d/mysqld.cnf`，而在基于Red Hat的发行版（如CentOS）中，文件位于`/etc/my.cnf`。

使用文本编辑器打开文件`/etc/mysql/mysql.conf.d/mysqld.cnf`文件：

```bash
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```

搜索以`bind-address`开头的行，并将其值设置为MySQL服务器应监听的IP地址。默认情况下，该值设置为`127.0.0.1`即仅在本地主机中监听。

如将值更改为`0.0.0.0`，将MySQL服务器设置为监听所有IPv4地址。

```bash
bind-address = 0.0.0.0
# skip-networking
```

在MySQL 8.0和更高版本中，`bind-address`指令可能不存在。在这种情况下，请将`bind-address = 0.0.0.0`其添加到`[mysqld]`下。

完成后，重新启动MySQL服务以使更改生效。在现代的Linux发行版中，MySQL通常使用systemd的服务在后台运行，因此可以使用systemctl命令重启MySQL服务

只有root用户或具有sudo权限的用户才能重新启动MySQL服务。要在Debian或Ubuntu上重新启动MySQL服务。

在基于RedHat的发行版上，例如CentOS/Fedora。MySQL服务名称是mysqld。

```bash
sudo systemctl restart mysql
sudo systemctl restart mysqld
```

## 允许从远程计算机访问

下一步是允许远程用户访问数据库。首先以root用户登录到MySQL服务器。运行命令`sudo mysql`。

如果您使用本地MySQL身份验证插件以root用户身份登录，请运行`mysql -uroot -p`命令并在出现提示时输入密码。

在MySQL Shell中，使用`GRANT`语句为用户授予远程访问权限。

```bash
sudo mysql
mysql -uroot -p
```

```sql
GRANT ALL ON database_name.* TO user_name@'ip_address' IDENTIFIED BY 'user_password';
```

其中`database_name`是用户将连接到的数据库的名称。`user_name`是MySQL用户的名称。

`ip_address`是用户本地计算机的[IP地址](https://www.myfreax.com/how-to-find-ip-address-linux/)。使用`%`允许用户从任何IP地址进行连接。`user_password`是用户密码。

例如，仅允许IP是`10.8.0.5`的客户端使用密码`my_passwd`和用户名为`foo`访问数据库`dbname`，请运行以下命令，如需允许所有IP，请使用`%`代替IP地址。

```shell
GRANT ALL ON dbname.* TO foo@'10.8.0.5' IDENTIFIED BY 'my_passwd';
```

## 配置防火墙

最后一步是配置防火墙，以允许来自远程计算机到MySQL默认端口`3306`上的连接。

如果你使用iptables作为防火墙，则下面的命令将允许从Internet上的所有IP地址访问MySQL端口。但这通常是不建议使用。

你也可以使用第二个命令设置仅允许从指定的IP地址访问，iptables的`-s`选项表示源IP地址， `--destination-port`表示目标端口， `-p tcp`表示所有TCP连接。

```shell
sudo iptables -A INPUT -p tcp --destination-port 3306 -j ACCEPT

sudo iptables -A INPUT -s 10.8.0.5 -p tcp --destination-port 3306 -j ACCEPT
```

> UFW是Ubuntu中的默认防火墙工具。要允许从Internet上的任何IP地址访问，请运行，我们不建议使用此防火墙规则。

同样你也可以设置为允许从指定的IP地址访问。`from 10.8.0.5` 表示源ip地址。

```shell
sudo ufw allow 3306/tcp

sudo ufw allow from 10.8.0.5 to any port 3306
```

> FirewallD是CentOS中的默认防火墙管理工具。可以允许从Internet上的任何IP地址访问，但不建议使用此防火墙规则。

```shell
sudo firewall-cmd --permanent --zone=public --add-port=3306/tcp
sudo firewall-cmd --reload
```

要仅允许从指定IP地址进行访问，您可以创建新的FirewallD区域和规则。`--new-zone=mysqlzone`命令将创建一个名为`mysqlzone`的新区域和规则。

```shell
sudo firewall-cmd --new-zone=mysqlzone --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --permanent --zone=mysqlzone --add-source=10.8.0.5/32
sudo firewall-cmd --permanent --zone=mysqlzone --add-port=3306/tcp
sudo firewall-cmd --reload
```

## 验证更改

要验证远程用户是否可以连接到MySQL服务器，可以运行命令`mysql -u user_name -h mysql_server_ip -p`。

其中`user_name`是您授予远程访问权限的用户名，`mysql_server_ip`是运行MySQL服务器的主机的IP地址。如果一切设置正确，您将能够登录到远程MySQL服务器。

如果收到类似以下的错误，则说明[端口3306未打开](https://www.myfreax.com/check-open-ports-linux/)，或者MySQL服务器未[监听IP地址](https://www.myfreax.com/check-listening-ports-linux/)。ERROR 2003 \(HY000\): Can't connect to MySQL server on '10.8.0.5' \(111\)"

"ERROR 1130 \(HY000\): Host ‘10.8.0.5’ is not allowed to connect to this MySQL server"。错误表示您尝试登录的用户无权访问远程MySQL服务器。

## 结论

MySQL是最流行的开源数据库服务器，默认情况下仅在本地主机上监听传入的连接。

要允许远程连接到MySQL服务器，您需要配置MySQL服务器以监听全部或指定定IP地址。授予对远程用户的访问权限。