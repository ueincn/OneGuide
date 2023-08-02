# UKUI
## 项目介绍
UKUI(Ultimate Kylin User Interface) 

## 项目地址
### 虚包/安装包
- [ukui-desktop-environment](https://gitee.com/openkylin/ukui-desktop-environment)

  UKUI桌面环境：此安装包分为UKUI核心安装包ukui-desktop-environment-core、UKUI完整安装包ukui-desktop-environment和UKUI扩展安装包ukui-desktop-environment-extras，其中，核心安装包安装时会将UKUI必需的基础组件进行安装，这将为你提供一个轻量级的桌面环境；完整安装包在必需基础组件的基础上会安装截图、备忘录、平板环境等应用并建议安装主题框架、输入法框架等桌面环境框架，这将很大程度上丰富你的办公、生活和娱乐场景；扩展安装包将会添加一些额外的工具，它为开发者提供一些必要的开发工具。

### 基础组件

- [ukui-greeter](https://gitee.com/openkylin/ukui-greeter)

   ukui-greeter是UKUI桌面环境的基于Lightdm的登录程序

- [ukui-session-manager](https://gitee.com/openkylin/ukui-session-manager)

  ukui-session-manager是UKUI桌面环境的会话管理器，它将管理我们如何去与Linux shell进行交互

- [ukui-control-center](https://gitee.com/openkylin/ukui-control-center)

  UKCC(ukui-control-center)是UKUI桌面环境的控制面板，在这里我们可以通过界面来配置主题、桌面背景、添加用户和修改密码等操作

- [ukui-screensaver](https://gitee.com/openkylin/ukui-screensaver)

  ukui-screensaver是UKUI桌面环境的锁屏及屏保

- [ukui-menu](https://gitee.com/openkylin/ukui-menu)

  ukui-menu是UKUI桌面环境的启动器，在这里我们可以方便地选择我们要打开的应用

- [ukui-panel](https://gitee.com/openkylin/ukui-panel)

  ukui-panel是UKUI桌面环境的任务栏，在这里我们可以直观地看到使用中应用的状态并进行快捷地切换

- [ukui-sidebar](https://gitee.com/openkylin/ukui-sidebar)

  ukui-sidebar是UKUI桌面环境中的侧边栏快捷工具，主要包括控制中心和通知中心两个部分，我们可以通过它查询应用消息和配置一些开关

- [peony](https://gitee.com/openkylin/peony)

  peony是UKUI桌面环境的文件管理器,它允许用户浏览目录、预览文件并启动与之相关的应用程序,它还负责处理UKUI桌面上的图标，并且适用于本地和远程文件系统

- [ukui-window-switch](https://gitee.com/openkylin/ukui-window-switch)

  ukui-window-switch是在UKUI桌面环境中的多任务视图。在PC模式下，多任务视图提供了一个方便快捷的交互界面，可以方便地在虚拟桌面之间切换和定位您想要的窗口，从而提高您的生产效率和工作效率。在平板模式中可以方便地管理打开的窗口，用户可以选择唤醒或关闭任务视图中显示的任何窗口，还可以通过不同的动画提高交互体验

### 基础服务
- [ukui-settings-daemon](https://gitee.com/openkylin/ukui-settings-daemon)

  ukui-settings-daemon是UKUI桌面环境下的底层守护程序；负责设置UKUI会话的各种参数以及运行的应用程序

- [ukui-notification-daemon](https://gitee.com/openkylin/ukui-notification-daemon)

  ukui-notification-daemon是UKUI桌面环境的通知服务，它是根据freedesktop通知规范实现的一套通知框架，它将高效地为我们展示应用通知或系统通知

- [ukui-notification](https://gitee.com/openkylin/ukui-notification)

  ukui-notification包含UKUI桌面环境的通知服务（ukui-notification-server）和通知开发接口（libukui-notifiaction）

- [kylin-device-daemon](https://gitee.com/openkylin/kylin-device-daemon)

  kylin-device-daemon是UKUI桌面环境中的设备管理的守护进程

### 平板特性
- [ukui-tablet-desktop](https://gitee.com/openkylin/ukui-tablet-desktop)

  ukui-tablet-desktop是UKUI平板桌面和任务栏，它是基于Qt/QML实现的

- [kylin-status-manager](https://gitee.com/openkylin/kylin-status-manager)

  kylin-status-manager是UKUI桌面环境的状态管理器，它监听、管理笔记本电脑、平板等旋转、折叠等状态

- [ukui-app-widget](https://gitee.com/openkylin/ukui-app-widget)

  ukui-app-widget为桌面环境的平板桌面提供小插件实现框架，可以通过该框架实现桌面小插件

- [ukui-system-appwidget](https://gitee.com/openkylin/ukui-system-appwidget)

  ukui-system-appwidget是UKUI桌面环境平板模式下的时间小插件

### 特色应用
- [ukui-search](https://gitee.com/openkylin/ukui-search)

  ukui-search是UKUI桌面环境中的全局搜索，提供了本地文件、文本内容、应用、设置项、便签等聚合搜索功能，基于其文件索引功能，可以为用户提供快速准确的搜索体验，除此之外，提供文件、文件内容等搜索的解决方案，应用可以方便地通过接口接入开发使用

- [ukui-clock](https://gitee.com/openkylin/ukui-clock) 

  ukui-clock是UKUI桌面环境中的闹钟应用

- [time-shutdown](https://gitee.com/openkylin/time-shutdown)

  time-shutdown是UKUI桌面环境中的定时开关机应用

### 短距管理
- [kylin-nm](https://gitee.com/openkylin/kylin-nm)

  kylin-nm全称是kylin-network-manager，是UKUI桌面环境的网络前端，提供了对有线和无线连接管理等功能

- [libkylin-nm-base](https://gitee.com/openkylin/libkylin-nm-base)

  libkylin-nm-base是UKUI桌面环境中kylin-nm组件的插件开发包
  
- [kylin-nm-plugin](https://gitee.com/openkylin/kylin-nm-plugin)

  kylin-nm-plugin是UKUI桌面环境中kylin-nm的插件

- [ukui-bluetooth](https://gitee.com/openkylin/ukui-bluetooth)

  ukui-bluetooth是UKUI桌面环境中的蓝牙工具

### 主题风格
- [qt5-ukui-platformtheme](https://gitee.com/openkylin/qt5-ukui-platformtheme)

  qt5-ukui-platformtheme是UKUI桌面环境中的平台主题，主题根据UKUI的设计来统一和美化所有qt应用程序

- [ukui-globaltheme](https://gitee.com/openkylin/ukui-globaltheme)

  ukui-globaltheme是UKUI桌面环境上的系统主题，包括“寻光”和“和印”两种主题，用户可以在控制的主题选项中进行选择切换

- [ubuntukylin-theme](https://gitee.com/openkylin/ubuntukylin-theme)

  ubuntukylin-theme是Ubuntu Kylin主题，这个软件包包含Ubuntu Kylin的默认主题

- [openkylin-theme](https://gitee.com/openkylin/openkylin-theme)

  openkylin-theme是Open Kylin主题，这个包包含openKylin的默认主题

- [dmz-cursor-theme](https://gitee.com/openkylin/dmz-cursor-theme)

  dmz-cursor-theme是UKUI桌面环境中风格中立、可伸缩的光标主题，这些主题源自为Ximian GNOME桌面开发的工业主题，提供了可扩展格式的黑色和白色光标

### 生物特征识别
- [biometric-authentication](https://gitee.com/openkylin/biometric-authentication)

  biometric-authentication是UKUI桌面环境中的生物特征识别框架，用于各种生物特征识别和认证

- [ukui-biometric-auth](https://gitee.com/openkylin/ukui-biometric-auth)

  ukui-biometric-auth是PolicyKit-1的UKUI身份验证代理，ukui-polkit包支持通用身份验证和生物特征身份验证，即该服务由biometric-auth提供

- [ukui-biometric-manager](https://gitee.com/openkylin/ukui-biometric-manager)

  ukui-biometric-manager是UKUI桌面环境中的生物识别认证管理器，是一个用于管理生物识别设备驱动程序和用户功能以及管理是否启用生物识别身份验证的工具。

### 其他（待分类和补充）
- [ukui-interface](https://gitee.com/openkylin/ukui-interface)

  ukui-interface为桌面环境层的应用提供了多种API接口，包括操作系统、用户账户、个性化、时间、语言、安全管理、系统更新、网络管理、硬件管理等

- [ukui-power-manager](https://gitee.com/openkylin/ukui-power-manager)

  ukui-power-manager是UKUI桌面环境中的电源管理应用

- [ukui-kwin](https://gitee.com/openkylin/ukui-kwin)

  ukui-kwin是UKUI桌面环境的默认窗口管理器，是从kwin派生而来的

- [ukui-kwin-effects](https://gitee.com/openkylin/ukui-kwin-effects)

  ukui-kwin-effects是UKUI桌面环境的旧版多任务视图应用，目前已不维护，新版请参考[ukui-window-switch](https://gitee.com/openkylin/ukui-window-switch)

- [ukui-system-monitor](https://gitee.com/openkylin/ukui-system-monitor)

  ukui-system-monitor是UKUI桌面环境中的系统监视器应用，可以方便用户以图形方式查看和操作正在运行的进程，它还展示了系统资源（如CPU和内存）和文件系统

- [ukui-touch-settings-plugin](https://gitee.com/openkylin/ukui-touch-settings-plugin)

  ukui-touch-settings-plugin是一个触摸相关设备的插件集合，包括touchscreen-settings、touchpen-settings、touchpad-settings，这些插件会被控制面板加载

- [ukui-input-gather](https://gitee.com/openkylin/ukui-input-gather)

  ukui-input-gather是一个后台服务，负责事件分发，主要有两个功能，一是kwin用来处理触摸板手势，二是状态管理用来监控状态模式切换

- [ubuntukylin-default-settings](https://gitee.com/openkylin/ubuntukylin-default-settings)

  ubuntukylin-default-settings是Ubuntu Kylin桌面的默认设置，这个软件包包含Ubuntu Kylin使用的默认设置

- [openkylin-default-settings](https://gitee.com/openkylin/openkylin-default-settings)
  
  openkylin-default-settings是Open Kylin桌面的默认设置，这个软件包包含Open Kylin使用的默认设置

- [ubuntukylin-wallpapers](https://gitee.com/openkylin/ubuntukylin-wallpapers)

  ubuntukylin-wallpapers是从Ubuntu Kylin 13.10壁纸大赛中选出的杰出壁纸，这些壁纸有望展现出美妙的中国风格

- [kylin-app-manager](https://gitee.com/openkylin/kylin-app-manager)

  kylin-app-manager是UKUI桌面的应用管理组件，负责应用程序启动

- [kylin-app-cgroupd](https://gitee.com/openkylin/kylin-app-cgroupd)

   kylin-app-cgroupd负责UKUI桌面环境中的进程管理，是Kylin系统资源观察者和进程的管理者

- [kylin-usb-creator](https://gitee.com/openkylin/kylin-usb-creator)

  kylin-usb-creator是UIKUI桌面环境中的U盘启动盘制作工具

- [kylin-user-guide](https://gitee.com/openkylin/kylin-user-guide)

  kylin-user-guide是UKUI桌面环境中的用户指南

- [peony-extensions](https://gitee.com/openkylin/peony-extensions)

  peony-extensions是UKUI桌面环境penoy组件的扩展包，它为peony文件管理器添加了扩展功能

- [youker-assistant](https://gitee.com/openkylin/youker-assistant)
  
  youker-assistant是UKUI桌面环境中的工具箱应用，该工具向用户展示了整机信息、硬件参数、硬件监测和驱动管理四部分内容

- [libpwquality](https://gitee.com/openkylin/libpwquality)

  libpwquality用于密码质量检查和生成通过检查的随机密码

- [qt5-gesture-extensions](https://gitee.com/openkylin/qt5-gesture-extensions)

  qt5-gesture-extensions是UKUI桌面环境中的手势扩展的库，例如列表视图滚动等

- [kwin](https://gitee.com/openkylin/kwin)

  KWin是一个易于使用但灵活的复合窗口管理器，适用于Linux上的Xorg窗口系统（Wayland，X11），
它的主要用途是与Desktop Shell（例如KDE Plasma Desktop）结合使用。

- [chinese-segmentation](https://gitee.com/openkylin/chinese-segmentation)

  chinese-segmentation是UKUI桌面环境中的中文分词组件，以全局单例的形式提供了中文分词、汉字转拼音和中文繁体简体转换功能

- [ukui-file-meta-data](https://gitee.com/openkylin/ukui-file-meta-data)

  ukui-file-meta-data提供了文件元数据解析与用户自定义数据写入功能，其中读取部分结构与部分代码参考自KFileMetaData。为了满足ukui的个性化开发需求，我们在KFileMetaData的基础上做了部分修改与删减

- [kpipewire](https://gitee.com/openkylin/kpipewire)

  kpipewire在Qt项目中提供了一组使用PipeWire的方便类(https://pipewire.org/)。它是用C++开发的，它的主要使用目标是QML组件。kpipewire提供两个主要组件：KPipeWire，提供连接到应用程序并将PipeWire渲染到应用程序中的主要组件；KPipeWireRecord，使用FFmpeg，有助于将PipeWire视频流记录到文件中

- [lightdm](https://gitee.com/openkylin/lightdm)

  lightdm是UKUI桌面环境中的一款X显示器管理器，用于Linux系统中管理用户会话和登录。它是一个可定制的登录界面，可以支持多个用户，可以使用不同的桌面环境和窗口管理器，还可以添加自定义主题和背景

- [policykit-1](https://gitee.com/openkylin/policykit-1)

  polkit是UKUI桌面环境中一个用于定义和处理授权的工具包。它用于允许非特权进程与特权进程对话