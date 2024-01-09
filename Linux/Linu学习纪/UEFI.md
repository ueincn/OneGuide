UEFI（Unified Extensible Firmware Interface, 统一的可扩展固件接口）
是一种用来替代 BIOS 的标准，它一开始叫 EFI，后来统一之后改叫 UEFI。对于硬盘启动而言，UEFI 的作用之一是读取硬盘上的引导信息，然后加载。
UEFI固件会遍历磁盘上的每个EFI系统分区（按照磁盘上的分区顺序），固件将查找位于特定位置的具有特定名称的文件，即\EFI\BOOT\BOOT{计算机类型简称}.EFI。
对于x86_64平台来说，计算机类型简称为x64，所以这个默认的特定文件是\EFI\BOOT\BOOTx64.EFI；对于aarch64平台来说，计算机类型简称为AA64，所以这个默认的特定文件是\EFI\BOOT\BOOTAA64.EFI。