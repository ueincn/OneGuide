Git（读音为/gɪt/）是一个开源的分布式版本控制系统，可以有效、高速地处理从很小到非常大的项目版本管理。 
也是Linus Torvalds为了帮助管理Linux内核开发而开发的一个开放源码的版本控制软件。
> Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.
> Git is easy to learn and has a tiny footprint with lightning fast performance. It outclasses SCM tools like Subversion, CVS, Perforce, and ClearCase with features like cheap local branching, convenient staging areas, and multiple workflows.


---

#### 相关链接
Git官网：[https://git-scm.com/](https://git-scm.com/)
百度百科：[https://baike.baidu.com/item/GIT/12647237?fr=aladdin](https://baike.baidu.com/item/GIT/12647237?fr=aladdin)
Git所有命令列表：[https://git-scm.com/docs/git#_git_commands](https://git-scm.com/docs/git#_git_commands)
Git官方书籍：[https://git-scm.com/book/zh/v2](https://git-scm.com/book/zh/v2)
Git教程：

- Git官网文档：[https://git-scm.com/doc](https://git-scm.com/doc)
- Git培训工具包：[https://training.github.com/](https://training.github.com/)
- 廖雪峰Git教程：[https://www.liaoxuefeng.com/wiki/896043488029600](https://www.liaoxuefeng.com/wiki/896043488029600)

---

### Git 特性

- 近乎所有操作都是本地执行
   - 在 Git 中的绝大多数操作都只需要访问本地文件和资源，一般不需要来自网络上其它计算机的信息。
   - 要浏览项目的历史，Git 不需外连到服务器去获取历史，然后再显示出来——它只需直接从本地数据库中读取。
- 保证完整性
   - Git 中所有的数据在存储前都计算校验和，然后以校验和来引用。 这意味着不可能在 Git 不知情时更改任何文件内容或目录内容。 这个功能建构在 Git 底层，是构成 Git 哲学不可或缺的部分。 若你在传送过程中丢失信息或损坏文件，Git 就能发现。
   - Git 用以计算校验和的机制叫做 SHA-1 散列（hash，哈希）。 这是一个由 40 个十六进制字符（0-9 和 a-f）组成的字符串，基于 Git 中文件的内容或目录结构计算出来。
   - 实际上，Git 数据库中保存的信息都是以文件内容的哈希值来索引，而不是文件名。
- Git 一般只添加数据
   - 执行的 Git 操作，几乎只往 Git 数据库中 添加 数据。 
   - 很难使用 Git 从数据库中删除数据，也就是说 Git 几乎不会执行任何可能导致文件不可恢复的操作。
### Git 三种状态

- 已提交（committed）：已提交表示数据已经安全地保存在本地数据库中。
- 已修改（modified）：已修改表示修改了文件，但还没保存到数据库中。
- 已暂存（staged）：已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。
### Git 三个阶段

- 工作区：工作区是对项目的某个版本独立提取出来的内容。 这些从 Git 仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改。
- 暂存区：暂存区是一个文件，保存了下次将要提交的文件列表信息，一般在 Git 仓库目录中。 按照 Git 的术语叫做“索引”，不过一般说法还是叫“暂存区”。
- Git 目录：Git 仓库目录是 Git 用来保存项目的元数据和对象数据库的地方。 这是 Git 中最重要的部分，从其它计算机克隆仓库时，复制的就是这里的数据。
### Git 基本工作流程

1. 在工作区中修改文件。
2. 将你想要下次提交的更改选择性地暂存，这样只会将更改的部分添加到暂存区。
3. 提交更新，找到暂存区的文件，将快照永久性存储到 Git 目录。

