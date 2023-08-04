# MariaDB 简介
MariaDB Server 是一个通用的开源关系数据库管理系统。 它是世界上最受欢迎的数据库服务器之一，拥有包括 Wikipedia、WordPress.com 和 Google 在内的知名用户。 MariaDB Server 在 GPLv2 开源许可下发布，并保证保持开源。

它可用于高可用性事务数据、分析、作为嵌入式服务器，并且广泛的工具和应用程序支持 MariaDB Server。

# MariaDB Server
## 来历
当 MariaDB Server 的前身 MySQL 于 2009 年被 Oracle 收购时，MySQL 创始人 Michael “Monty” Widenius 出于对 Oracle 管理权的担忧而分叉了该项目，并将新项目命名为 MariaDB。 MySQL 以他的第一个女儿 My 命名，而 MariaDB 则以他的第二个女儿 Maria 命名。

大多数原始开发人员加入了新项目，此后 MariaDB Server 继续快速发展。

## 版本编号
在 MariaDB 5.5 之前，MariaDB Server 遵循 MySQL 版本编号模式，旨在与 MySQL 的同一主要版本兼容。

2012 年，为了反映 MySQL 中不可用的功能越来越多，MariaDB Server 的版本编号出现了分歧，MariaDB 发布了 10.0，而 MySQL 发布了 5.6。 当前的长期支持版本是 MariaDB 10.6，而最新的稳定短期支持版本是 MariaDB 10.9。

## 与 MySQL、PostgreSQL、MongoDB 和 Oracle 的兼容性
MariaDB Server 仍然保持与 MySQL 的高度兼容性，并且大多数使用 MySQL 的流行应用程序将与 MariaDB 无缝协作。 由于 MariaDB 的目标与 MySQL 不同，并且 MariaDB Server 有许多新功能，因此不再使用较早的术语 drop-in replacement。

MariaDB Server 非常强调不破坏其用户的向后兼容性。 就地升级支持从旧的 MySQL 版本升级到最新的 MariaDB 版本。

MariaDB Server 提供了一种 Oracle 语法兼容模式，无需更改即可运行 Oracle 数据库应用程序。

MariaDB 知识库包含有关从 SQL Server 迁移到 MariaDB 的部分。

与 MariaDB 相比，PostgreSQL 最初是一个研究项目，专注于特性，而不是性能和稳定性。 MariaDB 的前身 MySQL 遵循务实的方法，功能较少，但注重性能、稳定性和易用性。 从那时起，两者之间的差异已经缩小，MariaDB 专注于更全面地实现 ANSI SQL 标准，而 PostgreSQL 则专注于提高其性能。

对于 MongoDB 用户，我们的 JSON 功能可能会感兴趣：

有大量的 JSON 函数，用于处理非结构化数据。
JSON 数据类型，LONGTEXT 的别名，带有约束以确保它是有效的 JSON
CONNECT 存储引擎有一个 JSON 表类型，包括处理 JSON 数据的强大功能。
# 开放架构：存储引擎
MariaDB 服务器的模型允许人们选择最适合满足各种需求的特定存储引擎。 其中一些包括：

一般用途
- InnoDB 是一个很好的通用事务存储引擎，也是大多数情况下的最佳选择。
- Aria 是 MariaDB 对 MyISAM 的更现代改进，占用空间小，允许在系统之间轻松复制表。
- MyISAM 占用空间小，允许在系统之间轻松复制表。 MyISAM 是 MySQL 最古老的存储引擎。 除了遗留用途外，通常没有什么理由使用它。 Aria 是 MariaDB 更现代的改进。
## 扩大、分区
MariaDB Server 可以在多个服务器上拆分数据库负载并针对扩展进行优化。 还有 Galera，一个同步多主集群。

- ColumnStore 采用大规模并行分布式数据架构，专为大数据扩展而设计，可处理 PB 级数据。
- Spider 使用分区来通过多个服务器提供数据分片。
## 压缩/存档
MyRocks 可以实现比 InnoDB 更大的压缩，以及更少的写入放大，从而提供更好的闪存存储耐久性并提高整体吞吐量。
## 连接到其他数据源
当您想使用未存储在 MariaDB 服务器数据库中的数据时。

- CONNECT 允许访问不同类型的文本文件和远程资源，就好像它们是常规的 MariaDB 表一样。
## 搜索优化
针对搜索优化的存储引擎。

- Mroonga 使用列存储提供快速的 CJK-ready 全文搜索。
## 其他专用存储引擎
- S3 存储引擎是一种只读存储引擎，可将其数据存档在 Amazon S3（或任何与 S3 API 兼容的解决方案）中。
- OQGRAPH 允许您处理层次结构（树结构）和复杂图形（在多个方向上具有许多连接的节点）。
# 开放架构：插件
MariaDB 服务器支持使用插件，软件组件可以添加到核心软件中，而无需从源代码重建 MariaDB 服务器。 因此，插件可以在启动时加载，或者在服务器运行时加载和卸载而不会中断。 插件通常用于添加所需的存储引擎、额外的安全要求以及记录有关服务器的特殊信息。

一些额外的插件包括

- 性能模式，用于监控 MariaDB 服务器性能的功能。
- MariaDB 审计插件，用于记录服务器活动，需要符合一些审计规定。
- ed25519 身份验证插件，它使用椭圆曲线数字签名算法 (ECDSA) 来安全地存储用户的密码并对用户进行身份验证，这是对基于 SHA-1 的默认身份验证的改进。
- Cracklib 密码检查插件，用于检查新密码的强度。
# 开放式开发模式
MariaDB 服务器代码库在 GitHub 上维护。

MariaDB 在 jira.mariadb.org 上有一个公共问题跟踪器。 用户可以提交、投票和评论计划的功能和错误。

# 生态系统
MariaDB Server 在大多数 Linux 发行版上都可用，在某些情况下已取代 MySQL 作为默认产品。

它与大多数开发语言、框架和云工具很好地集成在一起，并且有许多连接器可以提供帮助，其中一些由 MariaDB Corporation 开发，另一些由社区的其他成员维护。

