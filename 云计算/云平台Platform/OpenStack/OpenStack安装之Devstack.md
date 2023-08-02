DevStack 是一组脚本和实用程序，用于从git源代码树快速部署 OpenStack云。
### Links

- GitHub：[https://github.com/openstack/devstack/](https://github.com/openstack/devstack/)
- OpenDev：[https://opendev.org/openstack/devstack](https://opendev.org/openstack/devstack)
- OpenStackWiki：[https://docs.openstack.org/devstack/latest/](https://docs.openstack.org/devstack/latest/)
- Blog：
   - [使用devstack安装部署OpenStack（据详细手把手教学）_专业烧板子的博客-CSDN博客](https://blog.csdn.net/woaikeji/article/details/123772104)\
   - [使用 Devstack 搭建 Openstack 开发环境](https://www.xiexianbin.cn/openstack/devstack/index.html#%E5%AE%89%E8%A3%85)
   - [DevStack-深入理解 OpenStack 自动化部署-面试哥](https://www.mianshigee.com/tutorial/deployopenstackwithpuppet/deployment_tool-devstack.md)
   - [其他部署工具 - DevStack - 《深入理解 OpenStack 自动化部署》 - 书栈网 · BookStack](https://www.bookstack.cn/read/deployopenstackwithpuppet/deployment_tool-devstack.md)
   - [使用devstack在单机上安装openstack(stein版本)和zun的踩坑之路 – heyin](https://www.he-yin.cn/archives/devstackinstall)
   - [Ubuntu 20.04 搭建OpenStack Yoga（allinone）-腾讯云开发者社区-腾讯云](https://cloud.tencent.com/developer/article/2166973)
   - [Devstack真实环境搭建OpenStack](http://www.taodudu.cc/news/show-3708640.html?action=onClick)

---

### 安装
Devstack 搭建 Openstack 开发环境```bash
#换源
#软件源根据使用的发行版安装开源镜像站中的使用帮助替换即可！

#pip换源
$ cd ~             
$ mkdir .pip      
$ vim .pip/pip.conf
# pip 清华源
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
[install]
trusted-host = https://pypi.tuna.tsinghua.edu.cn
```
```bash
#安装基础环境
$ sudo apt-get install python3-pip vim git
```
```bash
#创建stack账户并设置密码，添加sudo权限并切换用户
$ sudo useradd -s /bin/bash -d /opt/stack -m stack
$ sudo passwd stack
$ echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack
$ sudo su - stack
```
```bash
#下载devstack源码并切换要安装的openstack版本分支
$ git clone https://opendev.org/openstack/devstack stable/yoga #指定yoga版本
$ cd devstack
```
```bash
#创建并配置local.conf
[[local|localrc]]
ADMIN_PASSWORD=secret
DATABASE_PASSWORD=$ADMIN_PASSWORD
RABBIT_PASSWORD=$ADMIN_PASSWORD
SERVICE_PASSWORD=$ADMIN_PASSWORD

#修改OpenStack源码地址
GIT_BASE=http://git.trystack.cn
```
```bash
#安装
$ ./stack.sh
```

---

### FAQ
问题一：**ERROR keystone oslo_db.exception.DBConnectionError: (pymysql.err.OperationalError) (2003, "Can't connect to MySQL server on 'LAB@127.0.0.1' ([Errno -2] Name or service not known)")**#### Link

- [https://www.cnblogs.com/czp2016/p/15343486.html](https://www.cnblogs.com/czp2016/p/15343486.html)
#### 原因
`/etc/keystone/keystone.conf` 数据库端口未配置
#### 解决
数据库正确配置格式：`engine("mysql+pymysql://{user}:{password}@{host}:{port}/ajx?charset=utf8".format(**config))`
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1687088777365-65aae5bb-82a2-4986-b597-b8e045a6c388.png#averageHue=%23222120&clientId=ubd9c06aa-f710-4&from=paste&id=u1f6f8af8&originHeight=114&originWidth=782&originalType=url&ratio=1.25&rotation=0&showTitle=false&size=7503&status=done&style=none&taskId=u0623e1da-0ed9-4bad-85c8-6012f167d5f&title=)
问题二：**AttributeError: 'EntryPoints' object has no attribute 'get'**版本过高原因，试着降低版本。
先卸载importlib-metadata
`pip3 uninsatll importlib-metadata`
再安装制定版本importlib-metadata
`pip3 install importlib-metadata==4.13.0`
问题三：**You are using pip version 9.0.3,howerver version 18.1 is available pip更新到18.1之后安装stack又回到pip 9.0+版本**问题描述：You are using pip [version](https://so.csdn.net/so/search?q=version&spm=1001.2101.3001.7020) 9.0.3,howerver version 18.1 is available
使用命令 sudo pip install –upgrade pip 到了18.1,但是执行stack.sh又回到了9.0.3
原因：由于原因是安装中会检查版本，不在规定的范围内，就会重新安装，后面又需要最新版导致无限循环
解决方法一：vi /home/devstack/tools/cap-pip.txt
显示 pip!=8,<10 将 ,<10 删除就可以了，或直接整条注释掉。
方法二：devstack/tools目录下，找到install_pip.py，或者是ipstall_pip.sh, 找到并注释掉install_get_pip这个函数调用，就OK了。
问题四：**neutron CLI is deprecated and will be removed in the future. Use openstack CLI instead. Auth plugin requires parameters which were not given: auth_url**openstack命令 neutron net-list 报错：neutron CLI is deprecated and will be removed in the future. Use openstack CLI instead. Auth plugin requires parameters which were not given: auth_url
解决方法
修改admin-openrc.sh文件，设置export OS_PASSWORD=XXX
问题五：**Job for devstack@etcd.service failed because the control process exited with error code. See “systemctl status devstack@etcd.service” and “journalctl -xe” for details.**stack.sh.log 报错：Job for devstack@etcd.service failed because the control process exited with error code. See “systemctl status devstack@etcd.service” and “journalctl -xe” for details.
解决方法
修改local.conf，添加一行
```bash
disable_service etcd3 
```

问题六：**AttributeError: module ‘lib‘ has no attribute ‘OpenSSL_add_all_algorithms’**[Error Updating Python3 pip AttributeError: module ‘lib’ has no attribute ‘OpenSSL_add_all_algorithms’](https://stackoverflow.com/questions/74981558/error-updating-python3-pip-attributeerror-module-lib-has-no-attribute-openss)
原文的解释：The error is a result of incompatibility between cryptography and pyopenssl, so if possible, also upgrading to openssl>22.1.0 should work
cryptography和pyopenssl两个模块之间不兼容导致了这个问题，因此降低cryptography的版本就可以了
```bash
#先删除
pip uninstall cryptography
#再安装
pip install cryptography==38.0.4
```
问题七：**/stac.sh:191 if you wish to run this script anyway run with FORCE=yes /home/dexstack/functions-commom:232: /opt/stack/logs/error.log:No such file or directory**#解决方案：
```bash
$FORCE=yes ./stack.sh
```
