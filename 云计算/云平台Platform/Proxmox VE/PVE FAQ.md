 **SMBus host controller not enabled**错误： PVE开机出现错误提示：`SMBus host controller not enabled`
原因： PVE装入i2c_piix4模块所致，因为系统找不到这个模块，所以报错。
处理方法：

1. 查询相关模块
```bash
$ sudo lsmod | grep piix4
i2c_piix4 24576 0
```

2. 禁用报错的模块
```bash
$ sudo vi /etc/modprobe.d/pve-blacklist.conf
	blacklist i2c_piix4
```

3. 重新生成引导文件，如果不进行该操作直接重启还是会报错！
```bash
$ sudo update-initramfs  -u  -k  all
```

4. 重启即可
```bash
$ reboot
```
