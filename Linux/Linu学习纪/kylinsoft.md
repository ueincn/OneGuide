
麒麟操作系统（Kylin OS）亦称银河麒麟，是由中国国防科技大学、中软公司、联想公司、浪潮集团和民族恒星公司合作研制的商业闭源服务器操作系统，于2001年开始使用，此操作系统是863计划重大攻关科研项目，目标是打破国外操作系统的垄断，研发一套中国自主知识产权的服务器操作系统，该系统有高安全、跨平台、中文化的特点。2010年12月16日，两大国产操作系统（民用的“中标Linux”操作系统和解放军研制的“银河麒麟”操作系统）在上海正式宣布合并，双方共同以“中标麒麟”的新品牌统一出现在市场上。

银河麒麟桌面操作系统 V10

银河麒麟桌面 V10 是一款面向桌面应用的图形化操作系统，其大幅度优化桌面空间，提供丰富的系统环境及应用工具，使桌面办公更加高效，项目开发更加 流畅，通过硬件差异屏蔽、软件接口封装，保证了各国产处理器平台下使用体验 和环境的一致性。银河麒麟桌面 V10 提供了更好的硬件兼容性，支持更多有线和无线网卡、新 型号显卡以及 20 多万款外设，包括打印机、扫描仪、投影仪、摄像头、4K 高清屏、触摸屏等各类外部设备和特种设备。此外，银河麒麟桌面 V10 配备了完善的开发工具，提供了良好的开发环境， 支持主流编程语言，并提供了大量的开发库，同时支持国产数据库和中间件，封 装系统级 SDK，更好地支撑项目的开发工作。  

银河麒麟高级服务器操作系统V10是针对企业级关键业务，适应虚拟化、云计算、大数据、人工智能、工业互联网时代对主机系统可靠性、安全性、高性能、扩展性和实时性的需求，依据等保四级标准研制，研制过程符合CMMI 5 级管理体系，提供内生安全、云原生支持、自主平台深入优化、高性能、易管理的新一代自主服务器操作系统；同源支持飞腾、龙芯、兆芯、海光、申威、鲲鹏等自主平台；可支撑构建大型数据中心服务器高可用集群、负载均衡集群、分布式集群文件系统、虚拟化应用和容器云平台等，可部署在物理服务器和虚拟化环境、私有云、公有云和混合云环境；广泛应用于政府、财税、审计、能源、金融、交通、教育、医疗、制造等领域。


银河麒麟桌面操作系统V4 是天津麒麟信息技术有限公司开发的操作系统，操作界面美观、大方，使用方便，普通用户更容易上手。目前，银河麒麟桌面操作系统及相关软硬件产品和解决方案已经在政务、电力、金融、国防、军工、电信、能源、交通、邮政、教育等行业中得到了广泛应用，公司将进一步联合其他芯片、整机、数据库、中间件、应用软件和系统集成企业，共建安全可控信息系统的示范基地及生态。

中标麒麟高级服务器操作系统软件 V7.0是麒麟软件基于Linux Kernel等上游社区开源技术，融合麒麟长期积累的安全技术能力，提供内生安全、云原生支持、自主平台深入优化、高性能、易管理的，完全兼容Intel平台及RHEL/CentOS 7 生态的商业发行版操作系统。可靠性方面同银河麒麟高级服务器操作系统V10一样获得了国际电信级Linux最高认证（CGL5.0），生态方面兼容Oracle、VMware等国外厂商并获得国内操作系统独家互认证，历年来已广泛应用于金融、电信、能源、交通、央企等重点行业。借助批量迁移平台以及长期积累的覆盖全国的技术服务，中标麒麟高级服务器操作系统软件 V7.0完全具备替代CentOS7的能力，是存量场景下CentOS停服应对的最佳解决方案。


---

#### V10-SP1开放 root 登录
```bash
$ sudo vim /usr/share/lightdm/lightdm.conf.d/95-ukui-greeter.conf 
[Seat:*]
greeter-session=ukui-greeter
user-session=ukui
greeter-show-manual-login=true


$ sudo vim /usr/share/lightdm/lightdm.conf.d/50-disable-guest.conf
[Seat:*]
allow-guest=false

$ sudo systemctl restart lightdm
```


#### KylinDesktop：V10-SP1延迟登录
```bash
$ sudo vim /usr/share/lightdm/lightdm.conf.d/95-ukui-greeter.conf 
[Seat:*]
session-setup-script=sleep 20    #登录界面输入密码后等待20s后显示桌面
display-setup-script=sleep 20    #系统启动完成之后等待20s后显示登录界面
```


#### KylinDesktop：V10-SP1隐藏单个用户
```bash
$ sudo cd /var/lib/AccountsService/users/
$ sudo vim username

[User]
SystemAccount=false    #默认为false，如需隐藏改成true
```


#### KylinDesktop：V10-SP1免密登录
```bash
#将用户添加到nopasswdlogin组，xxx为用户名
$ sudo gpasswd -a xxxx nopasswdlogin

#查看是否添加成功
$ cat /etc/group grep nopass

#注销重新登录即可免密登录
```

---
#### KylinDesktop：KVM/QEMU安装
```bash
sudo apt-get install qemu-kvm qemu-utils qemu-system libvirt-daemon-system libvirt-clients bridge-utils virt-manager
```

#### 安装软件
- Neofetch
> 在终端中显示 Linux 系统信息
```bash
sudo apt-get install neofetch
```