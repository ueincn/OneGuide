#### 软件安装
```bash
##Debian/Ubuntu
$ apt-get install open-iscsi -y

#RHEL/CentOS
$ yum -y install iscsi-initiator-utils

#配置程序：iscsiadm
#相关服务：iscsid.service
#配置文件目录：/etc/iscsi
```
#### 软件使用

**查看iqn**
```bash
$ cat /etc/iscsi/initiatorname.iscsi
```
**探测target端**
```bash
$ iscsiadm -m discovery -t st -p 192.168.0.100
$ iscsiadm --mode discovery -t sendtargets -p 192.168.0.100
192.168.0.100:3260,1 abc.id123.testsite.xyz:lun1
```
**查看进程**
```bash
$ sudo iscsiadm -m session -o show
tcp: [1] 192.168.1.29:3260,1 iqn.2020-07.com.sample:target1 (non-flash)
```
**登录到iSCSI server共享的分区**
```bash
$ sudo iscsiadm --mode node --targetname iqn.2018-09.com.example:server.target1 --portal 192.168.110.166:3260 --login
Logging in to [iface: default, target: iqn.2018-09.com.example:server.target1, portal: 192.168.110.166,3260] (multiple)
Login to [iface: default, target: iqn.2018-09.com.example:server.target1, portal: 192.168.110.166,3260] successful.
```
**物理机上加载target，建立连接**
```bash
#单个target加载命令：iscsiadm -m node -T targetname -p targetIP:port --login

iscsiadm -m node -T iqn.2099-01.cn.com.zte:usp.spr11-4c:09:b4:b0:5a:e8 -p 192.168.100.100:3260 -l
iscsiadm -m node -T iqn.2099-01.cn.com.zte:usp.spr11-4c:09:b4:b0:5b:42 -p 192.168.100.110:3260 -l

#设置重启后自动加载
iscsiadm -m node -T iqn.2099-01.cn.com.zte:usp.spr11-4c:09:b4:b0:5a:e8 -p 192.168.100.100:3260 --op update -n node.startup -v automatic
iscsiadm -m node -T iqn.2099-01.cn.com.zte:usp.spr11-4c:09:b4:b0:5b:42 -p 192.168.100.110:3260 --op update -n node.startup -v automatic

#断开所有 Target 连接：
iscsiadm -m node -U all

#刪除所有 node 信息 ( 需重新 discovery) ：
iscsiadm -m node --op delete

#查看会话信息：
iscsiadm -m session

#显示存储端target name
iscsiadm --mode node

#搜索ISCSI
iscsiadm -m discovery -t st -p 192.168.20.20:3260

#建立所有与Target的连接
iscsiadm -m node -L all

#多个target一起加载
#根据上面 discovery发现的多业务路径配置，将所有业务路径的target连接建立起来
iscsiadm -m node --loginall=all
```
**常用命令**
```bash
#发现存储设备：
#其中10.43.16.20为存储设备数据面IP地址
#登陆：
iscsiadm -m node -p 10.43.16.20:3260 -l 或 iscsiadm -m node -T iqn.2099-01.cn.com.zte:usp.spr11-00:00:22:33:44:15 -p 10.43.16.20:3260 -l 其中iqn.2099-01.cn.com.zte:usp.spr11-00:00:22:33:44:15为存储设备iqn

#查看存储设备：
iscsiadm -m node

#查看会话：
iscsiadm -m session

#查看会话详细信息：
iscsiadm -m session -P3

#登出/断开单条连接：
iscsiadm -m node -p 10.43.16.20:3260 -u

#删除单个会话节点：
iscsiadm -m node -p 10.43.16.20:3260 -o delete

#登出/断开所有连接：
iscsiadm -m node -u

#删除所有会话节点：
iscsiadm -m node -o delete

#扫描设备和会话：
iscsiadm -m node -p 10.43.16.20:3260 --rescan iscsiadm -m node --rescan iscsiadm -m session --rescan

#设置系统启动时自动登入：
iscsiadm -m node -T iqn.2099-01.cn.com.zte:usp.spr11-00:00:22:33:44:15 -p 10.43.16.20:3260 --op update -n node.startup -v automatic

#取消系统启动时自动登入：
iscsiadm -m node -T iqn.2099-01.cn.com.zte:usp.spr11-00:00:22:33:44:15 -p 10.43.16.20:3260 --op update -n node.startup -v manual

#配置文件：/etc/iscsi/iscsid.conf
#node.conn[0].timeo.login_timeout = 15
#node.conn[0].timeo.logout_timeout = 15
#node.session.initial_login_retry_max = 8
#iscsi登陆超时时间为node.conn[0].timeo.login_timeout * node.session.initial_login_retry_max
#那么默认登陆超时时间为 15*8=120s。
#当磁阵数据面链路异常时，会影响挂载云盘时间，可修改登陆超时时长和尝试登陆次数来缩短挂载云盘时间。
#node.session.timeo.replacement_timeout = 120
#当磁阵数据面链路异常时，session状态会发生切换。session正常状态为loggen_in，故障态为failed和free。 切换到failed为10s，再切换到free为120s（node.session.timeo.replacement_timeout）。
#在修改iSCSI的配置文件后，重启iSCSI服务或重启主机都不会使配置生效，必须把当前的iSCSI会话logout后，将iSCSI已经发现的目标节点删除掉，重启iscsi服务，再重新发现目标节点，建立iSCSI会话
```