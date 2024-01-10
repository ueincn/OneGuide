uboot是从FADSROM、8xxROM、PPCBOOT逐步发展演化而来的。uboot发展至今，已经可以实现非常多的功能， 在操作系统方面，它不仅支持嵌入式Linux系统的引导，还支持NetBSD,VxWorks, QNX, RTEMS, ARTOS, LynxOS, Android等嵌入式操作系统的引导。在CPU架构方面， uboot支持PowerPC、MIPS、x86、ARM、NIOS、XScale等诸多常用系列的处理器。

一般来说BootLoader必须提供系统上电时的初始化代码，在系统上电时初始化相关环境后， BootLoader需要引导完整的操作系统，然后将控制器交给操作系统。 简单来说BootLoader是一段小程序，它在系统上电时执行，通过这段小程序可以将硬件 设备进行初始化，如CPU、SDRAM、Flash、串口、网络等，初始化完毕后调用操作系统内核。