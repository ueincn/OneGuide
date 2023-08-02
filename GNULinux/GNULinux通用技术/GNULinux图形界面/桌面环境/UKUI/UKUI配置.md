### 锁屏壁纸
```bash
#路径
/usr/share/ukui-greeter/images/background-ubuntu.png

#修改
$ sudo vim /etc/lightdm/ukui-greeter.conf
    # Background file to use, either an image path or a color
    background=/usr/share/ukui-greeter/images/background-ubuntu.png
    # Background color
    background-color=#035290
```
### 锁屏程序
```bash
$ cat /usr/share/lightdm/lightdm.conf.d/95-ukui-greeter.conf
[Seat:*]
greeter-session=ukui-greeter
user-session=ukui
```