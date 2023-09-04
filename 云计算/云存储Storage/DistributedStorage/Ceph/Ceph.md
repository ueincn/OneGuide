> **官网Wiki**：
> 
> Ceph uniquely delivers **object, block, and file storage in one unified system**.
> 
> Ceph 以独特的方式在一个统一系统中提供对象、块和文件存储。

## Ceph 介绍
Ceph以独特的方式在一个统一系统中提供对象、块和文件存储。Ceph 高度可靠、易于管理且免费。Ceph 的强大功能可以改变您公司的 IT 基础架构和管理大量数据的能力。Ceph 提供了非凡的可扩展性，可以使得数以千计的客户端访问 PB 到 EB 的数据。ceph存储集群相互通信以动态复制和重新分配数据。

#### Ceph 特点和特性

**高性能**

- 抛弃了传统的集中式存储运输局寻址的方案，采用 CRUSH 算法，数据分布均衡，并行度高。
- 考虑了容灾域的隔离，能够实现各类负载的副本设置规则，例如跨机房、机架感知等。
- 能够支持上千个存储节点的规模，支持 TB 到 PB 级的数据。

**高可用性**

- 副本数可以灵活控制
- 支持故障域分离，数据强一致性
- 多种故障场景自动进行修复自愈
- 没有单点故障，自动管理

**高可扩展性**

- 去中心化
- 扩展灵活
- 随着节点增加而线性增长

**特性丰富**

- 支持三种存储接口：块存储、文件存储、对象存储
- 支持自定义接口，支持多种语言驱动
Ceph 名称来源Ceph这个词是宠物章鱼的一个常见绰号。Ceph可以看作Cephalopod的缩写，它属于海洋软体类动物家族。Ceph以章鱼作为自己的吉祥物，表达了Ceph跟章鱼一样的并行行为。

---

## Ceph 链接
Ceph官网：[Home - Ceph](https://ceph.com/en/)
Ceph Wiki：[Intro to Ceph — Ceph Documentation](https://docs.ceph.com/en/latest/start/intro/#)
Ceph版本发布：[Ceph Releases (index) — Ceph Documentation](https://docs.ceph.com/en/latest/releases/)
教程链接：[【CEPH-初识篇】ceph详细介绍、搭建集群及使用，带你认识新大陆-云社区-华为云](https://bbs.huaweicloud.com/blogs/358172)

---

## Ceph 版本
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1676868202746-d095f26c-f30b-4de1-bf63-78f522f9e6c2.png#averageHue=%23f4f3f3&clientId=u83c3b81f-ec87-4&from=paste&height=450&id=ryX2F&originHeight=899&originWidth=1473&originalType=binary&ratio=1.75&rotation=0&showTitle=false&size=88005&status=done&style=stroke&taskId=ud063eee6-1d83-42bf-b4f7-e0024c19fd4&title=&width=737)

---

## Ceph 架构

**支持三种接口**

- Object：有原生 API，而且也兼容 Swift 和 S3 的 API
- Block：支持精简配置、快照、克隆
- File：Posix 接口，支持快照

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1677128750539-8386f2ac-3e50-41ee-b695-0b85c177615b.png#averageHue=%23f6f5f5&clientId=u2687f190-3be2-4&from=paste&height=275&id=llv3j&originHeight=367&originWidth=865&originalType=url&ratio=1.75&rotation=0&showTitle=false&size=238978&status=done&style=stroke&taskId=ufc3b7dd0-feb0-4bb4-a0ad-7a23b633f2d&title=&width=649)
**Ceph对象存储（RGW）**：RADOS Gateway> Ceph 对外提供的对象存储服务，接口与 S3 和 Swift 兼容。

**官网介绍**
Ceph 对象网关是建立在`librados`. 它在应用程序和 Ceph 存储集群之间提供了一个 RESTful 网关。
Ceph 对象存储支持两种接口：

- S3 兼容：通过与 Amazon S3 RESTful API 的大部分子集兼容的接口提供对象存储功能。
- Swift 兼容：通过与 OpenStack Swift API 的大部分子集兼容的接口提供对象存储功能。

Ceph 对象存储使用 Ceph 对象网关守护进程 (`radosgw`)，这是一个设计用于与 Ceph 存储集群交互的 HTTP 服务器。Ceph 对象网关提供与 Amazon S3 和 OpenStack Swift 兼容的接口，并且有自己的用户管理。Ceph 对象网关可以将数据存储在同一个 Ceph 存储集群中，其中存储了来自 Ceph 文件系统客户端和 Ceph 块设备客户端的数据。S3 API 和 Swift API 共享一个公共命名空间，这使得可以使用一个 API 将数据写入 Ceph 存储集群，然后使用另一个 API 检索该数据。
**注意**

- Ceph 对象存储不使用 Ceph 元数据服务器。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1676956911950-295c90bf-93a4-4efa-96dd-6ba12d80160f.png#averageHue=%23eaeaea&clientId=udc90f914-2e37-4&from=paste&id=iFkCb&originHeight=182&originWidth=570&originalType=url&ratio=1.75&rotation=0&showTitle=false&size=10391&status=done&style=none&taskId=ub97c987e-8ac3-420a-b032-0a243ebf952&title=)
**特征**

- RESTful 接口
- S3 和 Swift 兼容的 API
- S3 风格的子域
- 统一的 S3/Swift 命名空间
- 用户管理
- 使用跟踪
- 条纹对象
- 云端解决方案整合
- 多站点部署
- 多站点复制

---

**典型设备**
内置大容量硬盘的分布式服务器(swift, s3)；多台服务器内置大容量硬盘，安装上对象存储管理软件，对外提供读写访问功能。
**优点**

- 具备块存储的读写高速。
- 具备文件存储的共享等特性

**使用场景**：(适合更新变动较少的数据)

- 图片存储
- 视频存储
- ...
**Ceph块设备（RBD）**：RADOS Block Device> Ceph 对外提供的块设备服务，如虚拟机硬盘，支持快照功能。

**官网介绍**
块是字节序列（通常为 512）。基于块的存储接口是在 HDD、SSD、CD、软盘甚至磁带等介质上存储数据的一种成熟且常用的方法。块设备接口的普遍存在非常适合与包括 Ceph 在内的海量数据存储进行交互。
Ceph 块设备是精简配置的、可调整大小的，并且存储数据分布在多个 OSD 上。Ceph 块设备利用 RADOS功能，包括快照、复制和强一致性。Ceph 块存储客户端通过内核模块或`librbd`库与 Ceph 集群通信。
![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1676957880823-0abe0f41-71b6-4d3f-9079-043ecdd46e2a.png#averageHue=%23ececec&clientId=udc90f914-2e37-4&from=paste&id=yLaM6&originHeight=154&originWidth=570&originalType=binary&ratio=1.75&rotation=0&showTitle=false&size=6959&status=done&style=none&taskId=uce802c30-136f-44b8-a65f-8b189ecee39&title=)
**笔记**

- 内核模块可以使用 Linux 页面缓存。对于librbd基于 的应用程序，Ceph 支持RBD 缓存。

Ceph 的块设备为内核模块或QEMU等KVM以及依赖 libvirt 和 QEMU 与 Ceph 块设备集成的基于云的计算系统（如OpenStack和CloudStack）提供高性能和巨大的可扩展性 。您可以使用同一个集群同时操作Ceph RADOS 网关、 Ceph 文件系统和 Ceph 块设备。
**重要**

- 要使用 Ceph 块设备，您必须有权访问正在运行的 Ceph 集群。

**特征**

- 自动精简配置
- 高达 16 艾字节的图像
- 可配置条带化
- 内存缓存
- 快照
- 写时复制克隆
- 内核驱动支持
- KVM/libvirt 支持
- 云解决方案的后端
- 增量备份
- 灾难恢复（多站点异步复制）

---

**典型设备**
磁盘阵列，硬盘，主要是将裸磁盘空间映射给主机使用的。
**优点**

- 通过 Raid 与 LVM 等手段，对数据提供了保护。
- 多块廉价的硬盘组合起来，提高容量。
- 多块磁盘组合出来的逻辑盘，提升读写效率。

**缺点**

- 采用 SAN 架构组网时，光纤交换机，造价成本高。
- 主机之间无法共享数据。

**使用场景**

- Docker 容器、虚拟机磁盘存储分配。
- 日志存储
- 文件存储
- ...
**Ceph文件系统（CephFS）**：Ceph File System > Ceph 对外提供的文件系统服务。

**官网介绍**
Ceph 文件系统或CephFS是一个 POSIX 兼容的文件系统，构建在 Ceph 的分布式对象存储RADOS之上。CephFS 致力于为各种应用程序提供最先进、多用途、高可用性和高性能的文件存储，包括共享主目录、HPC 暂存空间和分布式工作流共享存储等传统用例。
CephFS 通过使用一些新颖的架构选择来实现这些目标。值得注意的是，文件元数据存储在与文件数据不同的 RADOS 池中，并通过可调整大小的元数据服务器集群或MDS提供服务，它可以扩展以支持更高吞吐量的元数据工作负载。文件系统的客户端可以直接访问 RADOS 来读写文件数据块。因此，工作负载可能会随着底层 RADOS 对象存储的大小线性扩展；也就是说，没有网关或代理为客户端调解数据 I/O。
对数据的访问通过 MDS 集群进行协调，MDS 集群充当由客户端和 MDS 共同维护的分布式元数据缓存状态的权威。每个 MDS 将元数据的变化聚合成一系列高效写入 RADOS 上的日志；MDS 没有在本地存储任何元数据状态。该模型允许在 POSIX 文件系统的上下文中在客户端之间进行连贯和快速的协作。
CephFS 因其新颖的设计和对文件系统研究的贡献而成为众多学术论文的主题。它是 Ceph 中最古老的存储接口，曾经是 RADOS 的主要用例。现在它与另外两个存储接口一起组成了一个现代统一存储系统：RBD（Ceph 块设备）和 RGW（Ceph 对象存储网关）。
**特征**

- 符合 POSIX 的语义
- 将元数据与数据分离
- 动态再平衡
- 子目录快照
- 可配置条带化
- 内核驱动支持
- 保险丝支持
- NFS/CIFS 可部署
- 与 Hadoop 一起使用（替代 HDFS）

---

**典型设备** 
FTP、NFS 服务器，为了克服块存储文件无法共享的问题，所以有了文件存储，在服务器上架设 FTP 与 NFS 服务器，就是文件存储。
**优点**

- 造价低，随便一台机器就可以了
- 方便文件可以共享

**缺点**

- 读写速率低
- 传输速率慢

**使用场景**

- 日志存储
- 有目录结构的文件存储
- ...

#### Ceph 组件

**RADOS**：Reliable Autonomic Distributed Object Store可靠、自动、分布式对象存储 （Reliable Autonomic Distributed Object Store，RADOS）是Ceph存储集群的基础。Ceph中的一切都以对象的形式存储，而RADOS就负责存储这些对象，而不考虑它们的数据类型。RADOS层确保数据一致性和可靠性。对于数据一致性，它执行数据复制、故障检测和恢复，还包括数据在集群节点间的迁移和再平衡。
RADOS是Ceph存储系统的核心，也称为Ceph存储集群。Ceph的所有优秀特性都是由RADOS提供的，包括分布式对象存储、高可用性、高可靠性、没有单点故障、自我修复以及自我管理等。因此，RADOS层在Ceph存储架构中扮演着举足轻重的角色。Ceph的数据访问方法（如RBD、CephFS、RADOSGW和librados）的所有操作都是在RADOS层之上构建的。
当Ceph集群接收到来自客户端的写请求时，CRUSH算法首先计算出存储位置，以此决定应该将数据写入什么地方。然后这些信息传递到RADOS层进行进一步处理。基于CRUSH规则集，RADOS以小对象的形式将数据分发到集群内的所有节点。最后，将这些对象存储在OSD中。
当配置的复制数大于1时，RADOS负责数据的可靠性。同时，它复制对象，创建副本，并将它们存储在不同的故障区域中，换言之，同一个对象的副本不会存放在同一个故障区域中。然而，如果有更多个性化需求和更高的可靠性，就需要根据实际需求和基础架构来优化CRUSH规则集。RADOS能够保证在一个RADOS集群中的对象副本总是不少于一个，只要你有足够的设备。
除了跨集群存储和复制对象之外，RADOS也确保对象状态的一致性。在对象不一致的情况下，将会利用剩下的副本执行恢复操作。这个操作自动执行，对于用户而言是透明的，从而为Ceph提供了自我管理和自我修复的能力。如果仔细分析Ceph的架构图，你会发现它有两部分：RADOS在最下部，它完全处于Ceph集群的内部，没有提供给客户端直接接口；另一部分就是在RADOS之上的面向所有客户端的接口。
RADOS系统主要由两个部分组成
1）OSD：由数目可变的大规模OSD（Object Storage Devices）组成的集群，负责存储所有的Objects数据。
2）Monitor：由少量Monitors组成的强耦合、小规模集群，负责管理Cluster Map。其中，Cluster Map是整个RADOS系统的关键数据结构，管理集群中的所有成员、关系和属性等信息以及数据的分发。
**LIBRADOS**：RADOS Library> RADOS 提供库，因为 RADOS 是协议很难直接访问，因此上层的 RBD、RGW 和 CephFS 都是通过 librados 访问的，目前提供 PHP、Ruby、Java、Python、C 和 C++ 支持。

librados库是一种用来简化访问RADOS的方法，它目前支持PHP、Ruby、Java、Python、C和C++语言。它提供了Ceph存储集群的一个本地接口RADOS，并且是其他服务（如RBD、RGW）的基础，以及为CephFS提供POSIX接口。librados API支持直接访问RADOS，使得开发者能够创建自己的接口来访问Ceph集群存储。
librados是一个本地的C语言库，通过它允许应用程序直接与RADOS通信，这样就可以绕过其他接口层与Ceph集群进行交互。librados是RADOS的一个库，它提供了丰富的API支持，这样就允许应用程序直接、并行地访问集群，而没有HTTP开销。应用程序可以扩展它们的本地协议以便通过直接连接librados来访问RADOS。类似的库也可用于支持C++、Java、Python、Ruby和PHP。librados是其他构建在librados本地接口之上的服务接口的基础，这些服务接口包括Ceph块设备、Ceph文件系统和Ceph RADOS网关。librados提供丰富的API子集，高效地在一个对象中存储键/值对。API通过同时更新数据、键和属性来支持atomic-single-object事务。通过对象实现对客户端之间通信的支持。
通过librados库直接与RADOS集群进行交互大大提高了应用程序的性能、可靠性和效率。librados提供了一套非常强大的库，使得它在平台即服务和软件即服务的云解决方案中可以提供额外的优势。
**MON**：Ceph Monitor> Ceph Monitor（简称：MON）组件通过一系列的Map来监控、跟踪整个集群的健康状态。

Monitor在Ceph集群中扮演者管理者的角色，维护了整个集群的状态，是Ceph集群中最重要的组件之一。
Monitor不存储实际的数据。Ceph Monitor Map包括OSD Map、PG Map、MDS Map和CRUSH Map等，这些Map被统称为集群Map。
#### Ceph Monitor Map 组件：

   1. **Monitor Map**：Monitor Map包括有关monitor节点端到端的信息，其中包括Ceph集群ID，监控主机名和IP地址和端口号，它还存储了当前版本信息以及最新更改信息。

`# ceph mon dump //查看Monitor Map` 

   2. **OSD Map**：OSD Map包括一些常用的信息，如集群ID，创建OSD Map的版本信息和最后修改信息，以及pool相关信息，pool的名字、pool的ID、类型，副本数目以及PGP，还包括OSD信息，如数量、状态、权重、最新的清洁间隔和OSD主机信息。

`# ceph osd dump //查看OSD Map`

   3. **PG Map**：PG Map包括当前PG版本、时间戳、最新的OSD Map的版本信息、空间使用比例，以及接近占满比例信息，同时，也包括每个PG ID、对象数目、状态、OSD的状态以及深度清理的详细信息。

`# ceph pg dump //查看PG Map`

   4. **CRUSH Map**：CRUSH Map包括集群存储设备信息，故障域层次结构和存储数据时定义失败域规则信息。

`# ceph crush dump //查看CRUSH Map`

   5. **MDS Map**：MDS Map包括存储当前MDS Map的版本信息、创建当前Map的信息、修改时间、数据和元数据POOL ID、集群MDS数目和MDS状态。

`# ceph mds dump //查看MDS Map`
**OSD**：Object Storage Devices实际存储数据的进程。通常一个OSD daemon绑定一个物理磁盘。Client write/read 数据最终都会走到OSD去执行write/read操作。
Ceph的OSD是Ceph存储集群中最重要的一个基础组件，它负责将实际的数据以对象的形式存储在每一个集群节点的物理磁盘驱动器中。Ceph集群中的大部分工作是由OSD守护进程完成的。存储用户数据是真正最耗时的部分。接下来将讨论Ceph中OSD守护进程的任务和职责。
Ceph OSD以对象的形式存储所有客户端数据，并在客户端发起数据请求时提供相同的数据。Ceph集群包含多个OSD。对于任何读或写操作，客户端首先向monitor请求集群的map，然后，它们就可以无须monitor的干预直接与OSD进行I/O操作。也正是因为产生数据的客户端能够直接写入存储数据的OSD而没有任何额外的数据处理层，才使得数据事务处理速度如此之快。与其他存储解决方案相比，这种类型的数据存储和取回机制是Ceph所独有的。
Ceph的核心特性（比如可靠性、自平衡、自恢复和一致性）都始于OSD。根据配置的副本数，Ceph通过跨集群节点复制每个对象多次来提供可靠性，同时使其具有高可用性和容错性。OSD上的每个对象都有一个主副本和几个辅副本，辅副本分散在其他OSD上。由于Ceph是一个分布式系统并且对象分布在多个OSD上，因此每一个OSD对于一些对象而言是主副本，但同时对于其他对象而言就是辅副本。存放辅副本的OSD受主副本OSD控制；然而，它们也可能又成为主副本OSD。从Ceph的Firefly版本（0.80）发布以来，添加了一个称为纠删码的新的数据保护机制。
在磁盘发生故障的时候，Ceph的OSD守护进程会自动与其他OSD通信，从而开始执行恢复操作。在这期间，存放故障磁盘对象的辅OSD会被提升为主OSD，同时，在恢复期间会为对象生成新的辅副本，整个过程对于用户是完全透明的。这保证了Ceph集群的可靠性和一致性。一个典型的Ceph集群部署方案会为集群节点上的每个物理磁盘创建一个OSD守护进程，这是推荐的做法。然而，OSD也支持以更灵活的方式部署OSD守护进程，比如每个磁盘、每个主机或者每个RAID卷一个OSD守护进程。JBOD环境下的多数Ceph集群部署会为每一个物理磁盘部署一个OSD守护进程
**MDS**：Ceph Metadata Server>  CephFS 服务依赖的元数据服务，对象存储和块设备存储不需要该服务。

Ceph元数据服务器 （MDS）跟踪文件层次结构并存储只供CephFS使用的元数据。Ceph块设备和RADOS网关不需要元数据，因此它们不需要Ceph MDS守护进程。MDS不直接给客户端提供数据，因此可以避免系统中的一个单点故障。
Ceph MDS是元数据服务器，只有Ceph文件系统（CephFS）才需要，其他存储方法不需要，如基于对象的存储不需要MDS服务。Ceph MDS作为一个守护进程运行，它允许客户端挂载一个任意大小的POSIX文件系统。MDS不直接向客户端提供任何数据，数据通过OSD服务提供。MDS提供一个带智能缓存层的共享型连续文件系统，因此可以大大减少读写操作。MDS在动态子树分区和一个MDS只负责一部分元数据等方面进一步发挥了它的好处。它在本质上就是动态的，守护进程可以加入、离开，并且快速接管出错的节点。
在某些情况下，MDS不存储本地数据会非常有用。如果一个MDS守护进程发生故障，我们可以在任何可以访问集群的节点上启动它。一个元数据服务器守护进程可配置为主动和被动状态。主MDS节点变为活跃状态，其他的则进入备用状态。在主MDS故障的时候，第二个MDS节点负责接管，并晋升为活跃节点。为了实现更快的恢复，你可以指定一个备用节点时刻跟随你的活跃节点，这将使得它们在内存中保存相同的数据来预填充缓存。

---

## Ceph 内部构件
Object> Ceph 最底层的存储单元是 Object 对象，一条数据、一个配置都是一个对象，每个 Object 包含 ID、元数据和原始数据。

一个对象通常包含绑定在一起的数据和元数据，并且用一个全局唯一的标识符标识。这个唯一的标识符确保在整个存储集群中没有其他对象使用相同的对象ID，从而保证对象唯一性。
基于文件的存储中，文件大小是有限制的；与此不同的是，对象的大小则是可以随着大小可变的元数据而变得很大。在一个对象中，数据存储为丰富的元数据，它们存储上下文和数据的实际内容等信息。对象存储的元数据允许用户妥善管理和访问非结构化数据。下图展示了如何把一个病人的信息另存为一个对象。
一个对象的元数据并不受限于类型或数量，它让你灵活地在元数据中添加一个自定义类型，因此给你数据的全部所有权。它不使用一个目录层次结构或树结构来存储；相反，它存储在一个包含数十亿对象且没有任何复杂性的线性地址空间中。对象可以存储在本地，也可以存放在地理上分开的线性地址空间中，也就是说，在一个连续的存储空间中。这种存储机制帮助对象在整个集群中唯一地标识自己。任何应用程序都可以基于对象ID通过调用RESTful API从对象中获取数据。这个URL可以以同样的方式工作在因特网上，一个对象ID作为一个唯一的指针指向对象。这些对象都以复制的方式存储在基于对象的存储设备（OSD）中，因而能提供高可用性。当Ceph集群接收到来自客户端的数据写请求时，它将接收到的数据另存为对象。然后OSD守护进程将数据写入OSD文件系统的一个文件中。
CRUSH：Controlled Replication Under Scalable Hashing>  	Ceph 使用的数据分布算法，类似一致性哈希，让数据分配到预期的地方。

可扩展散列下的受控复制（Controlled Replication Under Scalable Hashing，CRUSH）算法，它是Ceph的智能数据分发机制。CRUSH算法是Ceph皇冠上的珠宝之一，它是整个Ceph数据存储机制的核心。与传统系统依赖于存储和管理一个核心元数据/索引表不同的是，Ceph使用CRUSH算法来准确地计算数据应该被写入哪里或从哪里读取。CRUSH按需计算元数据，而不是存储元数据，从而消除传统的元数据存储方法中的所有限制。
**CRUSH查找**
CRUSH机制以这样一种方式工作：元数据计算的负载是分布式的并且只在需要时执行。元数据计算过程也称为CRUSH查找，现今的计算机硬件已经强大到足以快速且高效地执行CRUSH查找操作。CRUSH查找的独特之处在于，它不依赖系统。Ceph给客户端提供了足够的灵活性来按需执行元数据计算，也就是说，客户端使用自己的系统资源来执行CRUSH查找，从而取消中心查找。
对于Ceph集群的一次读写操作，客户端首先联系Ceph的monitor并获取一个集群map副本。集群map帮助客户端获取Ceph集群的状态和配置信息。使用对象和池名/ID将数据转换为对象。然后将对象和PG（placement groups，归置组）数一起经过散列来生成其在Ceph池中最终存放的那一个PG。然后前面计算好的PG经过CRUSH查找来确定存储或获取数据所需的主OSD的位置。计算完准确的OSD ID之后，客户端直接联系这个OSD来存储数据。所有这些计算操作都由客户端来执行，因此它不会影响集群的性能。一旦数据被写入主OSD，主OSD所在节点将执行CRUSH查找操作并计算辅助归置组和OSD的位置来实现数据复制，进而实现高可用性。参考下面的例子来了解CRUSH查找和对象到OSD的映射。
**CRUSH层级结构**
CRUSH是完全了解所有基础设施并支持用户自定义配置的，它维护你所有基础设施组件的一个嵌套层次结构。CRUSH设备列表通常包括磁盘、节点、机架（rack）、行（row）、开关、电源电路、房间、数据中心等。这些组件称为故障域或CRUSH bucket。CRUSH map包含一系列可用bucket，这些bucket表明了设备的具体物理位置。它还包括一系列的规则告诉CRUSH如何为不同的Ceph池复制数据。
CRUSH跨故障域来传播数据及其副本，因而即使一些组件出错，数据也是安全的。这就是CRUSH如何排除掉存储基础设施（它由商用软件组成）的单点故障问题，同时保证高可用性。CRUSH均匀地在整个集群磁盘上写数据，这样提高了性能和可靠性，并强制集群中的所有磁盘参与其中。它确保集群所有磁盘都同等地利用，而不考虑它们的能力。为此，CRUSH为每个OSD分配权重。OSD的权重越高，表示它的物理存储容量越大，这样CRUSH将会写入更多数据到这个OSD上。因此，较低权重的OSD与较高权重的OSD都同等地被填充数据。
**恢复和再平衡**
在故障域内任何组件发生故障之后，在Ceph将该OSD标记为down和out并初始化恢复操作前，默认情况下Ceph会等待300秒。这个值可以在Ceph集群的配置文件中通过参数mon osd down out interval进行修改。在恢复操作期间，Ceph开始重新组织发生故障的节点上受影响的数据。
CRUSH会复制数据到多个磁盘，这些复制的数据在恢复的时候使用。在恢复期间CRUSH试图移动尽量少的数据来构建一个新的集群布局，这样即使一些组件出现故障也能确保Ceph的容错性。
当一个新主机或磁盘添加到Ceph集群中时，CRUSH开始执行再平衡操作，在这个过程中，CRUSH从现有的主机/磁盘上移动数据到新的主机/磁盘。再平衡保证所有磁盘能均匀使用，以此提升集群性能和保持集群健康。例如，如果一个Ceph集群包含2000个OSD，这时一个新的系统添加20个新的OSD，这样就只有1%的数据会在再平衡期间移动，并且所有现有的OSD是并行地移动数据，使其迅速完成这个操作。然而，对于利用率高的Ceph集群，建议先将新添加的OSD的权重设为0，再逐渐增加权重到依据磁盘容量确定的更高的权重值。通过这种方式，新的OSD将减少Ceph集群再平衡时的负载并避免性能下降。
PG：Placement Grouops> 一个逻辑概念，一个 OSD 包含多个 PG。引入 PG 这一层其实是为了更好的分配数据和定位数据。每个 Pool 内包含很多个 PG，它是一个对象的集合，服务端数据均衡和恢复的最小单位就是 PG。

![image.png](https://cdn.nlark.com/yuque/0/2023/png/32659351/1677129887100-f83d1d32-c111-4dcd-b08d-50e40150248c.png#averageHue=%23f7f0d6&clientId=u2687f190-3be2-4&from=paste&height=323&id=ubf0efb02&originHeight=430&originWidth=865&originalType=url&ratio=1.75&rotation=0&showTitle=false&size=115063&status=done&style=stroke&taskId=u52b37fcf-fd75-4aef-bc83-8df5d666844&title=&width=649)

- pool 是 ceph 存储数据时的逻辑分区，它起到 namespace 的作用
- 每个 pool 包含一定数量(可配置)的 PG
- PG 里的对象被映射到不同的 Object 上
- pool 是分布到整个集群的

当Ceph集群接收到数据存储的请求时，它被分散到各个PG中。然而，CRUSH首先将数据分解成一组对象，然后根据对象名称、复制级别和系统中总的PG数目等信息执行散列操作，再将结果生成PG ID。PG是一组对象的逻辑集合，通过复制它到不同的OSD上来提供存储系统的可靠性。根据Ceph池的复制级别，每个PG的数据会被复制并分发到Ceph集群的多个OSD上。可以将PG看成一个逻辑容器，这个容器包含多个对象，同时这个逻辑容器被映射到多个OSD上。PG是保障Ceph存储系统的可伸缩性和性能必不可少的部分。
没有PG，在成千上万个OSD上管理和跟踪数以百万计的对象的复制和传播是相当困难的。没有PG的情况下管理这些对象所消耗的计算资源也是噩梦。与独立的管理每一个对象不同的是，我们的系统只管理包含大量对象的PG。这使得Ceph成为一个更易于管理和更易上手的系统。每个PG需要一定的系统资源（如CPU和内存），因为每个PG需要管理多个对象。因此应该精心计算集群中PG的数量。一般来说，增加集群PG的数量能够降低每个OSD上的负载，但是应该以规范的方式进行增加。建议每个OSD上放置50～100个PG。这是为了避免PG占用OSD节点太多的资源。随着存储数据的增加，同样需要根据集群规模来调整PG数。当在集群中添加或者删除一个设备的时候，大部分的PG保持不变；CRUSH管理PG在整个集群内部的分布。
**计算PG数**
计算正确的PG数是构建一个企业级的Ceph存储集群中至关重要的一步。因为PG在一定程度上能够提高或者影响存储性能。
计算Ceph集群中PG数的公式如下：PG总数=（OSD总数×100）/最大副本数
结果必须舍入到最接近2的N次幂的值。
比如：如果Ceph集群有160个OSD且副本数是3，这样根据公式计算得到的PG总数是5333.3，因此舍入这个值到最接近的2的N次幂的结果就是8192个PG。
我们还应该计算Ceph集群中每一个池中的PG总数。
计算公式如下：PG总数=（（OSD总数×100）/最大副本数）/池数
同样使用前面的例子：OSD总数是160，副本数是3，池总数是3。根据上面这个公式，计算得到每个池的PG总数应该是1777.7，最后舍入到2的N次幂得到结果为每个池2048个PG。平衡每个池中的PG数和每个OSD中的PG数对于降低OSD的方差、避免速度缓慢的恢复进程是相当重要的。

Pool> 一个存储对象的逻辑分区，它通常规定了数据冗余的类型与副本数，默认为3副本。对于不同类型的存储，需要单独的 Pool，如 RBD。

对于存储系统而言，池并不是很新的概念。企业级存储系统是通过创建不同的池来管理的，Ceph也通过池提供了简单的存储管理。Ceph的池是一个用来存储对象的逻辑分区。Ceph中每个池都包含一定数量的PG，进而实现把一定数量的对象映射到集群内部不同OSD上的目的。因此，每一个池都是交叉分布在集群所有节点上的，这样就能够提供足够的弹性。默认情况下，部署Ceph只会根据你的需求新建一个默认池，建议除了默认池外新建其他的池。
池可以通过创建需要的副本数来保障数据的高可用性，比如通过复制或者纠删码方式。纠删码（EC）特性是Ceph的新功能，首次发布是在Ceph的Firefly版本中。纠删码是一种数据保护方法，它首先将数据分解成块，接着编码，然后以分布式的方式存储。天生就是分布式的Ceph能够很好地利用EC。
在创建池的时候，可以指定副本数。默认的副本数是2。池的副本数是非常灵活的。在任何时候，都可以改变它。也可以在池创建的时候指定纠删码的规则集，它能够提供同等级别的可靠性，但是与副本的方法相比消耗更少的空间。
池可以以复制或者纠删码方式创建，但不能同时使用这两种方式。
当把数据写入一个池的时候，Ceph的池会映射到一个CRUSH规则集，CRUSH规则集就是通过识别池来实现集群内对象的分布和副本数。CRUSH规则集为Ceph池提供了新的功能。例如，我们可以创建一个使用SSD硬盘的faster池，也就是俗称的缓存池；或者是使用SSD、SAS和SATA硬盘组成的混合池。
Ceph的池还支持快照功能。我们可以使用ceph osd pool mksnap命令来给特定的池制作快照，并在必要的时候恢复这些快照。此外，Ceph的池还允许我们为对象设置所有者和访问权限。可以给池分配一个用户ID以此标识该池的所有者。在很多需要限制访问池的权限的场景下这非常有用。

---

## Ceph 重点
NoteRADOS是Ceph存储系统的核心，也称为Ceph存储集群。
Ceph的数据访问方法（如RBD、CephFS、RADOSGW和librados）的所有操作都是在RADOS层之上构建的。
RADOS包含两个核心组件：OSD和monitor。
Ceph的OSD是Ceph存储集群中最重要的一个基础组件，它负责将实际的数据以对象的形式存储在每一个集群节点的物理磁盘驱动器中。Ceph集群中的大部分工作是由OSD守护进程完成的。
Ceph集群的性能基准测试的主要标准之一就是文件系统的选择。
块存储是企业环境中最常见的一种数据存储格式。
Ceph中的所有数据单元都是以对象的形式存储在一个池中。Ceph的池是一个用来存储对象的逻辑分区，它提供了一个有组织的存储方式。
CRUSH机制以这样一种方式工作：元数据计算的负载是分布式的并且只在需要时执行。
计算正确的PG数是构建一个企业级的Ceph存储集群中至关重要的一步。
计算Ceph集群中PG数的公式如下：PG总数=（OSD总数×100）/最大副本数（结果必须舍入到最接近2的N次幂的值。）
对Ceph池的操作是Ceph管理员的日常工作之一。

| **状态** | **描述** |
| --- | --- |
| active | 当前拥有最新状态数据的pg正在工作中，能正常处理来自客户端的读写请求。 |
| inactive | 正在等待具有最新数据的OSD出现，即当前具有最新数据的pg不在工作中，不能正常处理来自客户端的读写请求。 |
| activating | Peering 已经完成，PG 正在等待所有 PG 实例同步并固化 Peering 的结果 (Info、Log 等) |
| clean | pg所包含的object达到指定的副本数量，即object副本数量正常 |
| unclean | PG所包含的object没有达到指定的副本数量，比如一个PG没在工作，另一个PG在工作，object没有复制到另外一个PG中。 |
| peering | PG所在的OSD对PG中的对象的状态达成一个共识（维持对象一致性） |
| peered | peering已经完成，但pg当前acting set规模小于存储池规定的最小副本数（min_size） |
| degraded | 主osd没有收到副osd的写完成应答，比如某个osd处于down状态 |
| stale | 主osd未在规定时间内向mon报告其pg状态，或者其它osd向mon报告该主osd无法通信 |
| inconsistent | PG中存在某些对象的各个副本的数据不一致，原因可能是数据被修改 |
| incomplete | peering过程中，由于无法选出权威日志，通过choose_acting选出的acting set不足以完成数据修复，导致peering无法正常完成 |
| repair | pg在scrub过程中发现某些对象不一致，尝试自动修复 |
| undersized | pg的副本数少于pg所在池所指定的副本数量，一般是由于osd down的缘故 |
| scrubbing | pg对对象meta的一致性进行扫描 |
| deep | pg对对象数据的一致性进行扫描 |
| creating | pg正在被创建 |
| recovering | pg间peering完成后，对pg中不一致的对象执行同步或修复，一般是osd down了或新加入了osd |
| recovering-wait | 等待 Recovery 资源预留 |
| backfilling | 一般是当新的osd加入或移除掉了某个osd后，pg进行迁移或进行全量同步 |
| down | 包含必备数据的副本挂了，pg此时处理离线状态，不能正常处理来自客户端的读写请求 |
| remapped | 重新映射态。PG 活动集任何的一个改变，数据发生从老活动集到新活动集的迁移。在迁移期间还是用老的活动集中的主 OSD 处理客户端请求，一旦迁移完成新活动集中的主 OSD 开始处理 |
| misplaced | 有一些回填的场景：PG被临时映射到一个OSD上。而这种情况实际上不应太久，PG可能仍然处于临时位置而不是正确的位置。这种情况下个PG就是misplaced。这是因为正确的副本数存在但是有个别副本保存在错误的位置上 |

