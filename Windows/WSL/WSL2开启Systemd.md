如果需要使用微软官方支持的systmed，在目前来说需要满足这些前置条件：

1. 操作系统为windows 11 
2. wsl 版本为 0.67.6 或以上（目前均为预览版本）。

查看wsl版本号命令为：`wsl --version`
（如果此命令未正常回显版本号，或版本号低于0.67.6，那么你安装的wsl还不支持systemd。）
```powershell
PS C:\Users\wq> wsl --version
WSL 版本： 1.1.3.0
内核版本： 5.15.90.1
WSLg 版本： 1.0.49
MSRDC 版本： 1.2.3770
Direct3D 版本： 1.608.2-61064218
DXCore 版本： 10.0.25131.1002-220531-1700.rs-onecore-base2-hyp
Windows版本： 10.0.22000.1574
```

在WSL里操作：
```bash
#配置wsl启用 systemd
$ echo -e "[boot]\nsystemd=true" | sudo tee -a /etc/wsl.conf

#关闭wsl，来进行wsl的完整重启。
$ wsl --shutdown

#判断systemd是否启用成功
$ ps --no-headers -o comm 1
$ systemctl list-unit-files --type=service
```