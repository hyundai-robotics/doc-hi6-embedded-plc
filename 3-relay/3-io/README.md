# 3.3 输入/输出

${cont_model} 机器人控制器的 I/O 图示如下所示。

![](../../_assets/io-diagram.png)

图 3.1 I/O 图示

<br><br>

图右侧的浅绿色框是 ${cont_model} 控制器内部的硬件模块。左侧是主模块 (COM 模块)，主软件在此运行。与此同时，右侧是 Hilscher 通信接口 (CIF) 卡，这是用于连接现场总线的外部组件互连 (PCI) 卡，以及用于连接 Modbus 的串行或以太网设备。

在主软件中，以小框形式绘制了各种继电器。在 ${cont_model} 控制器中，有软件元素可以访问这些继电器，它们是 HRScript（机器人语言）、I/O 分配以及嵌入式可编程逻辑控制器 (PLC)。

<br>

### HRScript（机器人语言）
机器人语言可以通过 I/O 变量访问用户 I/O (FB.DI/DO) 继电器和存储器 (M) 继电器。然而，应该使用小写字母，而不是大写字母 (例如，fb3.dow14, mw501.)。有关输入/输出变量的详细信息，请参阅 [${cont_model} 功能手册 - 机器人语言 - I/O 变量](https://hrbook-hrc.web.app/#/view/doc-hrscript/ko/6-external-comm/1-fb-io/1-io-val?cont_model=${cont_model}) 部分。

<br>

### I/O 分配，I/O 属性
I/O 分配可以访问 FB.DI/DO 继电器。此外，可以通过设置 I/O 属性在 FB.DI/DO 中设置负逻辑、脉冲等。例如，对于 “外部停止”，这是一个输入分配，如果在 DI24 中设置负逻辑，当 DI24 信号为 0（激活）时，机器人将停止。有关更多详细信息，请参阅 [${cont_model} 操作手册 - 输入/输出信号设置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/ko-tp630/7-system/3-control-parameter/2-io-signal-setting/README?cont_model=${cont_model}) 部分。

<br>

### 嵌入式 PLC
梯形图以虚线绘制在嵌入式 PLC 框内，并且此部分通过箭头连接到两侧的继电器。梯形图从继电器接收输入，执行作者意图的算术/逻辑操作，然后将结果值传输到其他继电器。

由于梯形图双向连接到存储器、系统、定时器和计数器继电器，因此可以从继电器读取值并将值写入它们。另一方面，FB.Y（物理输出）只能写值，而 FB.X（物理输入）只能读取值。

FB.DI 从机器人语言的角度来看是输入，但这个输入是通过嵌入式 PLC 进入控制器的逻辑输入。换句话说，从嵌入式 PLC 的角度来看，它是输出。因此，梯形图只能写入它。同样，FB.DO 从嵌入式 PLC 的角度来看是输入，梯形图只能从中读取。

<br>

### 连接到外部通信
Hilscher CIF 卡需连接到物理输入和输出。有关如何将一个或多个现场总线对象映射到特定 CIF 卡的说明，请参见 [${cont_model} 操作手册 - I/O 信号设置 - DIO 块分配](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/ko-tp630/7-system/3-control-parameter/2-io-signal-setting/9-dio-block-assign?cont_model=${cont_model}）。

所有继电器都映射到 Modbus 从站功能的地址空间。有关更多详细信息，请参阅 [${cont_model} 功能手册 - Modbus](https://hrbook-hrc.web.app/#/view/doc-modbus/ko/README?cont_model=${cont_model})。