# 1. 概述

${cont_model} 控制器的嵌入式可编程逻辑控制器 (PLC) 是指已像软件一样安装到控制器中的 PLC 功能。用户可以编写和操作通常在 PLC 中使用的梯形图程序。

梯形图程序可以使用 HRLadder 编写或编辑，HRLadder 是专门为现代机器人设计的梯形图编辑 PC 软件，并通过以太网下载到连接的 ${cont_model} 控制器。相反，运行在 ${cont_model} 控制器上的梯形图程序可以上传到 PC 上的 HRLadder，并且可以从 HRLadder 远程监控控制器上运行的 PLC 的状态，例如模式或继电器的值。

* 您可以从现代机器人网站下载 HRLadder (https://www.hd-hyundairobotics.com/) - 客户支持 - 应用软件界面。
* 有关如何使用 HRLadder 的信息，请参考与 HRLadder 帮助菜单链接的功能手册。
* HRLadder 可用于从 Hi4 到 Hi5a 的旧控制器型号。请注意，由于 ${cont_model} 控制器的梯形图程序与旧型号控制器不同，它们之间没有兼容性。

${cont_model} 控制器的 I/O 可以通过现场总线或远程 I/O 设备连接到上游 PLC 的现场总线主机或下游现场总线从设备。嵌入式 PLC 的功能旨在使用梯形逻辑控制连接的 I/O 信号。

${cont_model} 控制器的嵌入式 PLC 的功能与 Hi5a 控制器的嵌入式 PLC 类似，并且使用相同的 HRLadder，换句话说，使用相同的梯形图编辑器。因此，已经熟悉 Hi5a 控制器嵌入式 PLC 功能的用户可以通过仅检查 ${cont_model} 控制器的不同部分快速学习本手册。

{% hint style="info" %}
因此，已经熟悉 Hi5a 控制器嵌入式 PLC 功能的用户可以通过仅检查 ${cont_model} 控制器的不同部分快速学习本手册。请您查看下面显示的链接。
[5. Hi5a 和 ${cont_model} 控制器之间的嵌入式 PLC 差异](../5-diff-hi5a-hi6.md)

{% endhint %}