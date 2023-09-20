1. 配置 kvm-intel
```bash
$ sudo vim /etc/modprobe.d/kvm-nested.conf
```
以下信息填入kvm-nested.conf
```bash
options kvm-intel nested=1
options kvm-intel enable_shadow_vmcs=1
options kvm-intel enable_apicv=1
options kvm-intel ept=1
```
2. 最新微软商店里的Linux发行版使用的内核默认开启KVM支持，可以su - 切换到root环境下，输入kvm-ok查看：
```bash
root@DESKTOP:~# kvm-ok
INFO: /dev/kvm exists
KVM acceleration can be used
# 这样显示就代表已支持KVM特性。
# 如未返回任何信息，可安装链接中的方法开启：https://boxofcables.dev/accelerated-kvm-guests-on-wsl-2/
```
3. 检查嵌套的 KVM
```bash
$ cat /sys/module/kvm_intel/parameters/nested
```
应报告“Y”
4. 开启后就可以使用KVM了。