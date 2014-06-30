# 第四章 用户态探测
systemtap最初专注于内核探测。因为有很多例子表明用户态探  测能够帮助诊断问题，所以systemtap的0.6版本增加了允许探测用户态进程的支持。systemtap能够探测用户态进程中函数的入口点和返回点，探测用户态代码中预先定义的标记，以及监控用户态事件。

systemtap需要uprobes模块，用来支持用户态探测。如果你的内核版本是3.5或3.5以后的版本，内核就已经内置了uprobes模块。你可以运行以下命令，来验证当前内核版本是否支持uprobes模块：

    grep CONFIG_UPROBES /boot/config-`uname -r`
如果内核已经集成了uprobes模块，则以上命令会输出：

    CONFIG_UPROBES=y
如果你使用的内核版本低于3.5，systemtap会自动集成uprobes模块。但是，systemtap用户态探测还需要utrace内核扩展，用来追踪用户态的各种事件。关于utrace更详细的介绍，请参考：[http://sourceware.org/systemtap/wiki/utrace](http://sourceware.org/systemtap/wiki/utrace)。验证当前运行的linux内核是否提供utrace模块支持，在shell命令行下输入以下命令：

    grep CONFIG_UTRACE /boot/config-`uname -r`
如果linux内核支持用户态探测，以上命令将会产生如下输出：

    CONFIG_UTRACE=y
