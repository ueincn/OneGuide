Zstack安装部署：
1.获取相关Zstack安装文件。
2.上传至相关管理服务器节点。
3.bash zstack-upgrade -a ZStack-DVD-Kylin10SP2.iso （添加本地源文件）
4.bash zstack-upgrade -r ZStack-DVD-Kylin10SP2.iso （更新本地源文件）
5.安装管理节点：bash /opt/zstack-dvd/x86/ns10/zstack-installer.bin -E
6.安装完成，无报错后，浏览器登录：http://< Admin IP>:5000 默认账号：admin，密码：password
7.根据设置向导，获取软件授权。
8.设置集群，根据管理地址，添加其余节点。

