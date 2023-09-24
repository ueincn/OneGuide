#### 开机显示 dev sda1 clean,xxxxx xxxxx files,xxxxx xxxxx blocks

**解决方法**
1. 修改grub
```bahs
$ sudo vim /etc/default/grub 	
	GRUB_CMDLINE_LINUX_DEFAULT="" #把值清空即可；（quiet）：安静模式
$ sudo update-grup 
$ sudo reboot
```
2. 修改initramfs
这类信息有两种：
- initramfs 阶段的输出：（行首没有 systemd-fsck）
- /dev/sda1: clean, 131838/991232 files, 1193255/3933482 blocks
可修改 initramfs 将其移除，具体做法待查。
