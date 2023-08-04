MySQL 的官网下载地址：[http://www.mysql.com/downloads/](http://www.mysql.com/downloads/)
[![image.png](https://cdn.nlark.com/yuque/0/2022/png/32659351/1665926134855-f99bfcf5-ee4a-4dad-afec-f4655052c21d.png#averageHue=%23f39c30&clientId=ucf40c93b-5e67-4&from=paste&id=u2474f5fa&originHeight=170&originWidth=909&originalType=url&ratio=1&rotation=0&showTitle=false&size=34380&status=done&style=none&taskId=ue5b0b488-83ad-468d-b241-1dc6efc1eef&title=)](https://images2015.cnblogs.com/blog/417876/201701/417876-20170111165734556-997612557.png)
个人理解：
1、不要再纠结是否是5.1还是5.5、5.6、5.7这些，一般选择时不要选择太新，选择5.1或者5.5就可以了。
2、如果要了解每个版本的都有哪些更新，可以直接上官网查看change log，或者百度。
3、我们选择一般是选择开源免费版本：MySQL Community Server 社区版本。
4、如果要下载源代码或者指定的版本，直接参照上图中的[Archive](https://downloads.mysql.com/archives/)。这里有各个版本记录。
5、要下载最新版本，直接参考上图中的[Community](https://dev.mysql.com/downloads/)，要选择GA版本。

# 一、版本代号说明
1. MySQL Community Server 社区版本，开源免费，但不提供官方技术支持。
2. MySQL Enterprise Edition 企业版本，需付费，可以试用30天。
3. MySQL Cluster 集群版，开源免费。可将几个MySQL Server封装成一个Server。
4. MySQL Cluster CGE 高级集群版，需付费。
5. MySQL Workbench（GUITOOL）一款专为MySQL设计的ER/数据库建模工具。它是著名的数据库设计工具DBDesigner4的继任者。MySQLWorkbench又分为两个版本，分别是社区版（MySQL Workbench OSS）、商用版（MySQL WorkbenchSE）。
6. Generally Available（GA）Release，GA是指软件的通用版本，一般指正式发布的版本．
7. "essentials”是指精简版，不包含 embedded server and benchmarksuite，有自动安装程序和配置向导，没有MySQL文档。
8. “noinstall”是指非安装的压缩包的。包含 embedded server and benchmarksuite，没有自动安装程序和配置向导，需手动安装配置，有MySQL文档。

# 二、什么是MySQL企业版（MySQL Enterprise）？
MySQL企业版是一个已被证明和值得信赖的平台，这个平台包含了MySQL企业级数据库软件,、监控与咨询服务，以及确保您的业务达到最高水平的可靠性、安全性和实时性的技术支持。
MySQL企业版包括：
MySQL企业级服务器，这是全球最流行的开源数据库最可靠、最安全的最新版本。
MySQL企业级系统监控工具，它可以提供监控和自动顾问服务，以此来帮助您消除安全上的隐患、改进复制、优化性能等。
MySQL技术支持，可以使您最棘手的技术问题得到快速解答。
MySQL咨询支持，只有购买了MySQL企业级银质或金质服务的客户才能得到此项支持。MySQL技术支持团队将为您的系统提供针对性的建议，告诉您如何恰当地设计和调整您的MySQL服务器、计划、查询和复制设定，以获得更好的性能。
# 三、什么是MySQL社区版（MySQL Community Server）？
MySQL公司一直专注于向开源社区发布全球最流行的开源数据库——MySQL Community Server。
在开源GPL许可证之下可以自由的使用。
MySQL企业版和社区版之间有何不同？
2006年底，MySQL开始发行MySQL Enterprise，这个产品包含了一系列更健全的提高MySQLserver可靠性、安全性和性能的服务。
MySQL社区版是开源的GPL许可，可以免费获取。
MySQL网络版是通过MySQL认证的许可，需要花钱购买。
MySQL网络版在网络和企业部署功能、排错功能、技术和产品支持、升级更新、享有MySQL知识库、直接得到MySQL开发人员指导等方面，都是MySQL社区版所没有的。

# 四、其它名词解析
Windows Essentials (x86) 6.0.7 ：Essentials 精简，精简版 - 去除了实例文件
Windows ZIP/Setup.EXE (x86)6.0.7：自动安装版，下载下来后是个zip包，解压后有个setup.exe，可以直接运行安装
Without installer (unzip in C:\) 6.0.7：installer 压缩版 -绿色免安装版，解压后是程序文件，甚至相当于运行setup.exe后的样子，需要自己手动配置
MySQL GUITools一个可视化界面的MySQL数据库管理控制台，提供了四个非常好用的图形化应用程序，方便数据库管理和数据查询。这些图形化管理工具可以大大提高数据库管理、备份、迁移和查询效率，即使没有丰富的SQL语言基础的用户也可以应用自如。它们分别是：
MySQL Migration Toolkit：数据库迁移
MySQL Administrator：MySQL管理器
MySQL Query Browser：用于数据查询的图形化客户端
MySQL Workbench：DB Design工具
