
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - 嵌入式可编程逻辑控制器 (PLC)
[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include url="https://hrcontentsrelay-bmgae5hdbzapc4bc.koreacentral-01.azurewebsites.net/api/proxy?path=doc-common-pages/zh/precautions.md" %}
[__SOURCE](1-intro/README.md)
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
[__SOURCE](1-intro/1-ladder-logic.md)
# 1.1 梯形逻辑

梯形逻辑（Ladder Logic）或梯形图（Ladder Diagram，LD）是嵌入式PLC的主要编程方法。[除了LD，还有其他方法，如结构化文本（Structured Text，ST）、功能块图（Function Block Diagram，FBD）和顺序功能图（Sequential Function Chart，SFC），但嵌入式PLC不支持它们，后续将不再讨论。]

梯形程序之所以命名，是因为程序的结构类似于梯子。通过这一类似梯子的结构传输信号的水平连接线称为横档（rung），它包含多个指令。

![](../_assets/ladder-sample2.png)

一个机器人教学项目可以包括一个或多个梯形图，每个图可能由数十到数百个横档组成。
当可编程逻辑控制器（PLC）切换到运行模式（RUN）时，LD将被反复执行。完成一个周期所需的时间称为扫描时间（scan time），通常范围从几毫秒到几十毫秒不等。

<br>

指令由助记符（mnemonic）和操作数（operand）组成，助记符是指令的名称，操作数是要传递给指令的参数。

例如，下图中的加法（ADD）指令配置如下。

![](../_assets/ladder-add.png)

* 助记符：ADD
* 操作数1：MW5
* 操作数2：DOW2
* 操作数3：MW6

<br>

嵌入式PLC的指令可以分为多个指令组，如下所述。由于每个指令将在第4节中进行解释，本节中的指令将作为理解梯形逻辑概念的示例进行解释。

---

<br>

### 接触指令

被归类为接触指令的eXamine If Closed（XIC）是一种简单的指令，仅有一个操作数。该指令将在横档上通过- | |-符号标记的操作数显示。

![](../_assets/ladder-xic.png)

接触是一个开关，用于决定是否将施加到左侧的信号（1）传输到右侧。如果继电器DO3的值为0（未激活），接触将处于打开状态，信号无法传输。如果DO3的值为1（激活），接触将闭合，信号则可以传输。

![](../_assets/ladder-contact.png)

<br>

当几个XIC接触串联或并联连接形成一个分支时，可以创建逻辑运算表达式如AND、OR和NOT。
(![](../_assets/ladder-not.png)显示了一种反相（INV）指令，其设计用于将左侧的逻辑值的相反值传输到右侧，并且没有操作数。)

```
X1 AND (X2 OR (NOT X3))
```
![](../_assets/ladder-and-or-not.png)

<br>

### 输出线圈指令

输出能量（OTE）被分类为一种输出线圈指令。它始终放置在梯级的最右端，并用 -( )- 符号表示。该指令允许将从左侧传递的值输出到操作继电器。

如果上述逻辑操作表达式的结果输出到 Y8 继电器，它将以如下形式显示。

```
Y8 = X1 AND (X2 OR (NOT X3))
```

![](../_assets/ladder-ote.png)

<br>

### 功能指令

当左侧变为激活状态时，将执行给定操作数的特定操作。例如，在下图中，当 DO3 变为激活状态时，将执行将 MW5 和 DOW2 继电器的值相加的算术操作 ADD (+)，并将获得的总和替换到 MW6 继电器中。

```
IF DO3:
   MW6 = MW5 + DOW2
```

![](../_assets/ladder-add2.png)

比较指令也将操作结果转移到右侧。例如，在下图中，如果 DO6 变为激活状态，并且 MW8 超过 120，Y20 将被激活。

```
Y20 = DO6 AND (MW8 > 120)
```

![](../_assets/ladder-grt.png)
[__SOURCE](2-rc-setting/README.md)
# 2. 设置控制器
[__SOURCE](2-rc-setting/1-plc-mode-set.md)
# 2.1. 设置嵌入式PLC的模式

在 "[F7: Condition setting] - PLC的操作模式" 中，您可以选择嵌入式可编程逻辑控制器（PLC）的操作模式，包括 Off、Stop、R-Stop、R-Run 或 Run 模式。 R-Stop 和 R-Run 分别指代远程停止和远程运行，每个状态都表示该模式可以通过以太网连接的PC上的HRLadder远程更改。

![图 2.1 设置嵌入式PLC的模式](../_assets/plc_run_mode.png)

<br>
<br>
根据所选模式，状态将在教学挂件屏幕的右上角用图标指示。即在PLC=R-Run或PLC=Run的情况下，将显示如上图所示的PLC图标；在PLC=Off的情况下，PLC图标将消失，如下图所示；在PLC=Stop的情况下，PLC图标上将显示红色禁止标记。

![图 2.2 嵌入式PLC在关闭状态](../_assets/plc_mode_off.png)

 
![图 2.3 嵌入式PLC在停止状态](../_assets/plc_mode_stop.png)


* Off  
嵌入式PLC的功能将被关闭。当这种情况发生时，机器人控制器的逻辑输出FB0.DO0-FB9.DO959将自动作为物理输出（意味着旁路）输出，FB0.Y0-FB9.Y959，物理输入FB0.X0-FB9.X959将自动作为逻辑输入FB0.DI0-FB9.DI595输入。

* R-Stop/Stop  
嵌入式PLC的操作将被停止。R-Stop表示一种远程状态，可以通过HRLadder进行更改。如果设置了Stop模式，将无法通过HRLadder更改操作模式。 
当嵌入式PLC停止时，PLC输出信号的DI和Y继电器将自动变为0。 *(DI从机器人语言或分配的角度来看是输入，但从嵌入式PLC的角度来看是输出。)*  

* R-Run/Run  
嵌入式PLC将被执行。R-Run表示一种远程状态，可以通过HRLadder进行更改。如果设置了Run模式，将无法通过HRLadder更改操作模式。
[__SOURCE](2-rc-setting/2-tp-relay-mon.md)
# 2.2. 从控制器的教学挂件监控继电器状态

可以通过输入“[R2: 窗口调整] - [F1: 选择]”来监控继电器状态。

有关更多详细信息，请参阅 [${cont_model} 操作手册 - 6. 监控](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/ko-tp630/6-monitoring/README?cont_model=${cont_model})。
[__SOURCE](2-rc-setting/3-scan-time.md)
# 2.3. 扫描时间

在嵌入式PLC中，一个循环执行梯形文件所花费的时间将在HRLadder底部的状态栏上显示为“扫描时间”。随着梯形程序步骤的增加，执行时间也会增加，从而减慢I/O响应速度。
[__SOURCE](3-relay/README.md)
# 3. 继电器
[__SOURCE](3-relay/1-relay-is.md)
# 3.1 继电器的意义

一种处于开/关接触状态的设备，用于决定是否传输电信号，这被称为开关。与此同时，继电器是通过使用电力而非手动操作的开关。

最初，继电器是一个使用线圈的磁力控制接触的物理设备。然而，在可编程逻辑控制器（PLC）中，继电器是一个由软件控制的逻辑概念。在意义上，继电器被用作一种变量，可以存储不仅由1位组成的开/关状态，还可以是由多个比特组成的字节、字、双字或实值。
[__SOURCE](3-relay/2-relay-expression.md)
# 3.2 指定继电器

以下显示了如何在${cont_model}机器人控制器的嵌入式可编程逻辑控制器 (PLC) 中指定继电器。

`[FB{block-index}.]{relay-type}[{data-type}]{signal-index}`

例如，继电器可以如下指定。

Y1501  
FB3.DIW21

* block-index  
输入和输出继电器 (DI, DO, X, Y) 被分组为 10 个现场总线块，其对象名称范围从 FB0 到 FB9。对于物理输入和输出，每个块将映射到每个现场总线设备。  
一个现场总线块的大小分别为 120 字节 (=960 位) 用于输入和输出。

您还可以将 FB 的某些区域映射到 FN0 到 FN63 的对象名称。  
有关如何设置 FN 区域的说明，请参见下面的链接。

[操作手册: 7.3.2.12 fn 块分配](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/3-control-parameter/2-io-signal-setting/12-fn-block?cont_model=${cont_model})

* relay-type  
共有 10 种不同类型，如下所示。  
每种类型将在后面详细解释。

1) 数字输入 (DI): 这是一个逻辑输入信号，可以在 HRScript 中使用或用于分配各种输入。

2) 数字输出 (DO): 这是一个逻辑输出信号，可以在 HRScript 中使用或用于分配各种输出。

3) 系统输入 (SI): 这是一个专用输入信号，用于与公司的系统板接口。

4) 系统输出 (SO): 这是一个专用输出信号，用于与公司的系统板接口。

5) X: 这是一个物理输入信号，通过现场总线设备从控制器外部输入。

6) Y: 这是一个物理输出信号，通过现场总线设备输出到控制器外部。

7) 内存 (M): 这可以用于存储数据，并可以从 HRScript 访问。

8) 系统 (S): 这用于读取或写入控制器中的系统值。请参阅 [3.4 S 继电器](./4-sw-relay/README.md)。

9) 辅助 (R): 这是一个辅助继电器，用于临时存储过时的值，并为方便移植 Hi5a 梯形图文件而提供。建议在新的梯形图文件中使用 M 继电器。

10) 保持 (K): 这是一个辅助继电器，用于临时存储过时的值。即使在断电时，值也会被存储。为方便移植 Hi5a 梯形图文件而提供。建议在新的梯形图文件中使用 M 继电器。

| **继电器名称** | **点数** | **继电器 (位)** | **继电器 (字节)** |
| :--- | :--- | :--- | :--- |
| DI | 9600 位 (1280 字节) | FB0.DI0-FB9.DI959 | FB0.DIB0-FB9.DIB127 |
| DO | 9600 位 (1280 字节) | FB0.DO0-FB9.DO959 | FB0.DOB0-FB9.DOB127 |
| SI | 960 位 (128 字节) | SI0-SI959 | SIB0-SIB127 |
    | SO | 960 位 (128 字节) | SO0-SO959 | SOB0-SOB127 |
    | X | 9600 位 (1280 字节) | FB0.X0-FB9.X959 | FB0.XB0-FB9.XB127 |
    | Y | 9600 位 (1280 字节) | FB0.Y0-FB9.Y959 | FB0.YB0-FB9.YB127 |
    | M | 160000 位 (20000 字节) | M0-M159999 | MB0-MB19999 |
    | S | 160000 位 (20000 字节) | S0-S159999 | SB0-SB19999 |
    | R | 960 位 (128 字节) | R0-R959 | RB0-RB127 |
    | K | 960 位 (128 字节) | K0-K959 | KB0-KB127 |

* 数据类型  
有五种不同类型，如下所示。

  * 无指定：位，1 位
  * B：有符号字节，8 位
  * W：有符号字，16 位
  * L：有符号长，32 位
  * F：浮点数，32 位

  <br>
  它们只是表示 960 位相同内存空间的不同数据类型，而不是独立的内存空间。例如，DO[0-15]、DOB[0-1] 和 DOW[0] 都是相同的输出信号。

<br>

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table class="tg">
<tbody>
  <tr>
    <td class="tg-kftd">位</td>
    <td>DO0-DO7</td>
    <td>DO8-DO15</td>
    <td>DO16-DO23</td>
    <td>DO24-DO31</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">字节</td>
    <td>DOB0</td>
    <td>DOB1</td>
    <td>DOB2</td>
    <td>DOB3</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">字</td>
    <td colspan="2">DOW0</td>
<td colspan="2">DOW2</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">长整型</td>
    <td colspan="4">DOL0</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">浮点型</td>
    <td colspan="4">DOF0</td>
    <td>...</td>
  </tr>
</tbody>
</table>

<br>

* 信号索引

这是继电器类型内的0基索引。该索引将以位为单位给出用于DO，并以字节为单位给出用于DOB、DOW、DOL和DOF。

<br>
<br>

字段总线对象名称可以部分省略，如下所示。例如，DO961与FB1.DO1是相同的标识。

| **对象名称** | **DO标识** | **FB.DO标识** |
| :--- | :--- | :--- |
| FB0 | DO0-DO959 | FB0.DO0-FB0.DO959 |
| FB1 | DO960-DO1919 | FB1.DO0-FB1.DO959 |
| FB2 | DO1920-DO2879 | FB2.DO0-FB2.DO959 |
| FB3 | DO2880-DO3839 | FB3.DO0-FB3.DO959 |
| FB4 | DO3840-DO4799 | FB4.DO0-FB4.DO959 |
| FB5 | DO4800-DO5759 | FB5.DO0-FB5.DO959 |
| FB6 | DO5760-DO6719 | FB6.DO0-FB6.DO959 |
| FB7 | DO6720-DO7679 | FB7.DO0-FB7.DO959 |
| FB8 | DO7680-DO8639 | FB8.DO0-FB8.DO959 |
| FB9 | DO8640-DO9599 | FB9.DO0-FB9.DO959 |

DI和DO分别是逻辑输入和输出，可以通过机器人语言和I/O分配访问。
[__SOURCE](3-relay/3-io-diagram.md)
# 3.3 输入/输出图

${cont_model} 机器人控制器的 I/O 图如下所示。


![](../_assets/io-diagram.png)

图 3.1 I/O 图

<br><br>

图右侧的浅绿色框是 ${cont_model} 控制器内部的硬件模块。左侧是主模块 (COM 模块)，主软件在那里运行。同时，右侧是 Hilscher 通信接口 (CIF) 卡，这是用于连接现场总线的外围组件互连 (PCI) 卡，以及连接 Modbus 的串行或以太网设备。

在主软件中，有各种以小框形式绘制的继电器。在 ${cont_model} 控制器中，有访问这些继电器的软件元素，包括 HRScript（机器人语言）、I/O 分配和嵌入式可编程逻辑控制器 (PLC)。

<br>

### HRScript（机器人语言）
机器人语言可以通过 I/O 变量访问用户 I/O (FB.DI/DO) 继电器和内存 (M) 继电器。然而，需使用小写字母而不是大写字母（例如，fb3.dow14, mw501.）。有关输入/输出变量的详细信息，请参阅 [${cont_model} 功能手册 - 机器人语言 - I/O 变量](https://hrbook-hrc.web.app/#/view/doc-hrscript/ko/6-external-comm/1-fb-io/1-io-val?cont_model=${cont_model}) 部分。

<br>

### I/O 分配，I/O 属性
I/O 分配可以访问 FB.DI/DO 继电器。此外，可以通过设置 I/O 属性在 FB.DI/DO 中设置负逻辑、脉冲等。例如，对于“外部停止”，这是一个输入分配，如果在 DI24 中设置了负逻辑，当 DI24 信号为 0（有效）时，机器人将停止。有关更多详细信息，请参阅 [${cont_model} 操作手册 - 输入/输出信号设置](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/ko-tp630/7-setting/3-control-parameter/2-io-signal-setting/README?cont_model=${cont_model}) 部分。

<br>

### 嵌入式 PLC
梯形图在嵌入式 PLC 框内以虚线绘制，该部分与两侧的继电器通过箭头连接。梯形图从继电器接收输入，执行作者意图的算术/逻辑操作，然后将结果值传递给其他继电器。

由于梯形图双向连接到内存、系统、计时器和计数器继电器，因此它可以从继电器读取值并写入值。另一方面，FB.Y（物理输出）只能写入值，而 FB.X（物理输入）只能读取值。

FB.DI 从机器人语言的角度来看是一个输入，但这个输入是通过嵌入式 PLC 进入控制器的逻辑输入。换句话说，从嵌入式 PLC 的角度，它是一个输出。因此，梯形图只能写入它。同样，由于 FB.DO 从嵌入式 PLC 的角度来看是一个输入，梯形图只能从中读取。

<br>

### 连接到外部通信
Hilscher CIF 卡需要连接到物理输入和输出。有关如何将一个或多个现场总线对象映射到特定 CIF 卡的信息，请参阅 [${cont_model} 操作手册 - I/O 信号设置 - DIO 块分配](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/ko-tp630/7-setting/3-control-parameter/2-io-signal-setting/9-dio-block-assign?cont_model=${cont_model})。

所有继电器都映射到 Modbus 从功能的地址空间。有关更多详细信息，请参阅 [${cont_model} 功能手册 - Modbus](https://hrbook-hrc.web.app/#/view/doc-modbus/ko/README?cont_model=${cont_model})。
[__SOURCE](3-relay/3-sio/1-so.md)
# 3.3.1 SO - 系统输出

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>系统板</th>
		<th>字节</th>
		<th>位</th>
		<th>名称</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td rowspan=32>BD630</td>
		<td rowspan=4>sob0</td>
		<td>so0</td>
		<td>电机开启 (TP)</td>
	</tr>
	<tr>
		<td>so1</td>
		<td>启动 (TP)</td>
	</tr>
	<tr>
		<td>so2</td>
		<td>停止 (TP)</td>
	</tr>
	<tr>
		<td>so3</td>
		<td>系统错误</td>
	</tr>
	<tr>
		<td rowspan=8>sob1</td>
		<td>so8</td>
		<td>远程自动模式</td>
	</tr>
	<tr>
		<td>so9</td>
		<td>TP 断开</td>
	</tr>
	<tr>
		<td>so10</td>
		<td>ESCON(释放)</td>
	</tr>
<<<SOURCE_MARKDOWN_START>>>	<tr>
		<td>so11</td>
		<td>停止类别 1</td>
	</tr>	
	<tr>
		<td>so12</td>
		<td>停止类别 2</td>
	</tr>	
	<tr>
		<td>so13</td>
		<td>心跳 1</td>
	</tr>	
	<tr>
		<td>so14</td>
		<td>心跳 2</td>
	</tr>	
	<tr>
		<td>so15</td>
		<td>心跳 3</td>
	</tr>	
	<tr>
		<td rowspan=3>sob2</td>
		<td>so16</td>
		<td>系统错误接收</td>
	</tr>
	<tr>
		<td>so17</td>
		<td>系统停止</td>
	</tr>
	<tr>
		<td>so18</td>
		<td>自我诊断正常</td>
	</tr>	
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640 - 1</td>
		<td rowspan=8>sob4</td>
		<td>so32</td>
		<td>刹车控制 1</td>
	</tr>
	<tr>
		<td>so33</td>
		<td>刹车控制 2</td>
	</tr>
	<tr>
		<td>so34</td>
		<td>刹车控制 3</td>
	</tr><<<SOURCE_MARKDOWN_END>>>
<<<SOURCE_MARKDOWN_START>>>	<tr>
		<td>so35</td>
		<td>刹车控制 4</td>
	</tr>
	<tr>
		<td>so36</td>
		<td>刹车控制 5</td>
	</tr>
	<tr>
		<td>so37</td>
		<td>刹车控制 6</td>
	</tr>
	<tr>
		<td>so38</td>
		<td>刹车控制 7</td>
	</tr>
	<tr>
		<td>so39</td>
		<td>刹车控制 8</td>
	</tr>
	<tr>
		<td rowspan=2>sob5</td>
		<td>so42</td>
		<td>动态刹车</td>
	</tr>
	<tr>
		<td>so43</td>
		<td>动态刹车模式</td>
	</tr>
	<tr>
		<td rowspan=8>sob6</td>
		<td>so48</td>
		<td>用户 1</td>
	</tr>
	<tr>
		<td>so49</td>
		<td>用户 2</td>
	</tr>
	<tr>
		<td>so50</td>
		<td>用户 3</td>
	</tr>
	<tr>
		<td>so51</td>
		<td>用户 4</td>
	</tr>
	<tr>
		<td>so52</td>
		<td>用户 5 (BD640T)</td>
	</tr><<<SOURCE_MARKDOWN_END>>>
```html
<tr>
		<td>so53</td>
		<td>用户 6 (BD640T)</td>
	</tr>
	<tr>
		<td>so54</td>
		<td>用户 7 (BD640T)</td>
	</tr>
	<tr>
		<td>so55</td>
		<td>用户 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=1>sob7</td>
		<td>so56</td>
		<td>自我诊断正常</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640 - 2</td>
		<td rowspan=8>sob8</td>
		<td>so64</td>
		<td>刹车控制 1</td>
	</tr>
	<tr>
		<td>so65</td>
		<td>刹车控制 2</td>
	</tr>
	<tr>
		<td>so66</td>
		<td>刹车控制 3</td>
	</tr>
	<tr>
		<td>so67</td>
		<td>刹车控制 4</td>
	</tr>
	<tr>
		<td>so68</td>
		<td>刹车控制 5</td>
	</tr>
	<tr>
		<td>so69</td>
		<td>刹车控制 6</td>
	</tr>
	<tr>
		<td>so70</td>
		<td>刹车控制 7</td>
	</tr>
```
```html
<tr>
		<td>so71</td>
		<td>刹车控制 8</td>
	</tr>
	<tr>
		<td rowspan=2>sob9</td>
		<td>so74</td>
		<td>动态刹车</td>
	</tr>
	<tr>
		<td>so75</td>
		<td>动态刹车模式</td>
	</tr>
	<tr>
		<td rowspan=8>sob10</td>
		<td>so80</td>
		<td>用户 1</td>
	</tr>
	<tr>
		<td>so81</td>
		<td>用户 2</td>
	</tr>
	<tr>
		<td>so82</td>
		<td>用户 3</td>
	</tr>
	<tr>
		<td>so83</td>
		<td>用户 4</td>
	</tr>
	<tr>
		<td>so84</td>
		<td>用户 5 (BD640T)</td>
	</tr>
	<tr>
		<td>so85</td>
		<td>用户 6 (BD640T)</td>
	</tr>
	<tr>
		<td>so86</td>
		<td>用户 7 (BD640T)</td>
	</tr>
	<tr>
		<td>so87</td>
		<td>用户 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=1>sob11</td>
		<td>so88</td>
		<td>自我诊断正常</td>
```
</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640 - 3</td>
		<td rowspan=8>sob12</td>
		<td>so96</td>
		<td>刹车控制 1</td>
	</tr>
	<tr>
		<td>so97</td>
		<td>刹车控制 2</td>
	</tr>
	<tr>
		<td>so98</td>
		<td>刹车控制 3</td>
	</tr>
	<tr>
		<td>so99</td>
		<td>刹车控制 4</td>
	</tr>
	<tr>
		<td>so100</td>
		<td>刹车控制 5</td>
	</tr>
	<tr>
		<td>so101</td>
		<td>刹车控制 6</td>
	</tr>
	<tr>
		<td>so102</td>
		<td>刹车控制 7</td>
	</tr>
	<tr>
		<td>so103</td>
		<td>刹车控制 8</td>
	</tr>
	<tr>
		<td rowspan=2>sob13</td>
		<td>so106</td>
		<td>动态刹车</td>
	</tr>
	<tr>
		<td>so107</td>
		<td>动态刹车模式</td>
	</tr>
	<tr>
		<td rowspan=8>sob14</td>
		<td>so112</td><
<td>用户 1</td>
	</tr>
	<tr>
		<td>so113</td>
		<td>用户 2</td>
	</tr>
	<tr>
		<td>so114</td>
		<td>用户 3</td>
	</tr>
	<tr>
		<td>so115</td>
		<td>用户 4</td>
	</tr>
	<tr>
		<td>so116</td>
		<td>用户 5 (BD640T)</td>
	</tr>
	<tr>
		<td>so117</td>
		<td>用户 6 (BD640T)</td>
	</tr>
	<tr>
		<td>so118</td>
		<td>用户 7 (BD640T)</td>
	</tr>
	<tr>
		<td>so119</td>
		<td>用户 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=1>sob15</td>
		<td>so120</td>
		<td>自我诊断正常</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640 - 4</td>
		<td rowspan=8>sob16</td>
		<td>so128</td>
		<td>刹车控制 1</td>
	</tr>
	<tr>
		<td>so129</td>
		<td>刹车控制 2</td>
	</tr>
	<tr>
		<td>so130</td>
```html
<td>制动控制 3</td>
</tr>
<tr>
	<td>so131</td>
	<td>制动控制 4</td>
</tr>
<tr>
	<td>so132</td>
	<td>制动控制 5</td>
</tr>
<tr>
	<td>so133</td>
	<td>制动控制 6</td>
</tr>
<tr>
	<td>so134</td>
	<td>制动控制 7</td>
</tr>
<tr>
	<td>so135</td>
	<td>制动控制 8</td>
</tr>
<tr>
	<td rowspan=2>sob17</td>
	<td>so138</td>
	<td>动态制动</td>
</tr>
<tr>
	<td>so139</td>
	<td>动态制动模式</td>
</tr>
<tr>
	<td rowspan=8>sob18</td>
	<td>so144</td>
	<td>用户 1</td>
</tr>
<tr>
	<td>so145</td>
	<td>用户 2</td>
</tr>
<tr>
	<td>so146</td>
	<td>用户 3</td>
</tr>
<tr>
	<td>so147</td>
	<td>用户 4</td>
</tr>
<tr>
	<td>so148</td>
```
<td>用户 5 (BD640T)</td>
	</tr>
	<tr>
		<td>so149</td>
		<td>用户 6 (BD640T)</td>
	</tr>
	<tr>
		<td>so150</td>
		<td>用户 7 (BD640T)</td>
	</tr>
	<tr>
		<td>so151</td>
		<td>用户 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=1>sob19</td>
		<td>so152</td>
		<td>自我诊断正常</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640T 输送机</td>
		<td rowspan=4>sob20</td>
		<td>so160</td>
		<td>通道1 - 脉冲计数类型 (0=上升, 1=上下)</td>
	</tr>
	<tr>
		<td>so161</td>
		<td>通道1- 通信类型 (0=线路驱动器, 1=开集电极)</td>
	</tr>
	<tr>
		<td>so162</td>
		<td>通道2 - 脉冲计数类型 (0=上升, 1=上下)</td>
	</tr>
	<tr>
		<td>so163</td>
		<td>通道2- 通信类型 (0=线路驱动器, 1=开集电极)</td>
	</tr>
</tbody>

</table>
[__SOURCE](3-relay/3-sio/2-si.md)
# 3.3.2 SI - 系统输入

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>系统板</th>
		<th>字节</th>
		<th>位</th>
		<th>名称</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td rowspan=32>BD630</td>
		<td rowspan=8>sib0</td>
		<td>si0</td>
		<td>提升轴/臂限位</td>
	</tr>
	<tr>
		<td>si1</td>
		<td>主轴限位</td>
	</tr>
	<tr>
		<td>si2</td>
		<td>附加轴限位</td>
	</tr>
	<tr>
		<td>si3</td>
		<td>扩展轴限位</td>
	</tr>
	<tr>
		<td>si4</td>
		<td>紧急停止 (OP)</td>
	</tr>
	<tr>
		<td>si5</td>
		<td>紧急停止 (TP)</td>
	</tr>
	<tr>
		<td>si6</td>
		<td>紧急停止 (Ext)</td>
	</tr>
```html
<td>si7</td>
<td>安全链</td>
</tr>
<tr>
<td rowspan=7>sib1</td>
<td>si8</td>
<td>模式切换（自动）</td>
</tr>
<tr>
<td>si9</td>
<td>模式切换（手动）</td>
</tr>
<tr>
<td>si10</td>
<td>模式切换（远程）</td>
</tr>	
<tr>
<td>si11</td>
<td>TP启用开关</td>
</tr>	
<tr>
<td>si12</td>
<td>安全防护（自动）</td>
</tr>	
<tr>
<td>si13</td>
<td>安全防护（自动扩展）</td>
</tr>	
<tr>
<td>si14</td>
<td>安全防护（一般）</td>
</tr>	
<tr>
<td rowspan=8>sib2</td>
<td>si16</td>
<td>预充电</td>
</tr>
<tr>
<td>si17</td>
<td>电机电源</td>
</tr>
<tr>
<td>si18</td>
<td>放电</td>
</tr>	
<tr>
<td>si19</td>
<td>电机开启（TP）</td>
</tr>	
```
```html
<td>si20</td>
<td>启动 (TP)</td>
</tr>	
<tr>
<td>si21</td>
<td>停止 (TP)</td>
</tr>	
<tr>
<td>si22</td>
<td>操作员已安装</td>
</tr>	
<tr>
<td>si23</td>
<td>电机开启(外部)</td>
</tr>	
<tr>
<td rowspan=2>sib3</td>
<td>si24</td>
<td>心跳 1</td>
</tr>
<tr>
<td>si25</td>
<td>心跳 2</td>
</tr>
</tbody>

<tbody>
<tr>
<td rowspan=32>BD640 - 1</td>
<td rowspan=8>sib4</td>
<td>si32</td>
<td>刹车状态 1</td>
</tr>
<tr>
<td>si33</td>
<td>刹车状态 2</td>
</tr>
<tr>
<td>si34</td>
<td>刹车状态 3</td>
</tr>
<tr>
<td>si35</td>
<td>刹车状态 4</td>
</tr>
<tr>
<td>si36</td>
<td>刹车状态 5</td>
</tr>
```
<td>si37</td>
		<td>刹车状态 6</td>
	</tr>
	<tr>
		<td>si38</td>
		<td>刹车状态 7</td>
	</tr>
	<tr>
		<td>si39</td>
		<td>刹车状态 8</td>
	</tr>
	<tr>
		<td rowspan=8>sib5</td>
		<td>si40</td>
		<td>预充电继电器开启</td>
	</tr>
	<tr>
		<td>si41</td>
		<td>动态电阻过热</td>
	</tr>
	<tr>
		<td>si42</td>
		<td>过电压</td>
	</tr>
	<tr>
		<td>si43</td>
		<td>欠电压</td>
	</tr>
	<tr>
		<td>si44</td>
		<td>动态刹车状态</td>
	</tr>
	<tr>
		<td>si45</td>
		<td>/SVON (伺服开启)</td>
	</tr>
	<tr>
		<td>si46</td>
		<td>机器人风扇故障</td>
	</tr>
	<tr>
		<td>si47</td>
		<td>二极管模块过热</td>
	</tr>
	<tr>
		<td rowspan=8>sib6</td>
		<td>si48</td>
		<td>用户 1</td>
	</tr>
<td>si49</td>
<td>用户 2</td>
</tr>
<tr>
<td>si50</td>
<td>用户 3</td>
</tr>
<tr>
<td>si51</td>
<td>用户 4</td>
</tr>
<tr>
<td>si52</td>
<td>用户 5 (BD640T)</td>
</tr>
<tr>
<td>si53</td>
<td>用户 6 (BD640T)</td>
</tr>
<tr>
<td>si54</td>
<td>用户 7 (BD640T)</td>
</tr>
<tr>
<td>si55</td>
<td>用户 8 (BD640T)</td>
</tr>
<tr>
<td rowspan=2>sib7</td>
<td>si56</td>
<td>制动电源故障</td>
</tr>
<tr>
<td>si57</td>
<td>交流电压下降</td>
</tr>
</tbody>

<tbody>
<tr>
<td rowspan=32>BD640 - 2</td>
<td rowspan=8>sib8</td>
<td>si64</td>
<td>制动状态 1</td>
</tr>
<tr>
<td>si65</td>
<td>制动状态 2</td>
</tr>
<tr>
```html
<td>si66</td>
		<td>刹车状态 3</td>
	</tr>
	<tr>
		<td>si67</td>
		<td>刹车状态 4</td>
	</tr>
	<tr>
		<td>si68</td>
		<td>刹车状态 5</td>
	</tr>
	<tr>
		<td>si69</td>
		<td>刹车状态 6</td>
	</tr>
	<tr>
		<td>si70</td>
		<td>刹车状态 7</td>
	</tr>
	<tr>
		<td>si71</td>
		<td>刹车状态 8</td>
	</tr>
	<tr>
		<td rowspan=8>sib9</td>
		<td>si72</td>
		<td>预充电继电器开启</td>
	</tr>
	<tr>
		<td>si73</td>
		<td>动态电阻过热</td>
	</tr>
	<tr>
		<td>si74</td>
		<td>过电压</td>
	</tr>
	<tr>
		<td>si75</td>
		<td>欠电压</td>
	</tr>
	<tr>
		<td>si76</td>
		<td>动态刹车状态</td>
	</tr>
	<tr>
		<td>si77</td>
		<td>/SVON (伺服开启)</td>
	</tr>
	<tr>
		<td>si78</td>
```
<td>机器人风扇故障</td>
	</tr>
	<tr>
		<td>si79</td>
		<td>二极管模块过热</td>
	</tr>
	<tr>
		<td rowspan=8>sib10</td>
		<td>si80</td>
		<td>用户 1</td>
	</tr>
	<tr>
		<td>si81</td>
		<td>用户 2</td>
	</tr>
	<tr>
		<td>si82</td>
		<td>用户 3</td>
	</tr>
	<tr>
		<td>si83</td>
		<td>用户 4</td>
	</tr>
	<tr>
		<td>si84</td>
		<td>用户 5 (BD640T)</td>
	</tr>
	<tr>
		<td>si85</td>
		<td>用户 6 (BD640T)</td>
	</tr>
	<tr>
		<td>si86</td>
		<td>用户 7 (BD640T)</td>
	</tr>
	<tr>
		<td>si87</td>
		<td>用户 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=2>sib11</td>
		<td>si88</td>
		<td>刹车电源故障</td>
	</tr>
	<tr>
		<td>si89</td>
		<td>交流电压下降</td>
	</tr>
</tbody>
<tbody>
	<tr>
		<td rowspan=32>BD640 - 3</td>
		<td rowspan=8>sib12</td>
		<td>si96</td>
		<td>刹车状态 1</td>
	</tr>
	<tr>
		<td>si97</td>
		<td>刹车状态 2</td>
	</tr>
	<tr>
		<td>si98</td>
		<td>刹车状态 3</td>
	</tr>
	<tr>
		<td>si99</td>
		<td>刹车状态 4</td>
	</tr>
	<tr>
		<td>si100</td>
		<td>刹车状态 5</td>
	</tr>
	<tr>
		<td>si101</td>
		<td>刹车状态 6</td>
	</tr>
	<tr>
		<td>si102</td>
		<td>刹车状态 7</td>
	</tr>
	<tr>
		<td>si103</td>
		<td>刹车状态 8</td>
	</tr>
	<tr>
		<td rowspan=8>sib13</td>
		<td>si104</td>
		<td>预充电继电器打开</td>
	</tr>
	<tr>
		<td>si105</td>
		<td>动态电阻过热</td>
	</tr>
	<tr>
		<td>si106</td>
		<td>过电压</td>
	</tr>
	<tr>
		<td>si107</td>
```
<td>欠压</td>
	</tr>
	<tr>
		<td>si108</td>
		<td>动态制动状态</td>
	</tr>
	<tr>
		<td>si109</td>
		<td>/SVON (伺服开启)</td>
	</tr>
	<tr>
		<td>si110</td>
		<td>机器人风扇故障</td>
	</tr>
	<tr>
		<td>si111</td>
		<td>二极管模块过热</td>
	</tr>
	<tr>
		<td rowspan=8>sib14</td>
		<td>si112</td>
		<td>用户 1</td>
	</tr>
	<tr>
		<td>si113</td>
		<td>用户 2</td>
	</tr>
	<tr>
		<td>si114</td>
		<td>用户 3</td>
	</tr>
	<tr>
		<td>si115</td>
		<td>用户 4</td>
	</tr>
	<tr>
		<td>si116</td>
		<td>用户 5 (BD640T)</td>
	</tr>
	<tr>
		<td>si117</td>
		<td>用户 6 (BD640T)</td>
	</tr>
	<tr>
		<td>si118</td>
		<td>用户 7 (BD640T)</td>
	</tr>
	<tr>
		<td>si119</td>
		<td>用户 8 (BD640T)</td>
```
</tr>
	<tr>
		<td rowspan=2>sib15</td>
		<td>si120</td>
		<td>制动功率故障</td>
	</tr>
	<tr>
		<td>si121</td>
		<td>交流电压下降</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640 - 4</td>
		<td rowspan=8>sib16</td>
		<td>si128</td>
		<td>制动状态 1</td>
	</tr>
	<tr>
		<td>si129</td>
		<td>制动状态 2</td>
	</tr>
	<tr>
		<td>si130</td>
		<td>制动状态 3</td>
	</tr>
	<tr>
		<td>si131</td>
		<td>制动状态 4</td>
	</tr>
	<tr>
		<td>si132</td>
		<td>制动状态 5</td>
	</tr>
	<tr>
		<td>si133</td>
		<td>制动状态 6</td>
	</tr>
	<tr>
		<td>si134</td>
		<td>制动状态 7</td>
	</tr>
	<tr>
		<td>si135</td>
		<td>制动状态 8</td>
	</tr>
	<tr>
		<td rowspan=8>sib17</td>
		<td>si136</td>
<<<SOURCE_MARKDOWN_START>>>		<td>预充电继电器开启</td>
	</tr>
	<tr>
		<td>si137</td>
		<td>动态电阻过热</td>
	</tr>
	<tr>
		<td>si138</td>
		<td>过电压</td>
	</tr>
	<tr>
		<td>si139</td>
		<td>欠电压</td>
	</tr>
	<tr>
		<td>si140</td>
		<td>动态刹车状态</td>
	</tr>
	<tr>
		<td>si141</td>
		<td>/SVON (伺服开启)</td>
	</tr>
	<tr>
		<td>si142</td>
		<td>机器人风扇故障</td>
	</tr>
	<tr>
		<td>si143</td>
		<td>二极管模块过热</td>
	</tr>
	<tr>
		<td rowspan=8>sib18</td>
		<td>si144</td>
		<td>用户 1</td>
	</tr>
	<tr>
		<td>si145</td>
		<td>用户 2</td>
	</tr>
	<tr>
		<td>si146</td>
		<td>用户 3</td>
	</tr>
	<tr>
		<td>si147</td>
		<td>用户 4</td>
	</tr>
	<tr>
		<td>si148</td>
		<td>用户 5 (BD640T)</td><<<SOURCE_MARKDOWN_END>>>
```
</tr>
	<tr>
		<td>si149</td>
		<td>用户 6 (BD640T)</td>
	</tr>
	<tr>
		<td>si150</td>
		<td>用户 7 (BD640T)</td>
	</tr>
	<tr>
		<td>si151</td>
		<td>用户 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=2>sib19</td>
		<td>si152</td>
		<td>刹车电源故障</td>
	</tr>
	<tr>
		<td>si153</td>
		<td>交流电压下降</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640T 输送机</td>
		<td rowspan=1>sib42<br>sib43</td>
		<td></td>
		<td>通道1 - 脉冲计数器 (16位)</td>
	</tr>
	<tr>
		<td rowspan=1>sib44<br>sib45</td>
		<td></td>
		<td>通道2 - 脉冲计数器 (16位)</td>
	</tr>
	<tr>
		<td rowspan=4>sib46</td>
		<td>si368</td>
		<td>通道1 - 线路错误</td>
	</tr>
	<tr>
		<td>si369</td>
		<td>通道1 - 限位开关</td>
	</tr>
	<tr>
		<td>si370</td>
		<td>通道2 - 线路错误</td>
	</tr>
```
<td>si371</td>
<td>ch2- 限位开关</td>
</tr>
</tbody>

</table>
[__SOURCE](3-relay/4-sw-relay/README.md)
# 3.4 S 继电器

在 ${cont_model} 控制器中，各种状态的值映射到 S 继电器。通过向某些 S 继电器写入值，也可以改变 ${cont_model} 的状态。

因此，外部设备，例如过程可编程逻辑控制器 (PLC) 或个人计算机 (PC)，可以通过读取 S 继电器的值，通过现场总线、Modbus 等远程监控 ${cont_model} 控制器的状态，并且可以通过向 S 继电器写入值远程控制 ${cont_model} 控制器。

S 继电器的区域可以大致分为以下两个部分。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
	<tr>
		<th>地址</th>
		<th>内容</th>
	</tr>
	<tr>
		<td>SB00000-SB01999</td>
		<td>固定区域</td>
	</tr>
	<tr>
		<td>SB02000-SB19999</td>
		<td>可选项区域 (插槽)</td>
	</tr>
</table>

<br>

### 固定区域
经常使用的基本项分配到预定地址。无法通过设置更改或分配项目。固定区域的映射将在下一节中描述。

<br>

### 可选项区域
该区域由总共 900 个插槽组成，每个插槽 20 字节。每个插槽的配置将由放入首个字的命令值决定。每个命令的映射将在下一节中描述。

<table class="tg">
<thead>
	<tr>
		<th>插槽索引</th>
		<th>s 索引:偏移量</th>
		<th>字段</th>
	</tr>
</thead>
<tbody>
	<tr>
```html
<td rowspan=10>插槽 0</td>
<td>2000:0</td>
<td>命令（传统做法：获取偶数，设置奇数）</td>
</tr>
<tr>
	<td>:2</td>
	<td rowspan=2>参数</td>
</tr>
<tr>
	<td>:4</td>
</tr>
<tr>
	<td>:6</td>
	<td rowspan=5>结果</td>
</tr>
<tr><td>:8</td></tr>
<tr><td>:10</td></tr>
<tr><td>:12</td></tr>
<tr><td>:14</td></tr>
<tr><td>:16</td><td class='grayed'></td></tr>
<tr><td>:18</td><td class='grayed'></td></tr>
<tr>
	<td rowspan=10>插槽 1</td>
	<td>2020:0</td>
	<td>命令</td>
</tr>
<tr>
	<td>:2</td>
	<td>参数</td>
</tr>
<tr>
	<td>:4</td>
	<td rowspan=2>结果</td>
</tr>
<tr>
	<td>:6</td>
</tr>
<tr><td>:8</td><td class='grayed'></td></tr>
<tr><td>:10</td><td class='grayed'></td></tr>
<tr><td>:12</td><td class='grayed'></td></tr>
<tr><td>:14</td><td class='grayed'></td></tr>
<tr><td>:16</td><td class='grayed'></td></tr>
<tr><td>:18</td><td class='grayed'></td></tr>
<tr>
	<td rowspan=3>插槽 2</td>
	<td>2040:0</td>
	<td>命令</td>
</tr>
<tr>
	<td>:2</td>
```
<td>参数</td>
	</tr>
	<tr>
		<td>...</td>
		<td>...</td>
	</tr>
	<tr>
		<td>...</td>
		<td>...</td>
		<td>...</td>
	</tr>
	<tr>
		<td rowspan=3>槽 899</td>
		<td>19980:0</td>
		<td>命令</td>
	</tr>
	<tr>
		<td>:2</td>
		<td>参数</td>
	</tr>
	<tr>
		<td>...</td>
		<td>...</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/1-fixed-area.md)
# 3.4.1 S 继电器 - 固定区域

请参考下表中提供的 SB0-SB1999 区域的固定项目。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.bit { width: 10%; }
</style>

### 特殊标志区域

<table class="tg">
<thead>
	<tr>
		<th class='bit'>继电器</th>
		<th class='bit'>bit7</th>
		<th class='bit'>bit6</th>
		<th class='bit'>bit5</th>
		<th class='bit'>bit4</th>
		<th class='bit'>bit3</th>
		<th class='bit'>bit2</th>
		<th class='bit'>bit1</th>
		<th class='bit'>bit0</th>		
		<th class='bit'>备注</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>SB0</td>
		<td>如果在操作中发生进位则开启</td>
		<td>如果无法进行 BCD 操作则开启</td>
		<td>1秒时钟</td>
		<td>0.2秒时钟</td>
		<td>0.1秒时钟</td>
		<td>仅在一个扫描周期内开启</td>
		<td>始终关闭</td>
		<td>始终开启</td>		
		<td></td>
	</tr>
	<tr>
		<td>SB1</td>
		<td class='grayed'></td>
		<td>当标签为 0 或更低时，或没有跳转标签时则开启</td>
		<td>如果标签重复则开启</td>
		<td>如果标签数量超过 100 则开启</td>
		<td>如果标签不是常数则开启</td>
		<td class='grayed'></td>
		<td>4秒时钟</td>
<td>2秒时钟</td>
		<td></td>
	</tr>
	<tr>
		<td>SB2</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td>当没有通过Call调用的子梯形图时开启</td>
		<td>当扫描时间超过5秒时开启</td>
		<td></td>
	</tr>
	<tr>
		<td>SB3</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td>自我诊断完成</td>
		<td>T/P启动完成</td>
		<td></td>
	</tr>
</tbody>
</table>

<br>

### 基本信息区域

<table class="tg">
<thead>
	<tr>
		<th>继电器</th>
		<th>描述</th>
		<th>备注</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>SB4</th>
		<td>PLC执行模式<br>
		(0=停止, 1=R.停止, 2=R.运行, 3=运行, 4=关闭, 5=无程序)</td>
		<td></td>
	</tr>
<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
<tr>
	<td>SW6</td>
	<td>日期/时间：年份</td>
</tr>
<tr>
	<td>SB8</td>
	<td>日期/时间：月份</td>
	<td></td>
</tr>
<tr>
	<td>SB9</td>
	<td>日期/时间：日期</td>
	<td></td>
</tr>	
<tr>
	<td>SB10</td>
	<td>日期/时间：小时</td>
	<td></td>
</tr>	
<tr>
	<td>SB11</td>
	<td>日期/时间：分钟</td>
	<td></td>
</tr>	
<tr>
	<td>SB12</td>
	<td>日期/时间：秒</td>
	<td></td>
</tr>	
<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
<tr>
	<td>SB14</td>
	<td>软件版本：第一<br>
	例如，在 V60.05-08 的情况下，SB14:60, SB15:5, SB16:8</td>
	<td></td>
</tr>
<tr>
	<td>SB15</td>
	<td>软件版本：第二</td>
	<td></td>
</tr>
<tr>
	<td>SB16</td>
	<td>软件版本：小修复</td>
	<td></td>
</tr>
<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
<tr>
	<td>SW18</td>
<td>扫描时间</td>
<td>毫秒</td>
</tr>
<tr>
<td>SW20</td>
<td>分配时间</td>
<td>微秒</td>
</tr>
<tr>
<td>SW22</td>
<td>最大占用时间</td>
<td>毫秒</td>
</tr>
<tr>
<td>SW24</td>
<td>平均占用时间</td>
<td>毫秒</td>
</tr>
<tr>
<td>SW26</td>
<td>梯子中的总步骤数</td>
<td></td>
</tr>
<tr>
<td>SW28</td>
<td>占用比例</td>
<td>%</td>
</tr>
<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td>SB30</td>
<td>枪输出状态</td>
<td></td>
</tr>
<tr>
<td>SB39</td>
<td>当前用户坐标号</td>
<td></td>
</tr>
<tr>
<td>SB40</td>
<td>当前工具编号</td>
<td></td>
</tr>
<tr>
<td>SB41</td>
<td>机器人状态 (0=停止, 1=运行, 2=等待)</td>
<td></td>
</tr>
<tr>
<td>SB42</td>
		<td>播放速度</td>
		<td>%</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW44</td>
		<td>手动速度</td>
		<td>mm/s</td>
	</tr>
	<tr>
		<td>SW46</td>
		<td>工具尖端移动速度</td>
		<td>mm/s</td>
	</tr>
	<tr>
		<td>SW48</td>
		<td>错误/警告编号</td>
		<td></td>
	</tr>
	<tr>
		<td>SW50</td>
		<td>错误/警告辅助信息</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW60</td>
		<td>间接地址指定 1</td>
		<td></td>
	</tr>
	<tr>
		<td>SW62</td>
		<td>间接地址指定 2</td>
		<td></td>
	</tr>
	<tr>
		<td>SW64</td>
		<td>间接地址指定 3</td>
		<td></td>
	</tr>
	<tr>
		<td>SW66</td>
		<td>间接地址指定 4</td>
		<td></td>
	</tr>
	<tr>
		<td>SW68</td>
		<td>间接地址指定 5</td>
		<td></td>
</tr>
	<tr>
		<td>SW70</td>
		<td>间接地址指定 6</td>
		<td></td>
	</tr>
	<tr>
		<td>SW72</td>
		<td>间接地址指定 7</td>
		<td></td>
	</tr>
	<tr>
		<td>SW74</td>
		<td>间接地址指定 8</td>
		<td></td>
	</tr>
	<tr>
		<td>SW76</td>
		<td>间接地址指定 9</td>
		<td></td>
	</tr>
	<tr>
		<td>SW78</td>
		<td>间接地址指定 10</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB88</br>
		...</br>
		SB99</td>
		<td>教学挂件按键输入状态</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW100</td>
		<td>主程序编号</td>
		<td>主任务</td>
	</tr>
	<tr>
		<td>SW102</td>
		<td>步骤编号</td>
		<td>主任务</td>
	</tr>
	<tr>
		<td>SW104</td>
		<td>功能编号</td>
		<td>主任务</td>
	</tr>
<tr>
		<td>SW106</td>
		<td>主程序编号</td>
		<td>主任务</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB109</td>
		<td>运行时间选择<br>
		(1=总计（初始化后），2=总计（电源输入后），3=上一个周期，4=当前周期)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL110</td>
		<td>电机开启（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL114</td>
		<td>电机开启（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL118</td>
		<td>运行时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL122</td>
		<td>运行时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL126</td>
		<td>移动时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL130</td>
		<td>移动时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL134</td>
		<td>周期计数</td>
		<td></td>
	</tr>
	<tr>
		<td>SL138</td>
		<td>等待，二进制等待时间（天）</td>
```html
<td></td>
	</tr>
	<tr>
		<td>SL142</td>
		<td>等待，延迟时间 (毫秒)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL146</td>
		<td>延迟等待时间 (天)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL150</td>
		<td>延迟等待时间 (毫秒)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB159</td>
		<td>轴信息选择<br>
		1=当前的位置 (轴角度)， 2=当前的位置 (基坐标)， 3=当前的位置 (基/用户坐标)，<br> 6=轴速度， 7=电机速度<br>
		 10=负载因子(I/Ir)， 11=负载因子(I/Ip)， 13=负载因子（连续），<br> 15=编码器温度<br>
		 18=每个轴的累计距离)</td>
		<td></td>
	</tr>
	<tr>
		<td>SF160</td>
		<td>轴 1 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF164</td>
		<td>轴 2 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF168</td>
		<td>轴 3 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF172</td>
		<td>轴 4 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF176</td>
		<td>轴 5 的相关值</td>
		<td></td>
```
```html
</tr>
	<tr>
		<td>SF180</td>
		<td>轴 6 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF184</td>
		<td>轴 7 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF188</td>
		<td>轴 8 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF192</td>
		<td>轴 9 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF196</td>
		<td>轴 10 的相关值</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
</tbody>
</table>
```
[__SOURCE](3-relay/4-sw-relay/2-slot-task-info.md)
# 3.4.2 S 继电器 - 任务信息

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_TASK_INFO (100)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>任务处于激活状态</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>任务程序编号</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>任务步骤编号</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>任务功能编号</td>
<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>任务主程序编号</td>
		<td>s2</td>
	</tr>	
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/3-slot-op-time.md)
# 3.4.3 S 继电器 - 操作时间

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移量</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_OP_TIME (110)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>时间基准<br>1=自初始化以来, 2=自通电以来, 3=自上一个周期以来, 4=当前周期</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>参数 3</td>
		<td>项目<br>1=电机开启, 2=运行时间, 3=移动时间, 4=等待时间, 5=延迟时间, 11=点焊时间 (焊接机 1), 12=(焊接机 2), 13=(焊接机 3), 14=(焊接机 4)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>结果</td>
		<td>天数</td>
		<td>s4</td>
	</tr>
	<tr>
<td>12</td>
<td>毫秒</td>
<td>s4</td>
</tr>
<tr>
<td>16</td>
<td>循环计数 / 焊接计数</td>
<td>s4</td>
</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/4-slot-axis-info.md)
# 3.4.4 S 继电器 - AXIS_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_AXIS_INFO (120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>类型<br>1 = 当前坐标（轴角度），2 = 当前坐标（基坐标），3 = 当前坐标（基/用户坐标），<br> 6 = 轴速度,
7 = 电机速度，8 = 速度控制时的电机速度命令（rpm）<br> 10 = 负载系数 (I/Ir)，11 = 负载系数 (I/Ip)，12 = 负载系数（持续），<br>
15 = 编码器（温度），<br> 18 = 每个轴的累计距离</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>起始轴编号（1-）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>-</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>结果</td>
		<td>相关值（对于起始轴 + 轴 0）</td>
		<td>f4</td>
</tr>
	<tr>
		<td>12</td>
		<td>相关值（用于起始轴 + 轴 1）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>相关值（用于起始轴 + 轴 2）</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
<br>
<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>SET_AXIS_INFO (121)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>类型<br>8 = 当速度控制时的电机速度命令（rpm）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>起始轴号（1-）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>-</td>
<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>结果</td>
		<td>相关值（对于起始轴 + 轴 0）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>相关值（对于起始轴 + 轴 1）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>相关值（对于起始轴 + 轴 2）</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/5-slot-tp-keypad.md)
# 3.4.5 S relay - TP_KEYPAD

支持从 V60.30-07

<style type="text/css">
	table  {border-collapse:collapse;}
	th, td {
		border: 1px solid black;
		text-align: center;
		width: 9%;
		height: 3rem;
	}
	.grayed {
		background-color: lightgray;
	}
	.jog {
		color: black;
		background-color: rgb(255, 240, 200);
	}
	.fkey {
		color: black;
		background-color: rgb(210, 230, 200);
	}
	.opkey {
		color: black;
		background-color: rgb(240, 240, 150);
	}
	.spkey {
		color: black;
		background-color: rgb(250, 180, 170);
	}
	.num {
		color: black;
		background-color: rgb(240, 240, 240);
	}
	.arrow {
		color: black;
		background-color: lightgreen;
	}
	.ent {
		color: black;
		background-color: rgb(185, 250, 255);
	}
</style>

<table class="tg">
<thead>
	<tr>
		<th>SB offset</th>
		<th>byte\bit</th>
```html
<th>7</th>
<th>6</th>
<th>5</th>
<th>4</th>
<th>3</th>
<th>2</th>
<th>1</th>
<th>0</th>
<th>类型</th>
</tr>
</thead>

<tbody>
<tr>
<td>0</td>
<td>命令</td>
<td colspan='8'>GET_TP_KEYPAD (130)</td>
<td>s2</td>
</tr>
<tr>
<td>2</td>
<td>-</td>
<td colspan='8'></td>
<td></td>
</tr>
<tr>
<td>3</td>
<td>[0]</td>
<td class='jog'>J4-</td>
<td class='jog'>J5-</td>
<td class='jog'>J1-</td>
<td class='jog'>J2-</td>
<td class='jog'>J3-</td>
<td class='jog'>J1+</td>
<td class='jog'>J2+</td>
<td class='jog'>J3+</td>
<td>u1</td>
</tr>
<tr>
<td>4</td>
<td>[1]</td>
<td class='ent'>SHIFT</td>
<td class='arrow'>&larr;</td>
<td class='jog'>J6-</td>
<td class='jog'>J4+</td>
<td class='jog'>J5+</td>
<td class='jog'>J6+</td>
<td class='jog'>步骤<br>前进</td>
<td class='jog'>步骤<br>后退</td>
<td>u1</td>
```
```
	</tr>
	<tr>
		<td>5</td>
		<td>[2]</td>
		<td>设置</td>
		<td></td>
		<td>机器人<br>移动</td>
		<td></td>
		<td></td>
		<td>SHIFT+1</td>
		<td>SHIFT+3</td>
		<td>SHIFT+2</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>[3]</td>
		<td class='fkey'>F7</td>
		<td class='fkey'>F6</td>
		<td class='fkey'>F5</td>
		<td class='fkey'>F4</td>
		<td class='fkey'>F3</td>
		<td class='fkey'>F2</td>
		<td class='fkey'>F1</td>
		<td></td>
		<td>u1</td>
	</tr>
	<tr>
		<td>7</td>
		<td>[4]</td>
		<td>退格</td>
		<td>虚拟<br>TP</td>
		<td class='ent'>CTRL</td>
		<td class='opkey'>模式2</td>
		<td class='opkey'>模式1</td>
		<td class='opkey'>停止</td>
		<td class='opkey'>开始</td>
		<td class='opkey'>电机<br>开启</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>[5]</td>
		<td class='num'>7</td>
		<td class='num'>6</td>
		<td class='num'>5</td>
		<td class='num'>4</td>
		<td class='num'>3</td>
		<td class='num'>2</td>
		<td class='num'>1</td>
```
<td class='num'>0</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>[6]</td>
		<td class='arrow'>&darr;</td>
		<td class='arrow'>&uarr;</td>
		<td class='arrow'>&rarr;</td>
		<td class='ent'>R</td>
		<td class='ent'>进入</td>
		<td class='ent'>退出</td>
		<td class='num'>9</td>
		<td class='num'>8</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>[7]</td>
		<td class='spkey'>速度<br>.低</td>
		<td class='spkey'>速度<br>.高</td>
		<td class='spkey'>录制</td>
		<td class='spkey'>步进</td>
		<td class='spkey'>机械</td>
		<td class='spkey'>枪</td>
		<td class='spkey'>坐标</td>
		<td></td>
		<td>u1</td>
	</tr>
	<tr>
		<td>11</td>
		<td>[8]</td>
		<td class='spkey'>历史</td>
		<td class='num'>.</td>
		<td></td>
		<td>对齐<br>移动</td>
		<td class='jog'>J8+</td>
		<td class='jog'>J8-</td>
		<td class='jog'>J7+</td>
		<td class='jog'>J7-</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>12</td>
		<td>[9]</td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
<td></td>
		<td></td>
		<td></td>
		<td>u1</td>
	</tr>
	<tr>
		<td>13</td>
		<td>[10]</td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td>u1</td>
	</tr>
	<tr>
		<td>14</td>
		<td>[11]</td>
		<td colspan='8'>序列号</td>
		<td>u1</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/6-slot-tp-app.md)
# 3.4.6 S 继电器 - TP_APP

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GETSET_TP_APP (140)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>获取</td>
		<td>教导挂件当前应用的快捷键编号 (1-9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>设置</td>
		<td>教导挂件目标应用的快捷键编号，状态需要被读取或控制 (1-9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>获取</td>
		<td>教导挂件目标应用的当前状态值<br>(-1=无操作, 0=未执行, 1=已激活, 2=未激活)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>设置</td>
		<td>控制教导挂件的目标应用<br>
(0: 无操作, 1: 已激活, 2: 未激活, 8: 已执行, 9: 强制结束)<br>
* 每当值变化时将执行一次。</td>
		<td>s2</td>
</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/7-slot-date-time.md)
# 3.4.7 S 继电器 - 日期时间

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_DATE_TIME (150)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td rowspan=6>结果</td>
		<td>年份（例如，2022）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>月份（1-12）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>日期（1-31）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>小时（0-23）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>分钟（0-59）</td>
		<td>s2</td>
</tr>
	<tr>
		<td>12</td>
		<td>秒 (0-59)</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/8-slot-cur-spotgun-no.md)
# 3.4.8 S 继电器 - CUR_SPOTGUN_NO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_CUR_SPOTGUN_NO (2000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>task_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=12>结果</td>
		<td>当前点焊枪编号 (主枪)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>当前条件编号 (主 cnd)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>7</td>
		<td>当前序列编号 (主 seq)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>当前点焊枪编号 (从枪 #1)</td>
<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>当前条件编号 (从设备 cnd #1)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>11</td>
		<td>当前序列编号 (从设备 seq #1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>12</td>
		<td>当前点焊枪编号 (从设备 gun #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>13</td>
		<td>当前条件编号 (从设备 cnd #2)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>15</td>
		<td>当前序列编号 (从设备 seq #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>16</td>
		<td>当前点焊枪编号 (从设备 gun #3)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>17</td>
		<td>当前条件编号 (从设备 cnd #3)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>19</td>
		<td>当前序列编号 (从设备 seq #3)</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/9-slot-spotweld-info.md)
# 3.4.9 S realy - SPOTWELD_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_SPOTWELD_INFO (2010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>枪编号 (1-4)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td rowspan=5>结果</td>
		<td>枪搜索状态 (1=完成, 0=未完成)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>移动电极消耗量 x 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
<<<SOURCE_MARKDOWN_START>>>		<td>固定电极消耗量 x 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>挤压力指令值 x 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>挤压力电流值 x 10</td>
		<td>s2</td>
	</tr>
</tbody>
</table><<<SOURCE_MARKDOWN_END>>>
[__SOURCE](3-relay/4-sw-relay/10-slot-arcweld-info.md)
# 3.4.10 S realy - ARCWELD_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3000) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>焊接电流</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊接电压</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
<<<SOURCE_MARKDOWN_START>>>
		<td>焊机错误</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>送线速度</td>
		<td>f4</td>
	</tr>
</tbody>
</table>



<br>
以下服务从 V60.32-00 开始支持。
<br>
<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3001) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>送线电机电流</td>
		<td>f4</td><<<<SOURCE_MARKDOWN_END>>>
</tr>
	<tr>
		<td>8</td>
		<td>缝合跟踪数据</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>焊接过程</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td></td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3002) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊工编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双工编号 (0~1)</td>
		<td>s1</td>
	</tr>
<td>4</td>
		<td rowspan=5>结果</td>
		<td>焊接机总操作时间（秒）</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊接机固件版本 - 低位（Vx.x.255）</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>焊接机固件版本 - 中位（Vx.255.x）</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>焊接机固件版本 - 高位（V255.x.x）</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S 偏移量</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3004) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>
			0x01 = WCR(接触继电器) <br>
			0x02 = 火炬碰撞 <br>
			0x04 = 电源正常 <br>
			0x08 = 电线卡住 <br>
			0x10 = 焊机错误 <br>
			0x20 = 过程激活 <br>
			0x40 = 通信准备 <br>
			0x80 = 电线使用可能 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 火炬状态 <br>
			0x02 = 微步状态 <br>
			0x04 = 回缩状态 <br>
			0x08 = 气体检查 <br>
			0x10 = 协同可用 <br>
			0x20 = 限制状态 <br>
			0x40 = 设置超出范围 <br>
		</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3005) - 输出</td>
<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双胞胎编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>焊机电流</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊机电压</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>作业/程序编号</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>操作模式</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>协同代码</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
```html
<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3006) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>脉冲动态修正</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊丝回缩</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>过程控制</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>弧力</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
```
```html
<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3007) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>电线材料</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>电线直径</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>气体类型</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>7</td>
		<td>焊接模式</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>8</td>
```
```html
<td>双工模式</td>
<td>s1</td>
</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3009) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双工编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>
			0x01 = 弧开启 <br>
			0x02 = 机器人就绪 <br>
			0x04 = 主焊炬选择 <br>
			0x08 = 气体开启 <br>
			0x10 = 焊丝进给 <br>
			0x20 = 焊丝回缩 <br>
			0x40 = 焊机错误重置 <br>
			0x80 = 焊丝粘连检查 <br>
		</td>
		<td>s1</td>
```
</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 焊接模拟 <br>
			0x02 = 引弧 <br>
			0x04 = 提升弧使用 <br>
			0x08 = 超脉冲使用 <br>
			0x10 = 在线状态 <br>
			0x20 = 工作模式激活 <br>
			0x40 = 电压设定模式 <br>
			0x80 = 电流设定模式 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>
			0x01 = 机器人焊枪碰撞 <br>
			0x02 = 机器人错误状态 <br>
		</td>
		<td>s1</td>
	</tr>	
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3010) - 状态</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>当前弧控制状态编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>当前触摸传感状态编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>当前编织状态编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>当前lvs状态编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>当前弧控制状态编号。</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/11-slot-conveyor-info.md)
# 3.4.10 S 继电器 - CONVEYOR_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_CONVEYOR_INFO (4000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>conv_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=7>结果</td>
		<td>输送机脉冲</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>工件位置</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>输送机速度</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>工件数量</td>
```html
<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>限位开关输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>原始脉冲</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>编码器分辨率</td>
		<td>s4</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_CONVEYOR_INFO_LIN (4010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>conv_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>结果</td>
		<td>线性输送机水平角度</td>
		<td>f4</td>
```
</tr>
	<tr>
		<td>8</td>
		<td>线性输送机垂直角度</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_CONVEYOR_INFO_CIR (4020)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>conv_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>结果</td>
		<td>圆形输送机角度 (X 轴)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>圆形输送机角度 (Y 轴)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_CONVEYOR_INFO_CIR2 (4040)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=3>结果</td>
		<td>圆形输送机中心 (X)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>圆形输送机中心 (Y)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>圆形输送机中心 (Z)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/12-slot-sys-var.md)
# 3.4.12 S realy - SYSTEM_VARIABLE

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>


### 系统变量设置

{% hint style="info" %}
要设置系统变量，请检查命令是否已更改并进行操作。 <br>
换句话说，它在命令值变化为161的瞬间操作一次。  

{% endhint %}

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>SET_SYS_VAR (161)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>项（已设置的数据）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4 ~ 18</td>
		<td>参数 n</td>
		<td>值</td>
		<td></td>
	</tr>
</tbody>
</table>

<br>
ex 1) 播放速度设置
<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>42 = 播放速度</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 1</td>
		<td>值</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

![](../../_assets/playback_speed.png)

<br>
<br>
ex 2) 工具号码更改
<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>40 = 工具号码</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 1</td>
		<td>值</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

![](../../_assets/tool_change.png)
[__SOURCE](3-relay/4-sw-relay/13-slot-hw-info.md)
# 3.4.13 S realy - HW_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_HW_INFO (170)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td rowspan=6>结果</td>
		<td>CPU 温度 * 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>主板温度 * 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>系统板温度 * 10</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/README.md)
# 3.4.14 S 继电器 - CIFX PCI 通信

#### CIFX PCI 通信通用继电器
* command 1000: 通用状态
* command 1001: 通用控制

<br>

#### CIFX PCI 通信协议继电器
* command 1010: Profibus-DP 主站
* command 1012: DeviceNet 主站
* command 1014: EtherNet/IP 主站
* command 1016: Profinet IO 主站
* command 1018: EtherCAT 主站
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/1-slot-common-info.md)
# 3.4.14.1 S 继电器 - CIFX PCI 通信状态

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<br>

### CIFX PCI 通用状态

<br>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 CIFX 状态 = 1000</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>状态 1 = 1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>4</td>
		<td>通道状态</td>
		<td class='grayed'></td>
		<td>需要重启启用</td>
		<td>需要重启</td>
		<td>配置新 </td>
		<td>配置锁定</td>
		<td>总线打开</td>
		<td>运行</td>
		<td>准备好</td>
	</tr>
	<tr>
		<td>8</td>
		<td>4</td>
		<td>通信状态</td>
		<td colspan=8>0 = 未知, <br> 1 = 未配置, <br> 2 = 停止, <br> 3 = 空闲, <br> 4 = 操作</td>
	</tr>
	<tr>
		<td>12</td>
		<td>4</td>
		<td>通信错误代码</td>
		<td colspan=8>0 = 无错误, <br> 非零 = 错误代码 (32位十六进制)</td>
	</tr>
	<tr>
		<td>16</td>
		<td>2</td>
		<td>诊断结构版本</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>18</td>
		<td>2</td>
		<td>看门狗超时 (毫秒)</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>


<br>
<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>获取 CIFX 状态 = 1000</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>状态 2 = 2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>1</td>
		<td>输入数据握手模式</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>5</td>
```html
<td>-</td>
<td></td>
<td colspan=8></td>
</tr>
<tr>
<td>6</td>
<td>1</td>
<td>输出数据握手模式</td>
<td colspan=8></td>
</tr>
<tr>
<td>7</td>
<td>-</td>
<td></td>
<td colspan=8></td>
</tr>
<tr>
<td>8</td>
<td>4</td>
<td>主机系统看门狗</td>
<td colspan=8></td>
</tr>
<tr>
<td>12</td>
<td>4</td>
<td>通信错误计数</td>
<td colspan=8></td>
</tr>
<tr>
<td>16</td>
<td>-</td>
<td></td>
<td colspan=8></td>
</tr>
<tr>
<td>17</td>
<td>1</td>
<td>输入数据握手错误</td>
<td colspan=8></td>
</tr>
<tr>
<td>18</td>
<td>1</td>
<td>输出数据握手错误</td>
<td colspan=8></td>
</tr>
<tr>
<td>19</td>
<td>-</td>
<td></td>
```
<td colspan=8></td>
	</tr>
</tbody>
</table>


<br>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 CIFX 状态 = 1000</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>状态 3 = 3</td>
	</tr>
<tr>
		<td>4</td>
		<td>16</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>

<br>

### 仅限 CIFX PCI 主控

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 CIFX 状态 = 1000</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>状态 4 = 4</td>
	</tr>
	<tr>
		<td>4</td>
		<td>4</td>
		<td>从设备状态</td>
		<td colspan=8>0 = 未知, <br> 1 = 正常, <br> 2 = 失败</td>
	</tr>
	<tr>
		<td>8</td>
		<td>4</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>12</td>
		<td>4</td>
		<td>配置从设备的数量</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>16</td>
		<td>4</td>
		<td>活动从设备的数量</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
<td class='powderblued'>位 6</td>
<td class='powderblued'>位 5</td>
<td class='powderblued'>位 4</td>
<td class='powderblued'>位 3</td>
<td class='powderblued'>位 2</td>
<td class='powderblued'>位 1</td>
<td class='powderblued'>位 0</td>
</tr>
<tr>
<td>0</td>
<td>2</td>
<td>命令</td>
<td colspan=8>获取 CIFX 状态 = 1000</td>
</tr>
<tr>
<td>2</td>
<td>1</td>
<td>参数 1</td>
<td colspan=8>插槽编号 = 1 ~ 3</td>
</tr>
<tr>
<td>3</td>
<td>1</td>
<td>参数 2</td>
<td colspan=8>状态 5 = 5</td>
</tr>
<tr>
<td>4</td>
<td>4</td>
<td>诊断从设备数量</td>
<td colspan=8></td>
</tr>
<tr>
<td>8</td>
<td>12</td>
<td>保留</td>
<td colspan=8></td>
</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/2-slot-common-control.md)
# 3.4.14.2 S 继电器 - CIFX PCI 通信控制

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<br>

#### 支持的版本: TBD 

<br>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 CIFX 控制 = 1001</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽号 = 1 ~ 3</td>
```
</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>控制组 = 1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>1</td>
		<td>通信重置</td>
		<td colspan=8>当信号变化 0 -> 1 时重置</td>
	</tr>
	<tr>
		<td>5</td>
		<td>1</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>6</td>
		<td>1</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>7</td>
		<td>1</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>8</td>
		<td>2</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>10</td>
		<td>2</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>12</td>
		<td>8</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
```
<table>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/3-slot-profibus-dp-info.md)
# 3.4.14.3 S 继电器 - Profibus-DP 主状态

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移量</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>起始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 Profibus-DP 状态 = 1010</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
```html
<td>参数 2</td>
<td colspan=8>状态 = 1</td>
</tr>
<tr>
	<td>4</td>
	<td>1</td>
	<td>全局位 <br> (Profibus 主设备)</td>
	<td class='grayed'></td>
	<td class='grayed'></td>
	<td>超时</td>
	<td>主机未准备好</td>
	<td>致命错误</td>
	<td>非交换错误</td>
	<td>自动清除错误</td>
	<td>控制错误</td>
</tr>
<tr>
	<td>5</td>
	<td>1</td>
	<td>主设备状态</td>
	<td colspan=8>0x00 = 离线, <br> 0x40 = 停止, <br> 0x80 = 清除, <br> 0xC0 = 操作</td>
</tr>
<tr>
	<td>6</td>
	<td>1</td>
	<td>保留</td>
	<td colspan=8></td>
</tr>
<tr>
	<td>7</td>
	<td>1</td>
	<td>保留</td>
	<td colspan=8></td>
</tr>
<tr>
	<td>8</td>
	<td>2</td>
	<td>保留</td>
	<td colspan=8></td>
</tr>
<tr>
	<td>10</td>
	<td>2</td>
	<td>保留</td>
	<td colspan=8></td>
</tr>
<tr>
	<td>12</td>
	<td>8</td>
	<td>保留</td>
```
<td colspan=8></td>
	</tr>
</tbody>
</table>

	
<br>

{% hint style="info" %}
\.		如果您想监控从设备是否处于活动状态，请检查“IO交换中的从设备列表”。
{% endhint %}

<br>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 Profibus-DP 状态 = 1010</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>配置的从设备列表 = 2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
<td>节点 24</td>
	</tr>
	<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
	<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
	<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
	<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
```html
<td>节点 69</td>
<td>节点 68</td>
<td>节点 67</td>
<td>节点 66</td>
<td>节点 65</td>
<td>节点 64</td>
</tr>
<tr>
<td>13</td>
<td>节点 79</td>
<td>节点 78</td>
<td>节点 77</td>
<td>节点 76</td>
<td>节点 75</td>
<td>节点 74</td>
<td>节点 73</td>
<td>节点 72</td>
</tr>
<tr>
<td>14</td>
<td>节点 87</td>
<td>节点 86</td>
<td>节点 85</td>
<td>节点 84</td>
<td>节点 83</td>
<td>节点 82</td>
<td>节点 81</td>
<td>节点 80</td>
</tr>
<tr>
<td>15</td>
<td>节点 95</td>
<td>节点 94</td>
<td>节点 93</td>
<td>节点 92</td>
<td>节点 91</td>
<td>节点 90</td>
<td>节点 89</td>
<td>节点 88</td>
</tr>
<tr>
<td>16</td>
<td>节点 103</td>
<td>节点 102</td>
<td>节点 101</td>
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
```
</tr>
	<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
	<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
		<td>节点 113</td>
		<td>节点 112</td>
	</tr>
	<tr>
		<td>19</td>
		<td>节点 127</td>
		<td>节点 126</td>
		<td>节点 125</td>
		<td>节点 124</td>
		<td>节点 123</td>
		<td>节点 122</td>
		<td>节点 121</td>
		<td>节点 120</td>
	</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移量</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody
<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>获取 Profibus-DP 状态 = 1010</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>IO 交换中的从设备列表 = 3</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
	<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
	<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
	<tr>
```
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
	<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
	<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
	<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
```
<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
	<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
	<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
		<td>节点 100</td>
		<td>节点 99</td>
		<td>节点 98</td>
		<td>节点 97</td>
		<td>节点 96</td>
	</tr>
	<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
	<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
		<td>节点 113</td>
		<td>节点 112</td>
	</tr>
	<tr>
		<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
    <tr>
        <th colspan=2>S 偏移</th>
        <th>名称</th>
        <th colspan=8>描述或位索引</th>
    </tr>
</thead>

<tbody>
    <tr>
        <td class='powderblued'>开始</td>
        <td class='powderblued'>大小</td>
        <td class='powderblued'>继电器</td>
        <td class='powderblued'>位 7</td>
        <td class='powderblued'>位 6</td>
        <td class='powderblued'>位 5</td>
        <td class='powderblued'>位 4</td>
        <td class='powderblued'>位 3</td>
        <td class='powderblued'>位 2</td>
        <td class='powderblued'>位 1</td>
        <td class='powderblued'>位 0</td>
    </tr>
    <tr>
        <td>0</td>
        <td>2</td>
        <td>命令</td>
        <td colspan=8>获取 Profibus-DP 状态 = 1010</td>
    </tr>
    <tr>
        <td>2</td>
        <td>1</td>
        <td>参数 1</td>
        <td colspan=8>插槽编号 = 1 ~ 3</td>
    </tr>
```html
<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>诊断从设备列表 = 4</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
```
<td>节点 24</td>
	</tr>
	<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
	<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
	<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
	<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td><
<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
	<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
	<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
	<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
	<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
		<td>节点 100</td>
		<td>节点 99</td>
		<td>节点 98</td>
		<td>节点 97</td>
		<td>节点 96</td>
</tr>
	<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
	<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
		<td>节点 113</td>
		<td>节点 112</td>
	</tr>
	<tr>
		<td>19</td>
		<td>节点 127</td>
		<td>节点 126</td>
		<td>节点 125</td>
		<td>节点 124</td>
		<td>节点 123</td>
		<td>节点 122</td>
		<td>节点 121</td>
		<td>节点 120</td>
	</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody
<<<SOURCE_MARKDOWN_START>>>	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>获取 Profibus-DP 状态 = 1010</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>配置的从站列表 = 5</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从站列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td><<<SOURCE_MARKDOWN_END>>>
```html
<td>节点 11</td>
<td>节点 10</td>
<td>节点 9</td>
<td>节点 8</td>
</tr>
<tr>
<td>6</td>
<td>节点 23</td>
<td>节点 22</td>
<td>节点 21</td>
<td>节点 20</td>
<td>节点 19</td>
<td>节点 18</td>
<td>节点 17</td>
<td>节点 16</td>
</tr>
<tr>
<td>7</td>
<td>节点 31</td>
<td>节点 30</td>
<td>节点 29</td>
<td>节点 28</td>
<td>节点 27</td>
<td>节点 26</td>
<td>节点 25</td>
<td>节点 24</td>
</tr>
<tr>
<td>8</td>
<td>节点 39</td>
<td>节点 38</td>
<td>节点 37</td>
<td>节点 36</td>
<td>节点 35</td>
<td>节点 34</td>
<td>节点 33</td>
<td>节点 32</td>
</tr>
<tr>
<td>9</td>
<td>节点 47</td>
<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
```
```html
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
<tr>
<td>12</td>
<td>节点 71</td>
<td>节点 70</td>
<td>节点 69</td>
<td>节点 68</td>
<td>节点 67</td>
<td>节点 66</td>
<td>节点 65</td>
<td>节点 64</td>
</tr>
<tr>
<td>13</td>
<td>节点 79</td>
<td>节点 78</td>
<td>节点 77</td>
<td>节点 76</td>
<td>节点 75</td>
<td>节点 74</td>
<td>节点 73</td>
<td>节点 72</td>
</tr>
<tr>
<td>14</td>
<td>节点 87</td>
<td>节点 86</td>
<td>节点 85</td>
<td>节点 84</td>
<td>节点 83</td>
```
<td>节点 82</td>
<td>节点 81</td>
<td>节点 80</td>
</tr>
<tr>
<td>15</td>
<td>节点 95</td>
<td>节点 94</td>
<td>节点 93</td>
<td>节点 92</td>
<td>节点 91</td>
<td>节点 90</td>
<td>节点 89</td>
<td>节点 88</td>
</tr>
<tr>
<td>16</td>
<td>节点 103</td>
<td>节点 102</td>
<td>节点 101</td>
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
</tr>
<tr>
<td>17</td>
<td>节点 111</td>
<td>节点 110</td>
<td>节点 109</td>
<td>节点 108</td>
<td>节点 107</td>
<td>节点 106</td>
<td>节点 105</td>
<td>节点 104</td>
</tr>
<tr>
<td>18</td>
<td>节点 119</td>
<td>节点 118</td>
<td>节点 117</td>
<td>节点 116</td>
<td>节点 115</td>
<td>节点 114</td>
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 Profibus-DP 状态 = 1010</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>IO交换中的从设备列表 = 6</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
```html
<td>节点 24</td>
</tr>
<tr>
	<td>8</td>
	<td>节点 39</td>
	<td>节点 38</td>
	<td>节点 37</td>
	<td>节点 36</td>
	<td>节点 35</td>
	<td>节点 34</td>
	<td>节点 33</td>
	<td>节点 32</td>
</tr>
<tr>
	<td>9</td>
	<td>节点 47</td>
	<td>节点 46</td>
	<td>节点 45</td>
	<td>节点 44</td>
	<td>节点 43</td>
	<td>节点 42</td>
	<td>节点 41</td>
	<td>节点 40</td>
</tr>
<tr>
	<td>10</td>
	<td>节点 55</td>
	<td>节点 54</td>
	<td>节点 53</td>
	<td>节点 52</td>
	<td>节点 51</td>
	<td>节点 50</td>
	<td>节点 49</td>
	<td>节点 48</td>
</tr>
<tr>
	<td>11</td>
	<td>节点 63</td>
	<td>节点 62</td>
	<td>节点 61</td>
	<td>节点 60</td>
	<td>节点 59</td>
	<td>节点 58</td>
	<td>节点 57</td>
	<td>节点 56</td>
</tr>
<tr>
	<td>12</td>
	<td>节点 71</td>
	<td>节点 70</td>
```
```html
<td>节点 69</td>
<td>节点 68</td>
<td>节点 67</td>
<td>节点 66</td>
<td>节点 65</td>
<td>节点 64</td>
</tr>
<tr>
<td>13</td>
<td>节点 79</td>
<td>节点 78</td>
<td>节点 77</td>
<td>节点 76</td>
<td>节点 75</td>
<td>节点 74</td>
<td>节点 73</td>
<td>节点 72</td>
</tr>
<tr>
<td>14</td>
<td>节点 87</td>
<td>节点 86</td>
<td>节点 85</td>
<td>节点 84</td>
<td>节点 83</td>
<td>节点 82</td>
<td>节点 81</td>
<td>节点 80</td>
</tr>
<tr>
<td>15</td>
<td>节点 95</td>
<td>节点 94</td>
<td>节点 93</td>
<td>节点 92</td>
<td>节点 91</td>
<td>节点 90</td>
<td>节点 89</td>
<td>节点 88</td>
</tr>
<tr>
<td>16</td>
<td>节点 103</td>
<td>节点 102</td>
<td>节点 101</td>
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
```
```html
</tr>
	<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
	<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
		<td>节点 113</td>
		<td>节点 112</td>
	</tr>
	<tr>
		<td>19</td>
		<td>节点 127</td>
		<td>节点 126</td>
		<td>节点 125</td>
		<td>节点 124</td>
		<td>节点 123</td>
		<td>节点 122</td>
		<td>节点 121</td>
		<td>节点 120</td>
	</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>
```
<<<SOURCE_MARKDOWN_START>>>	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>获取 Profibus-DP 状态 = 1010</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>槽位号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>诊断从设备列表 = 7</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td><<<SOURCE_MARKDOWN_END>>>
<td>节点 11</td>
<td>节点 10</td>
<td>节点 9</td>
<td>节点 8</td>
</tr>
<tr>
<td>6</td>
<td>节点 23</td>
<td>节点 22</td>
<td>节点 21</td>
<td>节点 20</td>
<td>节点 19</td>
<td>节点 18</td>
<td>节点 17</td>
<td>节点 16</td>
</tr>
<tr>
<td>7</td>
<td>节点 31</td>
<td>节点 30</td>
<td>节点 29</td>
<td>节点 28</td>
<td>节点 27</td>
<td>节点 26</td>
<td>节点 25</td>
<td>节点 24</td>
</tr>
<tr>
<td>8</td>
<td>节点 39</td>
<td>节点 38</td>
<td>节点 37</td>
<td>节点 36</td>
<td>节点 35</td>
<td>节点 34</td>
<td>节点 33</td>
<td>节点 32</td>
</tr>
<tr>
<td>9</td>
<td>节点 47</td>
<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
```
<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
	<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
	<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
	<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
```
```html
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
	<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
	<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
		<td>节点 100</td>
		<td>节点 99</td>
		<td>节点 98</td>
		<td>节点 97</td>
		<td>节点 96</td>
	</tr>
	<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
	<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
		<td>节点 113</td>
		<td>节点 112</td>
	</tr>
	<tr>
		<td>19</td>
```
```html
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 Profibus-DP 状态 = 1010</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
```
<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>输入更新中的从设备列表 = 8</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
<td>节点 24</td>
	</tr>
	<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
	<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
	<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
	<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
```html
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
	<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
	<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
	<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
	<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
		<td>节点 100</td>
		<td>节点 99</td>
		<td>节点 98</td>
		<td>节点 97</td>
		<td>节点 96</td>
```
</tr>
	<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
	<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
		<td>节点 113</td>
		<td>节点 112</td>
	</tr>
	<tr>
		<td>19</td>
		<td>节点 127</td>
		<td>节点 126</td>
		<td>节点 125</td>
		<td>节点 124</td>
		<td>节点 123</td>
		<td>节点 122</td>
		<td>节点 121</td>
		<td>节点 120</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/4-slot-devicenet-info.md)
# 3.4.14.4 S 继电器 - DeviceNet 主状态

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
<td>参数. 2</td>
<td colspan=8>状态  = 1</td>
</tr>
<tr>
<td>4</td>
<td>1</td>
<td>全球位 <br> (Profibus 主控)</td>
<td>检查重复的 MAC ID</td>
<td>重复的 MAC ID</td>
<td>主机未准备好</td>
<td>总线事件错误</td>
<td>致命错误</td>
<td>非交换错误</td>
<td>自动清除错误</td>
<td>控制错误</td>
</tr>
<tr>
<td>5</td>
<td>1</td>
<td>主控状态</td>
<td colspan=8>0x00 = 离线, <br> 0x40 = 停止, <br> 0x80 = 空闲, <br> 0xC0 = 运行</td>
</tr>
<tr>
<td>6</td>
<td>1</td>
<td>错误站地址</td>
<td colspan=8></td>
</tr>
<tr>
<td>7</td>
<td>1</td>
<td>错误代码</td>
<td colspan=8>DeviceNet 主控仅 <br> 52 = 未知过程数据握手模式, <br> 53 = 波特率错误, <br> 54 = MAC ID 错误, <br> 57 = 重复的 MAC ID, <br> 58 = 无设备, <br> 210 = 无配置, <br> 212 = 读取配置失败, <br> 220 = 用户看门狗失败, <br> 221 = 用户数据无响应, <br> 223 = 主控停止 (CAN 总线关闭), <br> 226 = 设备不是主控</td>
</tr>
<tr>
<td>8</td>
<td>2</td>
<td>总线数据事务错误计数</td>
<td colspan=8></td>
</tr>
<tr>
<td>10</td>
<td>2</td>
<td>总线关闭错误计数</td>
<td colspan=8></td>
</tr>
<tr>
<td>12</td>
<td>4</td>
<td>总线错误代码</td>
<td colspan=8></td>
	</tr>
	<tr>
		<td>16</td>
		<td>4</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>

	
<br>

{% hint style="info" %}
\.		如果您想监视从设备是否处于活动状态，请检查“IO交换中的从设备列表”。
{% endhint %}

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取设备网络状态 = 1012</td>
	</tr>
<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>已激活 / 未激活从站列表 = 2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>已激活从站列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
```html
<td>节点 30</td>
<td>节点 29</td>
<td>节点 28</td>
<td>节点 27</td>
<td>节点 26</td>
<td>节点 25</td>
<td>节点 24</td>
</tr>
<tr>
<td>8</td>
<td>节点 39</td>
<td>节点 38</td>
<td>节点 37</td>
<td>节点 36</td>
<td>节点 35</td>
<td>节点 34</td>
<td>节点 33</td>
<td>节点 32</td>
</tr>
<tr>
<td>9</td>
<td>节点 47</td>
<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
```
<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td rowspan=8>8</td>
		<td rowspan=8>停用从属设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>13</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>14</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>15</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
	<tr>
		<td>16</td>
<td>节点 39</td>
<td>节点 38</td>
<td>节点 37</td>
<td>节点 36</td>
<td>节点 35</td>
<td>节点 34</td>
<td>节点 33</td>
<td>节点 32</td>
</tr>
<tr>
<td>17</td>
<td>节点 47</td>
<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>18</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>19</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
```html
<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
		<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>从设备列表（显式消息 / IO 交换） = 3</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>激活显式消息的从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
```
<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
	<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
	<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
<tr>
<td>12</td>
<td rowspan=8>8</td>
<td rowspan=8>IO 交换中的从属设备列表</td>
<td>节点 7</td>
<td>节点 6</td>
<td>节点 5</td>
<td>节点 4</td>
<td>节点 3</td>
<td>节点 2</td>
<td>节点 1</td>
<td>节点 0</td>
</tr>
<tr>
<td>13</td>
<td>节点 15</td>
<td>节点 14</td>
<td>节点 13</td>
<td>节点 12</td>
<td>节点 11</td>
<td>节点 10</td>
<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>14</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>15</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
	<tr>
		<td>16</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
	<tr>
		<td>17</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
	<tr>
		<td>18</td>
		<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>19</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移</th>
<th>名称</th>
<th colspan=8>描述或位索引</th>
</tr>
</thead>

<tbody>
<tr>
<td class='powderblued'>开始</td>
<td class='powderblued'>大小</td>
<td class='powderblued'>继电器</td>
<td class='powderblued'>位 7</td>
<td class='powderblued'>位 6</td>
<td class='powderblued'>位 5</td>
<td class='powderblued'>位 4</td>
<td class='powderblued'>位 3</td>
<td class='powderblued'>位 2</td>
<td class='powderblued'>位 1</td>
<td class='powderblued'>位 0</td>
</tr>
<tr>
<td>0</td>
<td>2</td>
		<td>命令</td>
		<td colspan=8>获取设备网络状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>诊断从站列表 = 4</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>从站列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
	<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
	<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
	<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
	<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
```html
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>8</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移量</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
```
```html
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>已配置从属设备列表 = 5</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
```
```html
<td>节点 27</td>
<td>节点 26</td>
<td>节点 25</td>
<td>节点 24</td>
</tr>
<tr>
<td>8</td>
<td>节点 39</td>
<td>节点 38</td>
<td>节点 37</td>
<td>节点 36</td>
<td>节点 35</td>
<td>节点 34</td>
<td>节点 33</td>
<td>节点 32</td>
</tr>
<tr>
<td>9</td>
<td>节点 47</td>
<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
```
```html
<td>12</td>
<td>8</td>
<td>保留</td>
<td colspan=8></td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移量</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
```
<td colspan=8>已激活从属设备列表 = 6</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>从属设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
	<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
	<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
	<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
	<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>8</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>
<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移量</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>中继</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>诊断列表 = 7</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>从设备列表</td>
		<td>节点 7</td>
<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
	<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
<td>节点 32</td>
	</tr>
	<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
	<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
	<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>8</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/5-slot-ethernet-ip-info.md)
# 3.4.14.5 S 继电器 - EtherNet/IP 主状态

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 EtherNet/IP 状态 = 1014</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
<td>参数 2</td>
<td colspan=8>状态 = 1</td>
</tr>
<tr>
<td>4</td>
<td>4</td>
<td>报警计数</td>
<td colspan=8></td>
</tr>
<tr>
<td>8</td>
<td>4</td>
<td>警告计数</td>
<td colspan=8></td>
</tr>
<tr>
<td>12</td>
<td>4</td>
<td>错误计数</td>
<td colspan=8></td>
</tr>
<tr>
<td>16</td>
<td>4</td>
<td>错误级别</td>
<td colspan=8>报警，警告，错误</td>
</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移</th>
<th>名称</th>
<th colspan=8>描述或位索引</th>
</tr>
</thead>

<tbody>
<tr>
<td class='powderblued'>开始</td>
<td class='powderblued'>大小</td>
<td class='powderblued'>继电器</td>
<td class='powderblued'>位 7</td>
<td class='powderblued'>位 6</td>
<td class='powderblued'>位 5</td>
<table>
	<tr>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 EtherNet/IP 状态 = 1014</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>状态 = 2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>4</td>
		<td>错误代码</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>8</td>
		<td>4</td>
		<td>错误代码的参数</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>12</td>
		<td>4</td>
		<td>错误发生源行</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>16</td>
		<td>4</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>
<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 EtherNet/IP 状态 = 1014</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>状态 = 3</td>
	</tr>
	<tr>
		<td>4</td>
		<td>12</td>
		<td>错误发生源标识符</td>
		<td colspan=8></td>
</tr>
	<tr>
		<td>16</td>
		<td>4</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>


<br>

{% hint style="info" %}
\.		如果您想监控从站是否处于活动状态，请检查“IO交换中的从站列表”。
{% endhint %}

<br>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>获取 EtherNet/IP 状态 = 1014</td>
	</tr>
	<tr>
```html
<td>2</td>
<td>1</td>
<td>参数 1</td>
<td colspan=8>插槽编号 = 1 ~ 3</td>
</tr>
<tr>
<td>3</td>
<td>1</td>
<td>参数 2</td>
<td colspan=8>已配置从设备列表 = 5</td>
</tr>
<tr>
<td>4</td>
<td rowspan=16>16</td>
<td rowspan=16>从设备列表</td>
<td>节点 7</td>
<td>节点 6</td>
<td>节点 5</td>
<td>节点 4</td>
<td>节点 3</td>
<td>节点 2</td>
<td>节点 1</td>
<td>节点 0</td>
</tr>
<tr>
<td>5</td>
<td>节点 15</td>
<td>节点 14</td>
<td>节点 13</td>
<td>节点 12</td>
<td>节点 11</td>
<td>节点 10</td>
<td>节点 9</td>
<td>节点 8</td>
</tr>
<tr>
<td>6</td>
<td>节点 23</td>
<td>节点 22</td>
<td>节点 21</td>
<td>节点 20</td>
<td>节点 19</td>
<td>节点 18</td>
<td>节点 17</td>
<td>节点 16</td>
</tr>
<tr>
<td>7</td>
<td>节点 31</td>
<td>节点 30</td>
```
```html
<td>节点 29</td>
<td>节点 28</td>
<td>节点 27</td>
<td>节点 26</td>
<td>节点 25</td>
<td>节点 24</td>
</tr>
<tr>
<td>8</td>
<td>节点 39</td>
<td>节点 38</td>
<td>节点 37</td>
<td>节点 36</td>
<td>节点 35</td>
<td>节点 34</td>
<td>节点 33</td>
<td>节点 32</td>
</tr>
<tr>
<td>9</td>
<td>节点 47</td>
<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
```
</tr>
	<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
	<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
	<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
	<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
	<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
</tr>
<tr>
<td>17</td>
<td>节点 111</td>
<td>节点 110</td>
<td>节点 109</td>
<td>节点 108</td>
<td>节点 107</td>
<td>节点 106</td>
<td>节点 105</td>
<td>节点 104</td>
</tr>
<tr>
<td>18</td>
<td>节点 119</td>
<td>节点 118</td>
<td>节点 117</td>
<td>节点 116</td>
<td>节点 115</td>
<td>节点 114</td>
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移</th>
<th>名称</th>
<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 EtherNet/IP 状态 = 1014</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>IO 交换中的从设备列表 = 6</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
```html
<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
	<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
	<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
	<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
	<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
```
```html
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
	<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
	<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
	<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
	<tr>
		<td>14</td>
```
```html
<td>节点 87</td>
<td>节点 86</td>
<td>节点 85</td>
<td>节点 84</td>
<td>节点 83</td>
<td>节点 82</td>
<td>节点 81</td>
<td>节点 80</td>
</tr>
<tr>
<td>15</td>
<td>节点 95</td>
<td>节点 94</td>
<td>节点 93</td>
<td>节点 92</td>
<td>节点 91</td>
<td>节点 90</td>
<td>节点 89</td>
<td>节点 88</td>
</tr>
<tr>
<td>16</td>
<td>节点 103</td>
<td>节点 102</td>
<td>节点 101</td>
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
</tr>
<tr>
<td>17</td>
<td>节点 111</td>
<td>节点 110</td>
<td>节点 109</td>
<td>节点 108</td>
<td>节点 107</td>
<td>节点 106</td>
<td>节点 105</td>
<td>节点 104</td>
</tr>
<tr>
<td>18</td>
<td>节点 119</td>
<td>节点 118</td>
<td>节点 117</td>
<td>节点 116</td>
<td>节点 115</td>
<td>节点 114</td>
```
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移</th>
<th>名称</th>
<th colspan=8>描述或位索引</th>
</tr>
</thead>

<tbody>
<tr>
<td class='powderblued'>开始</td>
<td class='powderblued'>大小</td>
<td class='powderblued'>继电器</td>
<td class='powderblued'>位 7</td>
<td class='powderblued'>位 6</td>
<td class='powderblued'>位 5</td>
<td class='powderblued'>位 4</td>
<td class='powderblued'>位 3</td>
<td class='powderblued'>位 2</td>
<td class='powderblued'>位 1</td>
<td class='powderblued'>位 0</td>
</tr>
<tr>
<td>0</td>
<td>2</td>
<td>command</td>
<td colspan=8>获取 EtherNet/IP 状态 = 1014</td>
</tr>
<tr>
```html
<td>2</td>
<td>1</td>
<td>参数 1</td>
<td colspan=8>插槽编号 = 1 ~ 3</td>
</tr>
<tr>
<td>3</td>
<td>1</td>
<td>参数 2</td>
<td colspan=8>诊断从设备列表 = 7</td>
</tr>
<tr>
<td>4</td>
<td rowspan=16>16</td>
<td rowspan=16>从设备列表</td>
<td>节点 7</td>
<td>节点 6</td>
<td>节点 5</td>
<td>节点 4</td>
<td>节点 3</td>
<td>节点 2</td>
<td>节点 1</td>
<td>节点 0</td>
</tr>
<tr>
<td>5</td>
<td>节点 15</td>
<td>节点 14</td>
<td>节点 13</td>
<td>节点 12</td>
<td>节点 11</td>
<td>节点 10</td>
<td>节点 9</td>
<td>节点 8</td>
</tr>
<tr>
<td>6</td>
<td>节点 23</td>
<td>节点 22</td>
<td>节点 21</td>
<td>节点 20</td>
<td>节点 19</td>
<td>节点 18</td>
<td>节点 17</td>
<td>节点 16</td>
</tr>
<tr>
<td>7</td>
<td>节点 31</td>
<td>节点 30</td>
```
<td>节点 29</td>
<td>节点 28</td>
<td>节点 27</td>
<td>节点 26</td>
<td>节点 25</td>
<td>节点 24</td>
</tr>
<tr>
<td>8</td>
<td>节点 39</td>
<td>节点 38</td>
<td>节点 37</td>
<td>节点 36</td>
<td>节点 35</td>
<td>节点 34</td>
<td>节点 33</td>
<td>节点 32</td>
</tr>
<tr>
<td>9</td>
<td>节点 47</td>
<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
	<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
	<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
	<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
	<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
	<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
<td>节点 100</td>
		<td>节点 99</td>
		<td>节点 98</td>
		<td>节点 97</td>
		<td>节点 96</td>
	</tr>
	<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
	<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
		<td>节点 113</td>
		<td>节点 112</td>
	</tr>
	<tr>
		<td>19</td>
		<td>节点 127</td>
		<td>节点 126</td>
		<td>节点 125</td>
		<td>节点 124</td>
		<td>节点 123</td>
		<td>节点 122</td>
		<td>节点 121</td>
		<td>节点 120</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/6-slot-profinet-io-info.md)
# 3.4.14.6 S 继电器 - Profinet IO 主状态

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>


<br>

<br>

{% hint style="info" %}
\.		如果您想监视从站是否处于活动状态，请检查“IO 交换中的从站列表”。
{% endhint %}

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 Profinet IO 状态 = 1016</td>
	</tr>
	<tr>
```html
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>配置从属设备列表 = 5</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从属设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
```
```html
<td>节点 29</td>
<td>节点 28</td>
<td>节点 27</td>
<td>节点 26</td>
<td>节点 25</td>
<td>节点 24</td>
</tr>
<tr>
<td>8</td>
<td>节点 39</td>
<td>节点 38</td>
<td>节点 37</td>
<td>节点 36</td>
<td>节点 35</td>
<td>节点 34</td>
<td>节点 33</td>
<td>节点 32</td>
</tr>
<tr>
<td>9</td>
<td>节点 47</td>
<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
```
</tr>
		<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
</tr>
<tr>
<td>17</td>
<td>节点 111</td>
<td>节点 110</td>
<td>节点 109</td>
<td>节点 108</td>
<td>节点 107</td>
<td>节点 106</td>
<td>节点 105</td>
<td>节点 104</td>
</tr>
<tr>
<td>18</td>
<td>节点 119</td>
<td>节点 118</td>
<td>节点 117</td>
<td>节点 116</td>
<td>节点 115</td>
<td>节点 114</td>
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移</th>
<th>名称</th>
<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 Profinet IO 状态 = 1016</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>IO 交换中的从设备列表 = 6</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
```html
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
<tr>
<td>12</td>
<td>节点 71</td>
<td>节点 70</td>
<td>节点 69</td>
<td>节点 68</td>
<td>节点 67</td>
<td>节点 66</td>
<td>节点 65</td>
<td>节点 64</td>
</tr>
<tr>
<td>13</td>
<td>节点 79</td>
<td>节点 78</td>
<td>节点 77</td>
<td>节点 76</td>
<td>节点 75</td>
<td>节点 74</td>
<td>节点 73</td>
<td>节点 72</td>
</tr>
<tr>
<td>14</td>
```
```
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
		<td>节点 100</td>
		<td>节点 99</td>
		<td>节点 98</td>
		<td>节点 97</td>
		<td>节点 96</td>
	</tr>
		<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
		<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
```
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移量</th>
<th>名称</th>
<th colspan=8>描述或位索引</th>
</tr>
</thead>

<tbody>
<tr>
<td class='powderblued'>开始</td>
<td class='powderblued'>大小</td>
<td class='powderblued'>继电器</td>
<td class='powderblued'>位 7</td>
<td class='powderblued'>位 6</td>
<td class='powderblued'>位 5</td>
<td class='powderblued'>位 4</td>
<td class='powderblued'>位 3</td>
<td class='powderblued'>位 2</td>
<td class='powderblued'>位 1</td>
<td class='powderblued'>位 0</td>
</tr>
<tr>
<td>0</td>
<td>2</td>
<td>command</td>
<td colspan=8>获取 Profinet IO 状态 = 1016</td>
</tr>
<tr>
```html
<td>2</td>
<td>1</td>
<td>参数 1</td>
<td colspan=8>插槽编号 = 1 ~ 3</td>
</tr>
<tr>
<td>3</td>
<td>1</td>
<td>参数 2</td>
<td colspan=8>诊断从站列表 = 7</td>
</tr>
<tr>
<td>4</td>
<td rowspan=16>16</td>
<td rowspan=16>从站列表</td>
<td>节点 7</td>
<td>节点 6</td>
<td>节点 5</td>
<td>节点 4</td>
<td>节点 3</td>
<td>节点 2</td>
<td>节点 1</td>
<td>节点 0</td>
</tr>
<tr>
<td>5</td>
<td>节点 15</td>
<td>节点 14</td>
<td>节点 13</td>
<td>节点 12</td>
<td>节点 11</td>
<td>节点 10</td>
<td>节点 9</td>
<td>节点 8</td>
</tr>
<tr>
<td>6</td>
<td>节点 23</td>
<td>节点 22</td>
<td>节点 21</td>
<td>节点 20</td>
<td>节点 19</td>
<td>节点 18</td>
<td>节点 17</td>
<td>节点 16</td>
</tr>
<tr>
<td>7</td>
<td>节点 31</td>
<td>节点 30</td>
```
<td>节点 29</td>
<td>节点 28</td>
<td>节点 27</td>
<td>节点 26</td>
<td>节点 25</td>
<td>节点 24</td>
</tr>
<tr>
<td>8</td>
<td>节点 39</td>
<td>节点 38</td>
<td>节点 37</td>
<td>节点 36</td>
<td>节点 35</td>
<td>节点 34</td>
<td>节点 33</td>
<td>节点 32</td>
</tr>
<tr>
<td>9</td>
<td>节点 47</td>
<td>节点 46</td>
<td>节点 45</td>
<td>节点 44</td>
<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
		<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
```html
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
</tr>
<tr>
<td>17</td>
<td>节点 111</td>
<td>节点 110</td>
<td>节点 109</td>
<td>节点 108</td>
<td>节点 107</td>
<td>节点 106</td>
<td>节点 105</td>
<td>节点 104</td>
</tr>
<tr>
<td>18</td>
<td>节点 119</td>
<td>节点 118</td>
<td>节点 117</td>
<td>节点 116</td>
<td>节点 115</td>
<td>节点 114</td>
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>
```
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/7-slot-ethercat-info.md)
# 3.4.14.7 S 继电器 - EtherCAT 主状态

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>


<br>

<br>

{% hint style="info" %}
\.		如果您想监控从站是否处于活动状态，请检查“IO交换中的从站列表”。
{% endhint %}

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 EtherCAT 状态 = 1018</td>
	</tr>
	<tr>
```html
<td>2</td>
<td>1</td>
<td>参数 1</td>
<td colspan=8>插槽编号 = 1 ~ 3</td>
</tr>
<tr>
<td>3</td>
<td>1</td>
<td>参数 2</td>
<td colspan=8>已配置从站列表 = 5</td>
</tr>
<tr>
<td>4</td>
<td rowspan=16>16</td>
<td rowspan=16>从站列表</td>
<td>节点 7</td>
<td>节点 6</td>
<td>节点 5</td>
<td>节点 4</td>
<td>节点 3</td>
<td>节点 2</td>
<td>节点 1</td>
<td>节点 0</td>
</tr>
<tr>
<td>5</td>
<td>节点 15</td>
<td>节点 14</td>
<td>节点 13</td>
<td>节点 12</td>
<td>节点 11</td>
<td>节点 10</td>
<td>节点 9</td>
<td>节点 8</td>
</tr>
<tr>
<td>6</td>
<td>节点 23</td>
<td>节点 22</td>
<td>节点 21</td>
<td>节点 20</td>
<td>节点 19</td>
<td>节点 18</td>
<td>节点 17</td>
<td>节点 16</td>
</tr>
<tr>
<td>7</td>
<td>节点 31</td>
<td>节点 30</td>
```
<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
</tr>
		<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
```html
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
</tr>
<tr>
<td>17</td>
<td>节点 111</td>
<td>节点 110</td>
<td>节点 109</td>
<td>节点 108</td>
<td>节点 107</td>
<td>节点 106</td>
<td>节点 105</td>
<td>节点 104</td>
</tr>
<tr>
<td>18</td>
<td>节点 119</td>
<td>节点 118</td>
<td>节点 117</td>
<td>节点 116</td>
<td>节点 115</td>
<td>节点 114</td>
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移量</th>
<th>名称</th>
```
	<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 EtherCAT 状态 = 1018</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>IO 交换中的从设备列表 = 6</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
<tr>
<td>12</td>
<td>节点 71</td>
<td>节点 70</td>
<td>节点 69</td>
<td>节点 68</td>
<td>节点 67</td>
<td>节点 66</td>
<td>节点 65</td>
<td>节点 64</td>
</tr>
<tr>
<td>13</td>
<td>节点 79</td>
<td>节点 78</td>
<td>节点 77</td>
<td>节点 76</td>
<td>节点 75</td>
<td>节点 74</td>
<td>节点 73</td>
<td>节点 72</td>
</tr>
<tr>
<td>14</td>
```html
<td>节点 87</td>
<td>节点 86</td>
<td>节点 85</td>
<td>节点 84</td>
<td>节点 83</td>
<td>节点 82</td>
<td>节点 81</td>
<td>节点 80</td>
</tr>
<tr>
<td>15</td>
<td>节点 95</td>
<td>节点 94</td>
<td>节点 93</td>
<td>节点 92</td>
<td>节点 91</td>
<td>节点 90</td>
<td>节点 89</td>
<td>节点 88</td>
</tr>
<tr>
<td>16</td>
<td>节点 103</td>
<td>节点 102</td>
<td>节点 101</td>
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
</tr>
<tr>
<td>17</td>
<td>节点 111</td>
<td>节点 110</td>
<td>节点 109</td>
<td>节点 108</td>
<td>节点 107</td>
<td>节点 106</td>
<td>节点 105</td>
<td>节点 104</td>
</tr>
<tr>
<td>18</td>
<td>节点 119</td>
<td>节点 118</td>
<td>节点 117</td>
<td>节点 116</td>
<td>节点 115</td>
<td>节点 114</td>
```
```html
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移</th>
<th>名称</th>
<th colspan=8>描述或位索引</th>
</tr>
</thead>

<tbody>
<tr>
<td class='powderblued'>开始</td>
<td class='powderblued'>大小</td>
<td class='powderblued'>继电器</td>
<td class='powderblued'>位 7</td>
<td class='powderblued'>位 6</td>
<td class='powderblued'>位 5</td>
<td class='powderblued'>位 4</td>
<td class='powderblued'>位 3</td>
<td class='powderblued'>位 2</td>
<td class='powderblued'>位 1</td>
<td class='powderblued'>位 0</td>
</tr>
<tr>
<td>0</td>
<td>2</td>
<td>command</td>
<td colspan=8>获取 EtherCAT 状态 = 1018</td>
</tr>
<tr>
```
<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>诊断从设备列表 = 7</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
</tr>
		<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
<<<SOURCE_MARKDOWN_START>>>		<td>节点 100</td>
		<td>节点 99</td>
		<td>节点 98</td>
		<td>节点 97</td>
		<td>节点 96</td>
	</tr>
		<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
		<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
		<td>节点 113</td>
		<td>节点 112</td>
	</tr>
		<tr>
		<td>19</td>
		<td>节点 127</td>
		<td>节点 126</td>
		<td>节点 125</td>
		<td>节点 124</td>
		<td>节点 123</td>
		<td>节点 122</td>
		<td>节点 121</td>
		<td>节点 120</td>
	</tr>
</tbody>
</table><<<SOURCE_MARKDOWN_END>>>
[__SOURCE](3-relay/4-sw-relay/15-slot-ip-info.md)
# 3.4.15 S realy - IP_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_IP_INFO (172)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>局域网 (1~3)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=6>结果</td>
		<td>IP - 1</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>IP - 2</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>IP - 3</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>IP - 4</td>
<td>s2</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/16-slot-mech-info.md)
# 3.4.16 S继电器 - MECH_INFO

Supported from V60.30-01.

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_MECH_INFO (122)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>类型<br>1 = 当前机制 #</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>-</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>6</td>
		<td>-</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>8</td>
		<td>结果</td>
		<td>当前机制 # (0 ~ 7)</td>
		<td>s2</td>
</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/17-slot-tool-info.md)
# 3.4.17 S 继电器 - 工具信息

获取工具数据中设定的信息。 <br>
支持版本 V60.30-01。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_TOOL_INFO (174)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>工具编号</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>工具数据<br>0 = 长度, 1=角度, 2=中心, 3=惯性</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>结果</td>
		<td>工具重量</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>工具数据 X</td>
		<td>f4</td>
</tr>
	<tr>
		<td>12</td>
		<td>工具数据 Y</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>工具数据 Z</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/18-slot-ucrd-info.md)
# 3.4.18 S relay - UCRD_INFO

获取在用户坐标系统中注册的信息。 <br>
支持从 V60.30-01 开始。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_UCRD_INFO (176)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>用户坐标编号</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>用户坐标数据<br>0 = 长度, 1=角度</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=6>结果</td>
		<td>用户坐标数据 X</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>用户坐标数据 Y</td>
		<td>f4</td>
</tr>
	<tr>
		<td>12</td>
		<td>用户坐标数据 Z</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/4-sw-relay/19-slot-monopump.md)
# 3.4.19 S 릴레이 - MONOPUMP

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_MONITOR_INFO (4100)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>流量 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>rpm 命令</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>rpm 当前</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>压力 (bar)</td>
<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>流量（cc） - 车辆类型的总值</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_MANUAL_OPER1 (4110)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪编号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>结果</td>
		<td>流量（cc/s）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>流量（固定量模式）（cc）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>回吸流量（cc/s）</td>
		<td>f4</td>
</tr>
	<tr>
		<td>16</td>
		<td>回吸时间 (s)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_MANUAL_OPER2 (4112)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪编号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>结果</td>
		<td>延迟时间 (s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>补充流速 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>补充时间 (s)</td>
		<td>f4</td>
	</tr>
<tr>
		<td>16</td>
		<td></td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>SET_MANUAL_OPER (4111)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>设定数据项 <br>
		1 = 流量 (cc/s) <br>
		2 = 流量 (固定量模式) (cc) <br>
		3 = 吸回流量 (cc/s) <br>
		4 = 吸回时间 (s) <br>
		5 = 延迟时间 (s) <br>
		6 = 重新填充流量 (cc/s) <br>
		7 = 重新填充时间 (s)
		</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>参数 3</td>
```
		<td>值</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>10</td>
		<td>参数 4</td>
		<td>设置 = 1，设置值后强制初始化为 0</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>MANUAL_OPER (4113)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪编号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>操作项 <br>
		1 = 固定速度放电 <br>
		2 = 固定数量放电 <br>
		3 = 停止放电 <br>
		操作开始后强制初始化为 0 <br>
		</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
```
<br>

<table class="tg">
<thead>
	<tr>
		<th>S偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_COND_INFO1 (4120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>条件号 (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>结果</td>
		<td></td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>流量（固定量模式）(cc)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>回吸流量（cc/s）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
<td>吸回时间 (秒)</td>
<td>f4</td>
</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_COND_INFO2 (4122)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>条件号 (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>结果</td>
		<td>延迟时间 (秒)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>补充流量 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
<td>补充时间 (s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td></td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>SET_COND_INFO (4121)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>条件编号 (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>设置数据项 <br>
		2 = 流量 (固定量模式) (cc) <br>
		3 = 吸回流量 (cc/s) <br>
		4 = 吸回时间 (s) <br>
		5 = 延迟时间 (s) <br>
		6 = 充填流量 (cc/s) <br>
		7 = 充填时间 (s)
		</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>参数 3</td>
		<td>值</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>10</td>
		<td>参数 4</td>
		<td>设置 = 1，设置值后强制初始化为 0</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/5-relative-addr.md)
# 3.5 为继电器指定间接地址

SW62-SW79 是用于指定间接地址的系统内存。无论继电器类型如何，如果为继电器地址指定了-2到-18之间的值，则该设置值将导致存储在 SW62-SW79 中的指定继电器地址。



![](../_assets/rel-addr-concept.png)

例如，当 SW62-SW79 的某些值如下时，

| **继电器** | **值** |
| :---      | :---      |
| SW62      | 12        |
| SW70      | 3         |
| SW78      | 56        |

间接地址的表示可以解释如下。

*	MW-2 -> MW12
*	FB-10.X3 -> FB3.X3
*	X-18 -> X56
*	FB-10.YW-2 -> FB3.YW12

下面呈现的嵌入式可编程逻辑控制器 (PLC) 示例是使用 FOR/NEXT 指令和间接地址指定方法创建的输出信号 Y1-Y128 与输入信号 X1-X128 对应的示例。

![](../_assets/rel-addr-for-next.png)
[__SOURCE](4-instruction/README.md)
# 4. 指示

梯形图程序由多个梯级组成，每个梯级由多个指令组成。

嵌入式 PLC 在顺序执行程序中的指令时执行逻辑输入/输出操作。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table>
<thead>
  <tr>
    <td rowspan="11">ladder project</td>
    <td rowspan="7">ladder program</td>
    <td rowspan="3">rung</td>
    <td>指令</td>
  </tr>
  <tr>
    <td>指令</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">rung</td>
    <td>指令</td>
  </tr>
  <tr>
    <td>指令</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td>...</td>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">ladder program</td>
    <td rowspan="2">rung</td>
    <td>指令</td>
  </tr>
  <tr>
    <td>指令</td>
  </tr>
  <tr>
<td>...</td>
    <td>...</td>
  </tr>
  <tr>
    <td>...</td>
    <td>...</td>
    <td>...</td>
  </tr>
</thead>
</table>

<br><br>

指令由三个元素组成，如下所示。

<table>
<thead>
  <tr>
    <th>指令（助记符）</th>
    <th>操作类型</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>操作数</td>
    <td>操作的参数。<br>根据指令，可以指定一个或多个操作数，但某些指令没有操作数。</td>
  </tr>
  <tr>
    <td>注释</td>
    <td>用于提高程序可读性的描述。注释不影响操作。</td>
  </tr>
</tbody>
</table>
[__SOURCE](4-instruction/1-inst-list.md)
# 4.1 指令列表


<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

### * 梯子和分支
<br>

<table>
<thead>
  <tr>
    <th>助记符</th>
    <th>名称</th>
    <th>符号</th>
    <th>描述</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>RUNG</td>
    <td>梯级</td>
    <td>├─┤</td>
    <td>梯级</td>
  </tr>
  <tr>
    <td>BST</td>
    <td>分支开始</td>
    <td>┬─</td>
    <td>分支的开始</td>
  </tr>
  <tr>
    <td>BND</td>
    <td>分支结束</td>
    <td>─┬</td>
    <td>分支的结束</td>
  </tr>
  <tr>
    <td>NXB</td>
    <td>嵌套分支</td>
    <td>└,├</td>
    <td>分支的嵌套</td>
  </tr>
</tbody>
</table>
### * 逻辑检查说明：如果检查结果为真，则梯级处于活动状态。如果为假，则梯级处于非活动状态。 
<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>XIC</td>
		<td>检查是否关闭</td>
		<td>-| |-</td>
		<td>检查接触点是否关闭（接触点 A）</td>
	</tr>
	<tr>
		<td>XIO</td>
		<td>检查是否打开</td>
		<td>-|/|-</td>
		<td>检查接触点是否打开（接触点 B）</td>
	</tr>
	<tr>
		<td>INV</td>
		<td>反转</td>
		<td>-//-</td>
		<td>反转梯级的结果（反转）</td>
	</tr>
	<tr>
		<td>EQU</td>
		<td>反转</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否相等 (=)</td>
	</tr>
	<tr>
		<td>NEQ</td>
		<td>反转</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否不相等 (<>)</td>
	</tr>
	<tr>
		<td>LES</td>
		<td>小于</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否小于 (<)</td>
</tr>
	<tr>
		<td>GRT</td>
		<td>大于</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否大于 (>)</td>
	</tr>
	<tr>
		<td>LEQ</td>
		<td>小于或等于</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否小于或等于 (<=)</td>
	</tr>
	<tr>
		<td>GEQ</td>
		<td>大于或等于</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否大于或等于 (>=)</td>
	</tr>
</tbody>
</table>

<br><br>  

### * 输出说明

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>OTE</td>
		<td>输出激活</td>
		<td>-( )-</td>
		<td>梯级的状态 (激活: ON/未激活: OFF) 将被输出</td>
	</tr>
	<tr>
		<td>OTL</td>
		<td>输出锁存</td>
		<td>-(L)-</td>
		<td>如果梯级是激活的，输出信号将以 ON (高) 状态输出</td>
	</tr>
<tr>
		<td>OTU</td>
		<td>输出解锁</td>
		<td>-(U)-</td>
		<td>如果梯级处于活动状态，则输出信号将以关闭（低）状态输出</td>
	</tr>
	<tr>
		<td>OSR</td>
		<td>单次上升</td>
		<td>-(OSR)-</td>
		<td>如果梯级处于活动状态，则输出信号仅在一次扫描的持续时间内以开启状态输出</td>
	</tr>
	<tr>
		<td>RES</td>
		<td>重置</td>
		<td>-(RES)-</td>
		<td>如果梯级处于活动状态，则定时器或计数器将被重置</td>
	</tr>
</tbody>
</table>



<br><br>  

### * 定时器和计数器指令

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TON</td>
		<td>定时开启延迟</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>定时器仅在梯级处于活动状态时工作</td>
	</tr>
	<tr>
		<td>CTD</td>
		<td>倒计时</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>梯级的激活（非活动 -> 活动）将被倒计时</td>
</tr>
</tbody>
</table>


<br><br>  

### * 算术操作说明

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>ADD</td>
		<td>加法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行加法 (+) 操作</td>
	</tr>
	<tr>
		<td>SUB</td>
		<td>减法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行减法 (-) 操作</td>
	</tr>
	<tr>
		<td>MUL</td>
		<td>乘法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行乘法 (x) 操作</td>
	</tr>
	<tr>
		<td>DIV</td>
		<td>除法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行除法 (/) 操作</td>
	</tr>
	<tr>
		<td>POW</td>
		<td>幂</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行幂 (^) 操作</td>
</tr>
	<tr>
		<td>与</td>
		<td>按位与</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，则执行按位与 (&) 操作</td>
	</tr>
	<tr>
		<td>或</td>
		<td>按位或</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，则执行按位或 (|) 操作</td>
	</tr>
</tbody>
</table>




<br><br>  

### * 数据转换说明

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TOD</td>
		<td>将整数转换为BCD</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，则整数将被转换为BCD</td>
	</tr>
	<tr>
		<td>FRD</td>
		<td>将BCD转换为整数</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，则BCD将被转换为整数</td>
	</tr>
	<tr>
		<td>SEG</td>
		<td>7段</td>
<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于激活状态，则将转换为7段值</td>
	</tr>
</tbody>
</table>


<br><br>  

### * 移动和复制指令

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>MOV</td>
		<td>移动</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于激活状态，则将复制一条数据</td>
	</tr>
	<tr>
		<td>COP</td>
		<td>复制数据</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于激活状态，则将复制多条数据</td>
	</tr>
	<tr>
		<td>CCOP</td>
		<td>条件复制数据</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>根据梯级的状态将复制多条数据</td>
	</tr>
	<tr>
		<td>ROT</td>
		<td>旋转输出</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于激活状态，则将进行顺序输出</td>
	</tr>
</tbody>
</table>
### * 阻塞控制指令

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>FOR</td>
		<td>FOR 循环</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，将进行重复执行，直到 Next</td>
	</tr>
	<tr>
		<td>NEXT</td>
		<td>NEXT 循环</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果计数在重复计数范围内，将跳转到 FOR 指令</td>
	</tr>
	<tr>
		<td>LBL</td>
		<td>标签</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>根据 JMP 指令指定一个跳转位置</td>
	</tr>
	<tr>
		<td>JMP</td>
		<td>跳转</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，将跳转到 LBL 位置<br>
		(如果 Label&lt;0，跳过 -n NEXTs)</td>
	</tr>
	<tr>
		<td>CALL</td>
		<td>调用</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，将调用一个子梯级</td>
	</tr>
	<tr>
		<td>END</td>
<td>结束</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，从梯子将结束</td>
	</tr>
</tbody>
</table>
[__SOURCE](4-instruction/2-xic.md)
# 4.2 XIC (检查是否关闭): 检查是否关闭

### 描述
如果操作数的位值为1，则该梯级将被激活。如果为0，则将被禁用。

<br>

### 可用作操作数的类型
(不适用于X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常数<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>
<br>

### 使用示例

当运行开关，即输入 X2 的接点 A，处于按下状态 (1 = 激活) 且内部状态继电器 M5 正常 (1) 时，"运行" 灯输出 Y5 将会开启。 

![](../_assets/xic.png)
[__SOURCE](4-instruction/3-xio.md)
# 4.3 XIO (检查是否打开)：检查是否打开

### 描述
如果操作数的位值为 0，则该行将激活。如果为 1，则将其设置为非活动状态。

<br>

### 可以用作操作数的类型
(对于 X 不可能)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>
<br>

### 使用示例

当“暂停”按钮，即输入 X1 的接触 B，处于按下状态（0 = 激活）时，刹车输出 Y8 将被打开。  

![](../_assets/xio.png)
[__SOURCE](4-instruction/4-inv.md)
# 4.4 INV (反转): 反转


### 描述
反转（活动 <-> 非活动）梯级的先前结果。

<br>

### 使用示例

根据德摩根定律，处理反转将使 /(AxB) 等于 /A+/B 或 /(A+B) 等于 /Ax/B，从而允许使用没有分支的AND逻辑的简单配置，而不是使用具有多个分支的OR逻辑配置。因此，下面两个梯级的逻辑将具有相同的结果，因为 (X1+X2+X3) 等于 /(/X1x/X2x/X3)。

![](../_assets/inv.png)
[__SOURCE](4-instruction/5-equ.md)
# 4.5 EQU (等于): 检查是否相等


### 描述
如果比较两个值并发现它们相等，则该梯级将被激活（接触活跃）。

<br>

### 可用作操作数的类型
(不适用于 X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入XB3的值等于100，则输出Y7将被打开。否则，将被关闭。

![](../_assets/equ.png)
[__SOURCE](4-instruction/6-neq.md)
# 4.6 NEQ (不等于): 检查是否不相等


### 描述
如果比较两个值并发现它们不相等，则该 rung 将被激活（接触激活）。

<br>

### 可以用作操作数的类型
(不能用于 X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量.<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 A</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入 XB4 的值不等于 50，输出 Y8 将被打开。否则，它将被关闭。

![](../_assets/neq.png)
[__SOURCE](4-instruction/7-les.md)
# 4.7 LES (小于): 检查是否小于

### 描述
如果“源 a”的值小于“源 b”的值，则此梯级将被激活（接触激活）。

<br>

### 可用作操作数的类型
(不适用于 X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入 XB7 的值小于 70，则输出 Y9 将被打开。如果大于或等于 70，则输出将被关闭。

![](../_assets/les.png)
[__SOURCE](4-instruction/8-grt.md)
# 4.8 GRT (大于): 检查是否大于

### 描述
如果“源 a”的值大于“源 b”的值，则该梯级将处于活动状态（接触点激活）。

<br>

### 可用作操作数的类型
（对于 X 不可能）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常数<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>来源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入 XB8 的值大于 80，则输出 Y10 将被打开。如果小于或等于 80，则输出将被关闭。

![](../_assets/grt.png)
[__SOURCE](4-instruction/9-leq.md)
# 4.9 LEQ（小于或等于）：检查是否小于或等于

### 描述
如果“源 a”的值小于或等于“源 b”的值，则该 rung 将被激活（接触活动）。

<br>

### 可用作操作数的类型
（对 X 不可能）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
<tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入 XB9 的值小于或等于 90，则输出 Y11 将被打开。如果大于 90，输出将被关闭。

![](../_assets/leq.png)
[__SOURCE](4-instruction/10-geq.md)
# 4.10 GEQ (大于或等于): 检查是否大于或等于

### 描述
如果“源 a”的值大于或等于“源 b”的值，则该横杠将被激活（接触激活）。

<br>

### 可用作操作数的类型
(不适用于 X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入 XB9 的值大于或等于 100，输出 Y12 将被开启。如果小于 100，输出将被关闭。

![](../_assets/geq.png)
[__SOURCE](4-instruction/11-ote.md)
# 4.11 OTE (输出使能): 激活输出

### 描述
输出信号将根据梯级的状态输出。换句话说，如果梯级处于激活状态，输出信号将以 ON（高）状态输出，但如果梯级处于非激活状态，输出信号将以 OFF（低）状态输出。

<br>

### 可用作操作数的类型
(对于 X 不可能，DO 位从 V60.30-07 开始支持)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X, -</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>
<br>

### 使用示例

Y12将在输入DO12的状态下输出。

![](../_assets/ote.png)
[__SOURCE](4-instruction/12-otl.md)
# 4.12 OTL (输出锁存器): 锁存输出

### 描述
如果梯级处于活动状态，输出信号将以 ON（高）状态输出。然而，如果梯级处于非活动状态，输出将保持不变。

<br>

### 可以用作操作数的类型
（对于 X，不可能，DO 位支持从 V60.30-07 开始）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X, -</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>
<br>

### 使用示例

如果输入的 DO13 处于 ON 状态，Y13 将处于 ON 状态。即使 DO13 随后切换到 OFF 状态，Y13 仍将保持在 ON 状态。

![](../_assets/otl.png)
[__SOURCE](4-instruction/13-otu.md)
# 4.13 OTU (输出解除锁定): 解除锁定输出

### 描述
如果梯级处于活动状态，输出信号将以关闭（低）状态输出。 但是，如果梯级处于非活动状态，输出将保持不变。

<br>

### 可用作操作数的类型
（对X不可用，DO位支持自V60.30-07起）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X, -</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>
<br>

### 使用示例

当输入 DO14 处于开启状态时，Y14 将处于关闭状态。即使 DO14 随后切换到关闭状态，Y14 仍将保持在关闭状态。

![](../_assets/otu.png)
[__SOURCE](4-instruction/14-osr.md)
# 4.14 OSR (One Shot Rising): 一次上升输出

### 描述
如果梯级处于活动状态，输出信号仅会在一次扫描的持续时间内输出。换句话说，当梯级从非活动状态切换到活动状态时，相关继电器将在一次扫描的持续时间内处于ON状态。

<br>

### 可用作操作数的类型
（对于X，不可能，DO位从V60.30-07开始支持）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X, -</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>
<br>

### 使用示例

如果输入 X17 处于开启状态，内部状态继电器 M17 将处于开启状态。M17 会保持在开启状态，直到相关扫描完成，如果启动新的扫描，它将切换到关闭状态。

![](../_assets/osr.png)
[__SOURCE](4-instruction/15-res.md)
# 4.15 重置 (RES)：重置


### 描述
 如果该梯级处于活动状态，则定时器 (T) 或计数器 (C) 继电器值将被清除 (-1)。

<br>

### 可用作操作数的类型
(不适用于 X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th colspan="2">定时器<br>T</th>
    <th colspan="2">计数<br>C</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
<td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果内部状态继电器 M18 处于开启状态，则 T28 的定时器继电器将被重置为 -1。

![](../_assets/res.png)
[__SOURCE](4-instruction/16-ton.md)
# 4.16 时间延迟 (TON): 定时器

### 描述
在计算了继电器活动期间的时间（定时器基数 x 预设 x 10）[毫秒]后，相关的定时继电器将处于ON（高）状态。然而，如果继电器处于非活动状态，相关的定时继电器将立即被清除 (-1)。 
注意）T的值单位为1毫秒。

<br>

### 可以作为操作数使用的类型
（不适用于X）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th colspan="2">定时器<br>T</th>
    <th>常量<br>32bit</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>定时器</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>计时器基准(1/100s)</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>预设</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

当输入 DO34 处于 ON 状态后经过一秒时，T32 的定时器继电器将处于 ON 状态。此时，输出 Y34 将处于 ON 状态。

![](../_assets/ton.png)
[__SOURCE](4-instruction/17-ctd.md)
# 4.17 倒计时 (CTD)：计数器

### 描述
继电器的上升（从非活动转为活动）将被倒计时。如果相关 C 的值变为 0，相关计数器将处于 ON（高）状态，不再进行计数。当继电器处于活动状态但相关 C 的值为负时，预设值将被存储在 C 中。注意）即使继电器处于非活动状态，C 也不会被清除（-1）。要清除，必须执行 RES 指令。

<br>

### 可用作操作数的类型
(对 X 无效)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI</th>
    <th colspan="2">内存<br>M, S</th>
    <th colspan="2">计数<br>C</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>计数器</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
<td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>预设</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果内部状态继电器 M19 从 OFF 状态切换到 ON 状态，C20 的值从 3 开始并持续减少 1。当 C20 的值变为 0 时，计数器继电器将处于 ON 状态。此时，输出 Y35 将处于 ON 状态。

![](../_assets/ctd.png)
[__SOURCE](4-instruction/18-add.md)
# 4.18 加法 (ADD): 添加


### 描述
如果梯级处于活动状态，"source a" 的值和 "source b" 的值将相加，结果值将设置在 "destination" 继电器中。如果操作结果发生溢出，将发生设置 S7=1。

<br>

### 可用作为操作数的类型
(对于 X 不可能)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常数.<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目的地</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

当输入 DO36 处于活动状态时，50 将被添加到 XB3 的值，并且结果值将被设置在内部状态继电器 MB3 中。

![](../_assets/add.png)
[__SOURCE](4-instruction/19-sub.md)
# 4.19 减法 (SUB): 减去


### 描述
如果梯级处于活动状态，“源 b”的值将从“源 a”的值中减去，结果值将设置在“目标”继电器中。

<br>

### 可用作操作数的类型
(对于 X 不允许)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常数.<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目的地</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入 DO37 是激活状态，则从 XB3 的值中减去 10，结果值将设置在内部状态继电器 MB3 中。

![](../_assets/sub.png)
[__SOURCE](4-instruction/20-mul.md)
# 4.20 乘法 (MUL)：乘法

### 描述
如果梯级处于活动状态，"源 a" 的值将乘以 "源 b" 的值，结果值将设置在 "目标" 继电器中。如果操作结果发生溢出，将发生设置 S7=1。

<br>

### 可用作为操作数的类型
(不适用于 X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常数<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目的地</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入DO38处于活动状态，XB3的值将乘以3，结果值将设置在内部状态继电器MB3中。

![](../_assets/mul.png)
[__SOURCE](4-instruction/21-div.md)
# 4.21 除法 (DIV)：除法


### 描述
如果梯级处于活动状态，则“源 a”的值将被“源 b”的值除，并且结果值将设置在“目的地”继电器中。如果“源 b”的值为 0 或操作结果发生溢出，则将发生设置 S7=1。

<br>

### 可用作操作数的类型
(对X不可用)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目的地</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 用法示例

如果输入 DO39 处于活动状态，XB3 的值将除以 4，结果值将被设置在内部状态继电器 MB3 中。

![](../_assets/div.png)
[__SOURCE](4-instruction/22-pow.md)
# 4.22 功率 (POW)：功率

### 描述
如果梯级处于活动状态，"source a" 的值将提升到 "source b" 的值的幂，结果值将被设置在 "destination" 继电器中。如果操作结果溢出，将发生设置 S7=1。

<br>

### 可用作操作数的类型
(对于 X 不可能)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目标</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 示例使用

如果输入 DO40 被激活，XB3 的值将被提升到 2 次方，结果值将被设置在内部状态继电器 MB3 中。

![](../_assets/pow.png)
[__SOURCE](4-instruction/23-tod.md)
# 4.23 TOD (转换为BCD)：转换为BCD

### 描述
如果梯级处于活动状态，“源”的值将被转换为BCD值，转换后的值将存储在“目的地”中。当使用以BCD格式显示值的7段显示器时，此指令将非常方便。如果“目的地”的数据类型为字节（B）格式，“源”的值将被转换为两个数字。如果为字（W）格式，“源”的值将被转换为四个数字。但是，如果“源”的值大于要转换的数字位数，将发生设置S6=1。

<br>

### 可用作操作数的类型
（X，不可用于无符号整数u）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>u</td>
  </tr>
<tbody>
  <tr>
    <td class='hd'>目的地</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入的DO42处于活动状态，XB3的值将被转换为BCD值，转换后的值将被设置在内部状态继电器MB3中。 
（注意：二进制编码十进制（BCD）是指其4位代码值可以在0到9之间变化的数字。也就是说，对于BCD数字，0-F中可以用4位表示的数字中的A-F不使用。）
如果&H7B(123)被转换为BCD值，转换后的值将是&H23(35)，并且由于&H7B(123)大于&H63(99)，因此将发生设置S6=1。 

![](../_assets/tod.png)
[__SOURCE](4-instruction/24-frd.md)
# 4.24 FRD (从 BCD 转换为整数)：转换为整数

### 描述
如果梯级处于活动状态，“源”的 BCD 值将被转换为整数，并且转换后的值将存储在“目标”中。 
当以 BCD 格式接收到凸轮开关输出值作为输入时，此指令可以方便地使用。
如果“源”的值不是 BCD 值，将发生设置 S6=1。
此外，如果“源”以字 (W) 格式表示，而“目标”以字节 (B) 格式表示，则要转换的“源”的最大值为 &H9999。因此，转换为整数的结果将是 9999 (&H270F)，这将导致字节范围 &Hff 被超出，从而发生溢出。在这种情况下，将发生设置 S=6。

<br>

### 可以作为操作数使用的类型
(对于 X 不可能，u 的无符号整数)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>u</td>
</tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目标</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入的 DO43 处于活动状态，则 XB3 的值（BCD）将转换为整数，转换后的值将设置在内部状态继电器 MB3 中。
如果 &H23(35) 被转换为整数，则该整数将是 &H17(23)。

![](../_assets/frd.png)
[__SOURCE](4-instruction/25-seg.md)
# 4.25 SEG (7段): 转换为7段值

### 描述
如果梯级处于活动状态，则“源”的值将被转换为7段值（8位），并将转换后的值存储在“目标”中。
如果“目标”处于字（W）格式，则两个7段格式（8位）的值将存储在“目标”中。

<br>

### 可用作操作数的类型
（X、无符号整数u不适用）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>u</td>
  </tr>
<tbody>
  <tr>
    <td class='hd'>目的地</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入的DO44处于活动状态，则与XB3的值相对应的7段数值将被设置在内部状态继电器MW3中。
对于&H17，值&H0607结合了SEGD_1(SEGM_B|SEGM_C = 0x02|0x04 = 0x06)=&H06和 
SEGD_7(SEGM_A|SEGM_B|SEGM_C = 0x01|0x02|0x04 = 0x07)=&H07，将被存储在内部状态继电器MW3中。


![](../_assets/seg.png)


<br>

### 7段数据

![](../_assets/seg_data.png)

SEGM_A = 0x01<br>
SEGM_B = 0x02<br>
SEGM_C = 0x04<br>
SEGM_D = 0x08<br>
SEGM_E = 0x10<br>
SEGM_F = 0x20<br>
SEGM_G = 0x40<br>
SEGM_DP = 0x80<br>
[__SOURCE](4-instruction/26-mov.md)
# 4.26 MOV (移动): 移动

### 描述
如果梯级处于活动状态，则“源”的值将被复制到“目标”。
如果“源”是字（W）格式，且“目标”是字节（B）格式，则“源”值的低字节将被复制到“目标”。
由于嵌入式可编程逻辑控制器（PLC）的所有数据都作为有符号数据处理，如果“源”是字节（B）格式且其值为-1（&Hff），则该值将以-1（&HFFFF）复制到“目标”，该“目标”为字（W）格式（&H00ff变为255的值）。

<br>

### 可以作为操作数使用的类型
（X不可能）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>比特</th>
    <th>B,W,L,F</th>
    <th>比特</th>
    <th>B,W,L,F</th>
    <th>比特</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
<td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目标</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入DO55处于活动状态，则将55设置在内部状态继电器MB2中。

![](../_assets/mov.png)
[__SOURCE](4-instruction/27-cop.md)
# 4.27 复制数据 (COP): 复制


### 描述
如果梯级处于活动状态，值将从“源”的位置复制到“目标”的位置，数量等于“长度”的值。
如果“源”是一个数字，则“目标”将用“源”的值填充，数量等于“长度”的值。在这种情况下，当“目标”处于位格式时，如果“源”的值为0，则“目标”将填充为OFF；如果“源”的值不为0，则“目标”将填充为ON。
如果“源”是继电器，则“源”和“目标”的数据类型必须相同。也就是说，如果“源”处于位格式，则“目标”也应处于位格式；如果“源”处于字节 (B) 格式，则“目标”应处于字节 (B) 格式；如果“源”处于字 (W) 格式，则“目标”也应处于字 (W) 格式。
如果“源” + “长度”大于“源”继电器的最大数量或“目标” + “长度”大于“目标”继电器的最大数量，那么复制操作将仅执行到最大数量的继电器为止。


<br>

### 可用作操作数的类型
(不适用于 X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
<td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目标</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>长度</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入 DO56 处于活动状态，则对应 8 字节的值将从输入 DOB2 复制到输出 YB2，作为对应的 8 字节的值。

![](../_assets/cop.png)
[__SOURCE](4-instruction/28-ccop.md)
# 4.28 条件复制数据 (CCOP)：条件复制

### 描述
根据梯级的状态，值将从“源 a”或“源 b”的位置复制到“目的地”的位置，复制数量为“长度”的值。
如果“源”是一个数字，则“目的地”将填充为与“长度”值相等的相关值。在这种情况下，当“目的地”为比特格式时，如果相关值为 0，则“目的地”将填充 OFF；如果相关值不为 0，则“目的地”将填充 ON。
如果“源”是一个继电器，则“源”和“目的地”的数据类型应相同。也就是说，如果“源”是比特格式，则“目的地”也应为比特格式；如果“源”是字节 (B) 格式，则“目的地”应为字节 (B) 格式；如果“源”是字 (W) 格式，则“目的地”也应为字 (W) 格式。
如果“源” + “长度”大于“源”继电器的最大数量，或者“目的地” + “长度”大于“目的地”继电器的最大数量，则复制仅直到最大继电器数量为止。

<br>

### 可用作运算符的类型
(对于 X 不适用)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">存储器<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>比特</th>
    <th>B,W,L,F</th>
    <th>比特</th>
    <th>B,W,L,F</th>
    <th>比特</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
<td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>源 b</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目的地</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>长度</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入 DO57 激活，来自输入 DOB2 的 4 字节值将作为对应的 4 字节值复制到输出 YB2。相反，如果输入 DO57 激活，来自输入 DOB12 的 4 字节值将作为对应的 4 字节值复制到输出 YB2。

![](../_assets/ccop.png)
[__SOURCE](4-instruction/29-rot.md)
# 4.29 ROT (旋转输出): 旋转输出

### 描述
如果梯级处于活动状态，则在“计数”范围内的非0继电器值将在“开始继电器”到“输出继电器”之间输入，持续时间为“重复时间”。如果“复位继电器”有信号输入，则“开始继电器”将根据“计数”的数量被填充为0，定时器的值将初始化为“重复时间”的值，且“输出继电器”将输出0。该指令在需要在仅可输出错误编号的设备可用的情况下输出特定时间的错误编号时，可以非常方便地使用，尽管可能发生多种类型的错误。

<br>

### 可以用作操作数的类型
(对于 X 不可能)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th colspan="2">定时器<br>T</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>开始继电器</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
</tr>
</tbody>
<tbody>
<tr>
<td class='hd'>计数</td>
<td>X</td>
<td></td>
<td>X</td>
<td>X</td>
<td>X</td>
<td></td>
<td>X</td>
<td>X</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr>
<td class='hd'>定时继电器</td>
<td>X</td>
<td>X</td>
<td>x</td>
<td>X</td>
<td>X</td>
<td>X</td>
<td></td>
<td>X</td>
<td>X</td>
</tr>
</tbody>
<tbody>
<tr>
<td class='hd'>重复时间</td>
<td>X</td>
<td></td>
<td>X</td>
<td></td>
<td>X</td>
<td></td>
<td>X</td>
<td>X</td>
<td></td>
</tr>
</tbody>
<tbody>
<tr>
<td class='hd'>输出继电器</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>复位继电器</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>温度继电器</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果存在一个或多个与错误条件1到3相关的错误，则错误编号将存储在MW50-MW55。在这里，当输入DO58激活时，由ROT指令生成的错误编号将存储在MW70中，持续2秒，同时该数字将通过TOD指令转换为BCD值，并依次显示在连接到YB3的显示设备上。如果连接的X3有输入信号，用于外部错误复位信号，则存储错误编号的MW51-MW55的内容将被清零，MW70和MW80也将清零，并且显示设备将相应地显示0。

![](../_assets/rot.png)

[__SOURCE](4-instruction/30-for.md)
# 4.30 FOR : 重复执行块


### 描述
如果横档处于活动状态，从“下一条”指令开始，块将被重复执行，而“idx”继电器的值将从“init”值增加到“final”值的“step”值。
当执行FOR指令时，“init”值应无条件替换为“idx”继电器。
FOR/NEXT指令最多可以嵌套10层。例如：→ FOR() FOR() FOR() ... .NEXT NEXT NEXT
在“step”值大于0的情况下，如果“init”值大于“final”值，则不会执行。相反，将跳转到下一条指令。
在“step”值小于0的情况下，如果“init”值小于“final”值，则不会执行。相反，将跳转到下一条指令。
“final”和“step”可以指定为变量。然而，只有在执行FOR指令时的数值会被使用。
在特殊情况下，要在FOR指令中途退出，可以使用后面将描述的JMP（负数）指令（请参阅JMP指令的描述）。
注意：FOR指令没有任何分支的额外处理。
注意：有关NEXT指令的更多细节，请参阅[4.31 NEXT (NEXT)](./31-next)

<br>

### 可以作为操作数的类型
(无法用于X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>idx</td>
    <td>X</td>
    <td>X</td>
<td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>初始</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>最终</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>步骤</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

The instruction {XIC(DO-2), OTL(Y-2)} will be executed in repetition, while the value will increase by 1 from 1 to 4 in SW62.
换句话说，在“idx”使用继电器进行相对寻址（SW62-SW79）的状态下，XIC 指令的 DO 继电器和 OTL 指令的 Y 继电器为“-2”，SW62 的值中的数字将被应用。因此，对应于 DO1-DO4 中高态信号的数字的 Y 继电器数将以高态输出，而未输入的数字的 Y 输出将保持其先前状态。
注意：相对寻址是指当相关继电器设置为范围在 -2 到 -9 之间的数字时，将继电器地址指定为存储在 SW62-SW79 中的值，而不考虑继电器的类型。
[__SOURCE](4-instruction/31-next.md)
# 4.31 NEXT : Next Block


### 描述
操作将根据 FOR 指令的“步骤”进行执行。
如果“步骤”值大于 0，则执行将重复进行，直到“idx”继电器值小于或等于“final”值。
如果“步骤”值小于 0，则执行将重复进行，直到“idx”继电器值大于或等于“final”值。
如果没有 FOR 指令而执行 NEXT 指令，该 NEXT 指令将被忽略。
注意：  
FOR/NEXT 指令没有任何额外的分支处理。因此，如果 FOR 指令记录在分支内部，而 NEXT 指令记录在分支外部或另一个分支内部，FOR 指令将无法正确操作。
注意：有关 FOR 指令的更多详细信息，请参考 [4.30 FOR (FOR)](./30-for)

<br>

### 使用示例

请参考 FOR 指令的使用示例。
[__SOURCE](4-instruction/32-lbl.md)
# 4.32 LBL (标签): 指定标签


### 描述
跳转到的标签位置将被指定为一个大于 0 的数字 (const)。 
LBL 指令将无论横杆是否处于活动或非活动状态，都指定该位置。
注意：有关 JMP 指令的更多详细信息，请参见 [4.33 JMP (跳转)](./33-jmp)

<br>

### 可以用作操作数的类型
(对于 X 不可能)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>标签</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

由于这些说明将与 JMP 命令一起使用，请参阅 JMP 指令的描述。
[__SOURCE](4-instruction/33-jmp.md)
# 4.33 JMP (跳转): 跳转


### 描述
如果 rung 处于活动状态，将跳转到与 "label" 中指定的标签值匹配的 LBL 指令所在的位置。 
特别地，如果 "label" 被指定为小于 0 的值，可以用作离开 FOR 指令中间的功能（根据负数中指定的数字跳过。）
注意 1:  
如果标签的位置在 JMP 指令上方，并且 JMP 指令前没有条件，可能会发生无限循环，这需要引起您的注意。当这种情况发生时，设置将为 S16=1，因为扫描时间超过 5 秒。
注意 2:  
在 FOR/NEXT 指令块内使用 JMP（正数）指令离开块可能会导致块控制出现问题。在这种情况下，需要编程一种方式，通过使用 JMP 指令（负数）跳转到 NEXT 指令。
注意: 有关 LBL 指令的更多细节，请参见 [4.32 LBL (标签)](./32-lbl)

<br>

### 可用作操作数的类型
(不适用于 X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">存储器<br>M, S</th>
    <th>常数.<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>idx</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
<td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入 DO19 是活动的，将根据 JMP 指令的“标签 99”跳转到相关的 LBL 指令。这意味着指令 {XIC(DO20), OTE(Y20)} 将不会被执行。  
如果输入 DO19 不活动，JMP 指令将不会被执行，因此下一梯级中写的 {XIC(DO20), OTE(Y20)} 指令将被执行。

![](../_assets/jmp.png)
[__SOURCE](4-instruction/34-call.md)
# 4.34 CALL (Call): 调用子梯程序

### 描述
如果梯级处于活动状态，将调用由“文件编号”指定的子梯程序，编号范围为（1到99）。
子梯程序最多可以有99个文件名，范围从 S01xxxx.LAD 到 S99xxxx.LAD，文件名的“xxxx”部分，用户可以任意添加最多15个字符。

<br>

### 可用作操作数的类型
(对于 X 不可用)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常数<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>idx</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

当输入 DO21 激活时，从 S01xxxx.LAD 到 S99xxxx.LAD 的文件将会轮流调用。
如果执行 CALL 指令时，与该编号相关的子梯级程序不存在，或该编号的值超出了 1 到 99 的范围，将会设置 S17=1。但是，如果 CALL 指令正常执行，将会设置 S17=0。因此，在应该有必要的子梯级的情况下，可以在调用后通过使用 S17 检测错误。  
如果在主梯级程序中使用 CALL 指令调用编号从 1 到 99 的子梯级，并为每个应用分配一个子梯级编号是可能的，那么我们可以期望通过控制器根据每个应用自动加载必要的子梯级程序以执行与应用相关的梯级程序。  

![](../_assets/call.png)
[__SOURCE](4-instruction/35-end.md)
# 4.35 结束 (End): 结束梯形程序

### 描述
如果梯级处于活动状态，当前正在执行的梯形程序将被结束。 
如果当前梯形程序是子梯形程序，将返回主梯形程序。然而，如果当前梯形程序是主梯形程序，其执行将被结束，然后从头开始再次执行主梯形程序。

<br>

### 使用示例

如果输入 DO22 处于活动状态，梯形程序将通过 END 指令结束，随后的梯级指令将不会被执行。
如果输入 DO22 处于非活动状态，END 指令将不会被执行，允许后续的梯级指令自然地被执行。

![](../_assets/end.png)
[__SOURCE](4-instruction/36-and.md)
# 4.36 位运算与（AND）：位操作与


### 描述
如果梯级处于活动状态，则“源 a”的值和“源 b”的值将进行按位与运算，结果值将被设置在“目标”继电器中。(支持的版本为 60.28-00 和 HRLadder v2.86b1)

<br>

### 可用作操作数的类型
（X无法使用）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32bit</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>源 b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目的地</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

当输入 DO36 被激活时，MB0 将按位与操作到 &HFF 的值，结果值将被设置在内部状态继电器 MW8 中。

![](../_assets/and.png)
[__SOURCE](4-instruction/37-or.md)
# 4.37 位运算或 (OR): 位操作或

### 描述
如果梯级处于活动状态，“源 a”的值和“源 b”的值将进行按位或运算，结果值将设置在“目标”继电器中。（支持的版本是 60.28-00 和 HRLadder v2.86b1）

<br>

### 可用作操作数的类型
（X不可用）
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th>常量<br>32位</th>
  </tr>
  <tr>
    <th>数据类型</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源 a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tr>
    <td class='hd'>来源b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目标</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

当输入DO36激活时，DOW2将与&H0F0F的值进行按位或运算，结果值将被设置在内部状态继电器DIL8中。

![](../_assets/or.png)
[__SOURCE](5-diff-hi5a-hi6.md)
# 5. Hi5a与Hi6/Hi7嵌入式PLC的区别

Hi6/Hi7控制器的嵌入式PLC的功能与Hi5a控制器的嵌入式PLC相似，并且使用相同的HRLadder或相同的梯形编辑器。 
因此，已经熟悉Hi5a控制器嵌入式PLC功能的用户可以通过仅查看Hi6/Hi7控制器的不同部分快速从本手册中学习。

以下内容包括不同部分的列表。

<br>

#### HRLadder在线连接

HRLadder v2.80及以上版本支持Hi6/Hi7控制器。
HRLadder v2.80之前的版本允许通过在按下在线按钮时自动识别控制器类型进行远程连接。
但是，对于HRLadder v2.80或更高版本，您需要在项目的属性中选择控制器类型，然后按下在线按钮。

![](_assets/hrladder-prj-prop.png)

![](_assets/hrladder-prj-prop2.png)

<br>

#### 继电器类型

##### Hi5a

支持MW1-MW1000的M继电器。
存在特殊继电器SP。
SW中包含专用输入和输出信号。

##### Hi6/Hi7

M继电器的大范围扩展至MW0-MW19998，因此可以用作其他继电器的替代品。
SP继电器集成在[固定区域](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/en/3-relay/4-sw-relay/1-fixed-area?cont_model=${cont_model})的特殊标志区域中。
对于专用输入和输出信号，将提供SI和SO支持。

<br>

#### 索引

##### Hi5a
索引从1开始。
字、长整型和浮点型的索引每次增加1。 
例如，DO16-DO23与DOW1相同。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table class="tg">
<tbody>
  <tr>
    <td class="tg-kftd">比特</td>
    <td>DO1~DO8</td>
    <td>DO9~DO16</td>
    <td>DO17~DO24</td>
    <td>DO25~DO32</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">字节</td>
    <td>DOB1</td>
    <td>DOB2</td>
    <td>DOB3</td>
    <td>DOB4</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">字</td>
    <td colspan="2">DOW1</td>
    <td colspan="2">DOW2</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">长整型</td>
    <td colspan="4">DOL1</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">浮点数</td>
    <td colspan="4">DOF1</td>
    <td>...</td>
  </tr>
</tbody>
</table>

<br>

##### Hi6/Hi7
索引从0开始。
字、长整型和浮点数的索引将根据字节位置增加。
例如，DOW以DOW0、DOW2、DOW4、DOW6...的形式增加，而DOL以DOL0、DOL4、DOL8...的形式增加。
如下图所示，DO16-DO23与DOW2相同。

参考 [3.2 指定继电器](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/en/3-relay/2-relay-expression?cont_model=${cont_model})
<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table class="tg">
<tbody>
  <tr>
    <td class="tg-kftd">位</td>
    <td>DO0~DO7</td>
    <td>DO8~DO15</td>
    <td>DO16~DO23</td>
    <td>DO24~DO31</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">字节</td>
    <td>DOB0</td>
    <td>DOB1</td>
    <td>DOB2</td>
    <td>DOB3</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">字</td>
    <td colspan="2">DOW0</td>
    <td colspan="2">DOW2</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">长整形</td>
    <td colspan="4">DOL0</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">浮点数</td>
    <td colspan="4">DOF0</td>
    <td>...</td>
  </tr>
</tbody>
</table>

<br>


#### 系统继电器 (SW继电器)
##### Hi5a

在大多数情况下，每个监控项目都有一个固定的 SW 继电器索引地址。然而，在索引地址中，SW220-249 是用于 10 个多用途插槽的，可以在系统变量、主板存储空间、模拟输入/输出、日期/时间和 GE 变量的代码中，将所需的代码放入所需插槽进行监控。

- 大多数项目：固定区域
- 一些项目：可选项目区域 (插槽)

<br>

##### Hi6/Hi7

SB0-SB1999 区域是 [S Relay Fixed Area](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/en/3-relay/4-sw-relay/1-fixed-area?cont_model=${cont_model})，每个项目都有固定的索引地址，就像 Hi5a 一样。

然而，SB2000- 的区域是 [Optional items area](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/en/3-relay/4-sw-relay/README?cont_model=${cont_model})，大约有 900 个多用途插槽，允许通过插入所需项目的指令来使用它们。

几乎所有的项目都将通过可选项目区域进行监控。

- 大多数项目：可选项目区域 (插槽)
- 一些项目：固定区域