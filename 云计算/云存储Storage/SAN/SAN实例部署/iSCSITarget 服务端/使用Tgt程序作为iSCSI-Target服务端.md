#### 软件安装
```bash
#Debian/Ubuntu
$ sudo apt-get install tgt

#CentOS
#守护程序：tgtd
$ yum install -y scsi-target-utils

#如执行上面命令提示没有安装包，可添加epel源再安装
$yum install epel-release
$yum --enablerepo=epel -y install scsi-target-utils
```
#### 软件使用

守护程序： `tgt` 或 `tgtd`
配置文件路径：`/etc/tgt/ `
自定义配置文件路径：`/etc/tgt/conf.d/`
在线查询、删除target等功能命令：`/usr/sbin/tgt-admin`
主要提供iSCSI target服务的主程序：`/usr/sbin/tgt` 或 `/usr/sbin/tgtd`

配置说明：
- target：后面为节点名称，随便写
- backing-store：虚拟设备
- direct-store：实际设备
  - 设定的时候，如果把整块磁盘全部拿来使用可以使用配置direct-store，反之使用backing-store
  - 使用backing-store，计划在今后的生产环境中使用LVM逻辑卷，那么这里的配置还是应该使用backing-store\
- initiator-address：用户端地址，即可以允许连接的IP地址或地址范围
- incominguser username password：设置连接用户和密码，可以设定initiator使用账户密码才可以使用对应target 
- write-cache off/on：是否开启写入缓存，开启on/关闭off

##### 示例
```bash
$ sudo touch /etc/tgt/conf.d/iscsi.conf

<target iqn.2023-06.cn.uefire.www:imagestore>
     backing-store /dev/sdb
     initiator-address 168.17.0.0/16
     incominguser root kylin-999
</target>
```
```bash
$ sudo systemctl status tgt #查看tgt服务状态
$ sudo systemctl restart tgt #重启tgt服务
$ sudo systemctl enable tgt #配置开机自启
$ sudo tgtadm --mode target --op show #查看配置状态，debian
$ sudo tgt-admin --show
```
```bash
$ tgtadm --mode target --op show
Target abc.id123.testsite.xyz:lun1
    System information:
        Driver: iscsi
        State: ready
    I_T nexus information:
    LUN information:
        LUN: 0
            Type: controller
            SCSI ID: IET     00010000
            SCSI SN: beaf10
            Size: 0 MB, Block size: 1
            Online: Yes
            Removable media: No
            Prevent removal: No
            Readonly: No
            SWP: No
            Thin-provisioning: No
            Backing store type: null
            Backing store path: None
            Backing store flags: 
        LUN: 1
            Type: disk
            SCSI ID: IET     00010001
            SCSI SN: beaf11
            Size: 2146 MB, Block size: 512
            Online: Yes
            Removable media: No
            Prevent removal: No
            Readonly: No
            SWP: No
            Thin-provisioning: No
            Backing store type: rdwr
            Backing store path: /dev/sdb
            Backing store flags: 
    Account information:
        test
        test (outgoing)
    ACL information:
        192.168.0.0/16
```