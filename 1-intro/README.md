# 1. 概述

${cont_model} 控制器的嵌入式可编程逻辑控制器 (PLC) 指的是以软件的方式安装到控制器中的 PLC 功能。用户可以编写和操作在 PLC 中常用的梯形图程序。

梯形图程序可以使用 HRLadder 编写或编辑，HRLadder 是专门为现代机器人设计的梯形图编辑 PC 软件，可以通过以太网下载到连接的 ${cont_model} 控制器。相反，运行在 ${cont_model} 控制器上的梯形图程序可以上传到 PC 上的 HRLadder，控制器上运行的 PLC 模式或继电器的值等状态可以从 HRLadder 进行远程监控。

* 您可以从现代机器人网站下载 HRLadder (https://www.hd-hyundairobotics.com/) - 客户支持 - 应用软件屏幕。
* 有关如何使用 HRLadder 的信息，请参阅 HRLadder 帮助菜单链接的功能手册。
* HRLadder 可用于从 Hi4 到 Hi5a 的旧控制器型号。请注意，由于 ${cont_model} 控制器的梯形图程序与旧型号控制器不同，因此它们之间不兼容。

${cont_model} 控制器的 I/O 可以通过现场总线或远程 I/O 设备连接至上游过程 PLC 的现场总线主站或下级现场总线从站设备。嵌入式 PLC 的功能旨在使用梯形逻辑控制这些连接的 I/O 信号。

${cont_model} 控制器的嵌入式 PLC 功能与 Hi5a 控制器的嵌入式 PLC 类似，并且使用相同的 HRLadder，换句话说，相同的梯形图编辑器。因此，已经熟悉 Hi5a 控制器嵌入式 PLC 功能的用户可以通过只检查 ${cont_model} 控制器的不同部分快速从本手册中学习。

{% hint style="info" %}
因此，已经熟悉 Hi5a 控制器嵌入式 PLC 功能的用户可以通过只检查 ${cont_model} 控制器的不同部分快速从本手册中学习。请您仔细查看以下链接。
[5. Hi5a 和 ${cont_model} 控制器之间嵌入式 PLC 的差异](../5-diff-hi5a-hi6.md)

{% endhint %}