### 创建
**创建虚拟机**
**创建CT**
### 镜像
**使用qcow2镜像**

#### 整体步骤

1. 下载Cloud Images；
2. 把Cloud Images导入到PVE系统存储目录中；
3. PVE中创建VM，并移出CD/DVD，然后添加Cloud-Init设备；
4. 为PVE中VM导入Cloud Images；
5. 启用硬件，并设置引导顺序；
6. 配置Cloud-Init；
7. VM开机使用；
8. 配置启用root账户ssh登录；
9. VM转换成模板，链接或完整克隆使用。
#### Cloud Images下载地址 

- centos：[http://cloud.centos.org/centos/](http://cloud.centos.org/centos/)
- ubuntu：[http://cloud-images.ubuntu.com/releases/](http://cloud-images.ubuntu.com/releases/)
- debian：[https://cloud.debian.org/images/cloud/OpenStack/](https://cloud.debian.org/images/cloud/OpenStack/)

---

1. **下载Cloud Images**

建议wget直接下载到PVE系统中，这样就可以不用使用scp等其他方式传入。

2. **Cloud Images导入到PVE系统**

如果未使用wget方式下载，可以使用scp，ftp等工具传到PVE系统目录存储中。
local和local-lvm对应PVE系统目录：
`local`：/var/lib/vz/image/iso/
`local-lvm`：/var/lib/vz/images/

3. **PVE中创建VM，并修改硬件，然后添加Cloud-Init设备；**
- **创建VM**
   - 常规：默认
   - 操作系统：不使用任何介质
   - 系统：勾选QEMU代理，VirtIO SCSI
   - 磁盘：默认（等下要删除）
   - CPU：默认
   - 内存：默认
   - 网络：默认
   - 确认：完成
- 修改硬件
   - 分离并删除硬盘
   - 删除CD/DVD驱动器
   - 添加Cloud-init设备 
4. **为PVE中VM导入Cloud Images；**
```bash
$ qm importdisk 1001 /var/lib/vz/images/xxxxx.qcow2 local-lvm --format=qcow2

# 1001：创建VM时的ID
#/var/lib/vz/images/xxxxx.qcow2：Cloud Images镜像的绝对路径
#local-lvm：PVE存储库
#--format=qcow2：类型qcow2，如果镜像后缀本来就是qcow2后缀就没必要用这个选项。
```

5. **启用硬件，并设置引导顺序；**
- 此时在VM的硬件中有一块未使用磁盘，双击并启用即可；
- VM的选项中，勾选刚刚启用的那一块硬盘，网络引导就取消吧没有用了。
6. **配置Cloud-Init；**
- 用户：root（必须要填）
- 密码：自行设置
- DNS域：即DNS1
- DNS服务器：即DNS2
- IP配置：static/DHCP
7. **VM开机使用；**
- 开机使用。
8. **配置启用root账户ssh登录；**
- `vi /etc/ssh/sshd_config`
修改 PermitRootLogin yes
修改 PasswordAuthentication yes
9. **VM转换成模板，链接或完整克隆使用。**
- 关机，然后右键机器点击转换成模板。
**使用CT模板****前提：修改 CT Templates (LXC 容器)源**

- 将 `/usr/share/perl5/PVE/APLInfo.pm` 文件中默认的源地址 http://download.proxmox.com 替换为 https://mirrors.tuna.tsinghua.edu.cn/proxmox 即可。

可以使用如下命令修改：
```bash
cp /usr/share/perl5/PVE/APLInfo.pm /usr/share/perl5/PVE/APLInfo.pm_back
sed -i 's|http://download.proxmox.com|https://mirrors.tuna.tsinghua.edu.cn/proxmox|g' /usr/share/perl5/PVE/APLInfo.pm
```

- 针对 `/usr/share/perl5/PVE/APLInfo.pm `文件的修改，重启后生效。
```bash
systemctl restart pvedaemon.service
```
### 使用WEB下载LXC模板
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1682253256223-657d14b8-bce1-49a0-abfa-89599bbfcc61.png#averageHue=%23292828&clientId=u104646c1-3f6a-4&from=paste&height=726&id=ua69c5985&originHeight=1270&originWidth=2089&originalType=binary&ratio=1.75&rotation=0&showTitle=false&size=273574&status=done&style=none&taskId=ud4ebe7fb-a986-47fb-a654-ea32fe2fdf5&title=&width=1193.7142857142858)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1682253281817-cb77d86d-6d3c-4456-9f16-f852748f1a4b.png#averageHue=%232a2929&clientId=u104646c1-3f6a-4&from=paste&height=662&id=uaa95a907&originHeight=1158&originWidth=1639&originalType=binary&ratio=1.75&rotation=0&showTitle=false&size=174754&status=done&style=none&taskId=u9b0f6243-72a0-42d1-8b97-3fbb5d61d70&title=&width=936.5714285714286)
### 使用命令行下载LXC模板
```bash
$ pveam available #查看所有可用模板
$ pveam available --section system #查看所有可用系统模板
$ pveam available --section turnkeylinux #查看所有可用应用模板
$ pveam download local debian-9-turnkey-tomcat_15.1-1_amd64.tar.gz #下载模板到存储，如下载tomcat15到local：
$ pveam list local #查看存储local中的模板
```
### 磁盘
**PVE 磁盘扩容****步骤：（关机状态）**选中VM — 硬件 — 硬盘 — 磁盘操作 — 调整大小
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1682250213005-079518fc-cf81-4497-8e19-1a7863486801.png#averageHue=%23313130&clientId=u104646c1-3f6a-4&from=paste&height=391&id=u36270d0c&originHeight=782&originWidth=2031&originalType=binary&ratio=1.75&rotation=0&showTitle=false&size=162607&status=done&style=none&taskId=u1a9484f3-103f-48f2-bc6b-af114333fda&title=&width=1016)
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1682250239694-79b3ec3d-699e-406f-8c55-0a5640b7e982.png#averageHue=%23282828&clientId=u104646c1-3f6a-4&from=paste&height=464&id=u13f097d6&originHeight=812&originWidth=2025&originalType=binary&ratio=1.75&rotation=0&showTitle=false&size=90888&status=done&style=none&taskId=u20775c13-787e-4550-9310-844dbdd1de6&title=&width=1157.142857142857)
![屏幕截图 2023-04-23 195701.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1682251088789-73c97f92-7c8f-4625-9977-0bcee5825fd0.png#averageHue=%23161616&clientId=u104646c1-3f6a-4&from=paste&height=424&id=u30fa6b4d&originHeight=742&originWidth=1469&originalType=binary&ratio=1.75&rotation=0&showTitle=false&size=112442&status=done&style=none&taskId=u22b35ccc-b37e-4431-b4e4-e73d10408c1&title=&width=839.4285714285714)
### 软件镜像源
修改 CT Templates (LXC 容器)源
- 将 `/usr/share/perl5/PVE/APLInfo.pm` 文件中默认的源地址 http://download.proxmox.com 替换为 https://mirrors.tuna.tsinghua.edu.cn/proxmox 即可。

可以使用如下命令修改：
```bash
cp /usr/share/perl5/PVE/APLInfo.pm /usr/share/perl5/PVE/APLInfo.pm_back
sed -i 's|http://download.proxmox.com|https://mirrors.tuna.tsinghua.edu.cn/proxmox|g' /usr/share/perl5/PVE/APLInfo.pm
```

- 针对 `/usr/share/perl5/PVE/APLInfo.pm `文件的修改，重启后生效。
```bash
systemctl restart pvedaemon.service
```
更换Turnkeylinux源
- turnkey Linux 镜像服务器列表：[https://www.turnkeylinux.org/mirrors](https://www.turnkeylinux.org/mirrors)
- 中科大镜像地址为例：[https://mirrors.ustc.edu.cn/turnkeylinux/](https://mirrors.ustc.edu.cn/turnkeylinux/)

---

1. 备份`/usr/share/perl5/PVE/APLInfo.pm`： 
```bash
$ sudo cp /usr/share/perl5/PVE/APLInfo.pm /usr/share/perl5/PVE/APLInfo.pm_backup
```

2. 修改/usr/share/perl5/PVE/APLInfo.pm中的为：
```bash
    {
        host => "mirrors.ustc.edu.cn",
        url => "https://mirrors.ustc.edu.cn/turnkeylinux/metadata/pve",
        file => 'aplinfo.dat',
    },
```

3. 执行`pveam update`更新turnkeylinux源。
