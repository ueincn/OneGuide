# xfce4-panel - Applications Menu
xfce4面板 - 应用程序菜单
The Applications Menu panel plugin adds a menu to the panel that allows easy access to all installed applications, organised into categories.
应用程序菜单面板插件向面板添加一个菜单，允许轻松访问所有已安装的应用程序，按类别组织。

#Link
- 官网文档：[https://docs.xfce.org/xfce/xfce4-panel/applicationsmenu](https://docs.xfce.org/xfce/xfce4-panel/applicationsmenu)
- 自定义 Xfce 菜单：[https://wiki.xfce.org/zh-cn/howto/customize-menu](https://wiki.xfce.org/zh-cn/howto/customize-menu)

# 配置文件
```bash
#Debian12 xfce4.18
/etc/xdg/menus/xfce-applications.menu #菜单主配置文件，定义了菜单名称等信息

/usr/share/desktop-directories/ #<Directory>下文件存放目录，定义了菜单图标、名称等信息
```
# 创建子菜单
## 整体步骤
- 创建一个新的子菜单, 添加一个 “Menu” 元素到 /etc/xdg/menus/xfce-applications.menu文件中和其他 xfdesktop 子菜单（比如“图像”，“多媒体”）相同的级别。
    - 在“Menu” 元素中添加一个 “Name” 元素：菜单名称
    - 再添加一个“Directory” 元素，它对关联子菜单和 desktop 文件，及一个相应的合适的图标
    - 再添加一个“Category” 元素，它关联 .desktop 文件和子菜单。建议自定义类别时使用“X-“开头，这是非标准的类别的前缀约定。
- 创建一个xxx.directory文件放到/usr/share/desktop-directories/目录中，定义了菜单图标、名称等信息。
- 创建自定义应用xxx.desktop文件放到/usr/share/applications中，确保字段和xfce-applications.menu中Category的字段一致即可,然后在启动菜单中就可以看到了。

## 实战示例
> KVM虚拟机启动脚本

1.添加一个 “Menu” 元素到 /etc/xdg/menus/xfce-applications.menu文件中
```bash
  <Menu>
    <Name>KVM</Name>
    <Directory>kvm.directory</Directory>
    <Include>
      <Category>kvm</Category>
    </Include>
  </Menu>
```
2.创建kvm.directory文件放到/usr/share/desktop-directories/目录中
```bash
[Desktop Entry]
    Version=1.0
    Type=Directory
    Icon=kvm
    Name=KVM
    Name[zh_CN]=KVM管理
    Comment=KVM manager
    Comment[zh_CN]=KVM管理
```
3.创建自定义应用xxx.desktop文件放到/usr/share/applications中,确保字段和xfce-applications.menu中Category的字段一致即可。
```bash
[Desktop Entry]
    Name=KVM Run
    Exec=/xx/xxx/KvmRun.sh %U
    StartupNotify=true
    Terminal=true
    Icon=kvm
    Type=Application
    Categories=kvm;
```