Xfce 是一个提供全功能桌面环境的程序集。
以下程序是 Xfce 核心的部分：

- 窗口管理器 (xfwm4)：处理窗口在屏幕上的位置摆放
- 面板 (xfce4-panel)：程序启动器、窗口按钮、应用程序菜单、工作区切换器等等。
- 桌面管理器 (xfdesktop)：设置背景的颜色或图片，可选应用程序菜单或最小化应用程序、启动器、设备文件夹的图标。
- 文件管理器 (thunar)：一个 Unix/Linux 桌面平台上的现代文件管理器，旨在易用和快速。
- 卷管理器 (thunar-volman)：Thunar 可移动驱动器和介质的自动管理
- 会话管理器 (xfce4-session)：在桌面启动时恢复您的会话并让您从 Xfce 关闭计算机。
- 设置系统 (xfce4-settings)：控制桌面的如外观、显示、键盘和鼠标设置各个方面的配置系统。
- 应用程序查找器 (xfce4-appfinder)：分类显示在您系统上安装的应用程序，这样您就可以快速地查找和启动它们。
- 设置守护进程 (xfconf)：基于 D-Bus 的配置存储系统。
- 菜单库 (garcon)：基于 GLib 和 GIO 的 freedesktop.org 兼容菜单实现。
- 缩略图服务 (tumbler)：缩略图服务实现缩略图管理 D-Bus 规范。

Xfce 还是一个提供若干库文件，帮助程序员创建适合桌面环境的应用程序之开发平台。
Xfce 组件以自由或开源许可协议授权；应用程序以 GPL 或 BSDL，库文件以 LGPL 或BSDL 授权。浏览文档、源代码或 Xfce 站点(https://www.xfce.org) 以获取详情。

---
# xfce4-panel
- 面板插件：[https://docs.xfce.org/panel-plugins](https://docs.xfce.org/panel-plugins)
## xfce4-panel - Applications Menu
xfce4面板 - 应用程序菜单
The Applications Menu panel plugin adds a menu to the panel that allows easy access to all installed applications, organised into categories.
应用程序菜单面板插件向面板添加一个菜单，允许轻松访问所有已安装的应用程序，按类别组织。

Link
- 官网文档：[https://docs.xfce.org/xfce/xfce4-panel/applicationsmenu](https://docs.xfce.org/xfce/xfce4-panel/applicationsmenu)
- 自定义 Xfce 菜单：[https://wiki.xfce.org/zh-cn/howto/customize-menu](https://wiki.xfce.org/zh-cn/howto/customize-menu)
### 菜单插件
```bash
#xfce4-panel自带
$ xfce4-popup-applicationsmenu -p #在鼠标当前位置弹出xfce4-panel自带菜单
```
```bash
#xfce4-whiskermenu-plugin 插件：带搜索功能
$ sudo apt-get install xfce4-whiskermenu-plugin #安装
$ xfce4-popup-whiskermenu -p #在鼠标当前位置弹出whiskermenu自带菜单
```
### 配置文件
```bash
#Debian12 xfce4.18
/etc/xdg/menus/xfce-applications.menu #菜单主配置文件，定义了菜单名称等信息

/usr/share/desktop-directories/ #<Directory>下文件存放目录，定义了菜单图标、名称等信息
```

