# IP-SAN
IPSAN: 利用IP网络构建存储网络, 使用TCP/IP协议的iscsi协议封装构建的存储区域网络

#### 使用协议
Internet 小型计算机系统接口 (iSCSI)：第二大 SAN 或块协议，约占 10% 至 15% 的市场份额。iSCSI 将 SCSI 命令封装在以太网帧内，然后使用 IP 以太网络进行传输。

#### 协议基础
iSCSI 是 Internet SCSI（Small Computer System Interface，小型计算机系统接口）的缩写，是用于链接数据存储子系统的基于 Internet 协议 (Internet Protocol, IP) 的存储网络标准。

通过在 IP 网络上传输 SCSI 命令，iSCSI 协议可用于访问网络中的块设备，就像这些设备连接至本地系统一样。

iSCSI SAN 上单个可发现的实体（如启动器或目标）表示一个 iSCSI 节点。

每个节点可通过多种方式进行标识。

- IP 地址
每个 iSCSI 节点都可具有一个与其相关联的 IP 地址，以便网络上的路由和交换设备可以在服务器与存储器之间建立连接。此地址就像为了访问公司的网络或 Internet 而分配给计算机的 IP 地址一样。
- iSCSI 名称
用于标识节点的全球唯一名称。iSCSI 使用 iSCSI 限定名 (IQN) 和扩展唯一标识符 (EUI)。
默认情况下，Windows为 iSCSI 启动器生成唯一 iSCSI 名称，例如iqn.1991-05.com.microsoft:win-pjcqrusvvl9。通常无需更改默认值，如需修改启动器名称，请确保输入的新 iSCSI 名称是全球唯一的。
iSCSI，通过TCP/IP网络传输SCSI命令提供对存储设备的块级访问，属于SAN存储，因此又叫IP-SAN，默认端口3260/TCP。也就是说通过iSCS获取到的是一个真实的或者虚拟的存储设备，连接之后会多出一个硬件设备，就像一块本机硬盘一样，你需要在上面建立文件系统后才能使用。而NFS、SMB等获取到的只是一个挂载点，与文件系统无关，连接后即可以使用。
- 客户端称为initiators，服务器上的存储目标称为target，客户端发现服务器上存储目标的过程叫discovery。
- iscsi target：存储设备端，服务器端的设备，为其他服务器提供“磁盘”。
- Iscsi initiator：使用target提供“磁盘”的客户端。
- target端主要是把磁盘share出来给其他设备用的。initiator相当于用来映射target端的磁盘到本地的。
- iSCSI是对应透明的，以下几种方式可以作为“磁盘”分享出去给initiator使用：
  - 大型文件[dd]命令生成
  - 磁盘阵列、磁盘或者磁盘分区等真实磁盘  
  - 使用LVM中的逻辑卷

#### iqn
SCSI的target名称的命名方式：
```shell
iqn.yyyy-mm.<reversed domain name>[:identifier]
```
其含义：
- iqn表示“iSCSI Qualified Name”，简称iqn。
- yyyy-mm表示“年-月”。
- reversed domain name表示倒过来的域名。
- identifier是识别名称。