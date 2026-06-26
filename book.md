
[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - 嵌入式可编程逻辑控制器 (PLC)
[__SOURCE](0-about-this-manual/README.md)
# 关于手册
[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include file="zh/precautions.md" %}
[__SOURCE](0-about-this-manual/safety-notice.md)
# 安全注意事项

{% include file="zh/safety-notice.md" %}
[__SOURCE](1-intro/README.md)
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
[__SOURCE](1-intro/1-ladder-logic.md)
# 1.1 梯形逻辑

梯形逻辑，或称梯形图（LD），是嵌入式PLC的主要编程方法。[除了LD，还有其他方法，如结构化文本（ST）、功能块图（FBD）和顺序功能图（SFC），但嵌入式PLC不支持它们，因此不再进一步讨论。]

梯形程序之所以如此命名，是因为程序的结构类似梯子。信号在梯形结构中流动的水平连接线称为梯级，包含多个指令。

![](../_assets/ladder-sample2.png)

一个机器人教学项目可以包含一个或多个梯形图，每个图可能由十到几百个梯级组成。
当可编程逻辑控制器（PLC）切换到运行模式时，LD将被反复执行。完成一个周期所需的时间称为扫描时间，通常从几毫秒到几十毫秒不等。

<br>

指令由助记符组成，即指令的名称，以及操作数，即要传递给指令的参数。

 例如，下图中的添加（ADD (+)）指令配置如下。

![](../_assets/ladder-add.png)

* 助记符：ADD
* 操作数1：MW5
* 操作数2：DOW2
* 操作数3：MW6

<br>

嵌入式PLC的指令可以分为多个指令组，如下所述。由于每个指令将在第4节中进行解释，因此本节中的指令将作为理解梯形逻辑概念的示例进行解释。

---

<br>

### 接触指令

被分类为接触指令的检查是否关闭（XIC）是一个只有一个操作数的简单指令。该指令将在梯级上以标有-| |-符号的操作数表示。

![](../_assets/ladder-xic.png)

接触是一个开关，决定是否将应用于左侧的信号（1）沿梯级传递到右侧。如果继电器DO3的值为0（非活跃），则接触将处于开放状态，不会传递信号。如果DO3的值为1（活跃），则接触将关闭，允许信号传递。

![](../_assets/ladder-contact.png)

<br>

当多个XIC接触以串联或并联的形式相连时，可以创建逻辑运算表达式，例如AND、OR和NOT。
(![](../_assets/ladder-not.png)显示了一个反向（INV）指令，旨在将左侧的逻辑值的相反值传递到右侧，并且没有操作数。)

```
X1 AND (X2 OR (NOT X3))
```

![](../_assets/ladder-and-or-not.png)

<br>

### 输出线圈指令

输出使能（OTE）被分类为输出线圈指令。它总是放置在梯级的最右端，并由-( )-符号表示。该指令允许从左侧传递的值输出到操作数继电器。

如果上述逻辑运算表达式的结果输出到Y8继电器，则将以如下形式表示。

```
Y8 = X1 AND (X2 OR (NOT X3))
```

![](../_assets/ladder-ote.png)

<br>

### 功能指令

当左侧变为活跃时，将对给定的操作数执行特定操作。例如，在下图中，当DO3变为活跃时，将执行对MW5和DOW2继电器的值进行加法运算ADD (+)，然后将获得的和替换为MW6继电器。

```
IF DO3:
   MW6 = MW5 + DOW2
```

![](../_assets/ladder-add2.png)

比较指令也将操作结果传递到右侧。例如，在下图中，如果DO6变为活跃且MW8超过120，则Y20将被激活。

```
Y20 = DO6 AND (MW8 > 120)
```

![](../_assets/ladder-grt.png)
[__SOURCE](2-rc-setting/README.md)
# 2. 设置控制器
[__SOURCE](2-rc-setting/1-plc-mode-set.md)
# 2.1. 设置嵌入式PLC的模式

在“[F7: 条件设置] - PLC的操作模式”中，您可以选择关闭、停止、远程停止（R-Stop）、远程运行（R-Run）或运行（Run）模式之一作为嵌入式可编程逻辑控制器（PLC）的操作模式。  
R-Stop和R-Run分别表示远程停止和远程运行，每个状态表示可以通过以太网连接的PC的HRLadder远程更改模式的状态。

![Figure 2.1 设置嵌入式PLC的模式](../_assets/plc_run_mode.png)

<br>
<br>
根据所选模式，状态将在教学挂件的屏幕右上角以图标的形式显示。也就是说，当PLC=R-Run或PLC=Run时，将显示PLC图标，如上图所示；在PLC=Off的情况下，PLC图标将消失，如下图所示；在PLC=Stop的情况下，PLC图标上将显示红色禁止标志。

![Figure 2.2 嵌入式PLC在关闭状态](../_assets/plc_mode_off.png)

 
![Figure 2.3 嵌入式PLC在停止状态](../_assets/plc_mode_stop.png)


* Off  
嵌入式PLC的功能将被关闭。当这种情况发生时，机器人控制器的逻辑输出，FB0.DO0-FB9.DO959，将自动输出为物理输出（即旁路），FB0.Y0-FB9.Y959，物理输入，FB0.X0-FB9.X959，将自动输入为逻辑输入，FB0.DI0-FB9.DI595。

* R-Stop/Stop  
嵌入式PLC的操作将被停止。R-Stop表示可以从HRLadder进行更改的远程状态。如果设置为停止模式，则将无法从HRLadder更改操作模式。  
当嵌入式PLC被停止时，DI和Y继电器，即PLC输出信号，将自动变为0。*(DI是从机器人语言或指令的角度看是输入，但从嵌入式PLC的角度看是输出。)*  

* R-Run/Run  
嵌入式PLC将被执行。R-Run表示可以从HRLadder进行更改的远程状态。如果设置为运行模式，则将无法从HRLadder更改操作模式。  

[__SOURCE](2-rc-setting/2-tp-relay-mon.md)
# 2.2. 从控制器的教导示教器监控继电器状态

继电器状态可以通过输入 "[R2: 窗口调整] - [F1: 选择]" 来监控。

有关更多详细信息，请参阅 [${cont_model} 操作手册 - 6. 监控](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/ko-tp630/6-monitoring/README?cont_model=${cont_model})。
[__SOURCE](2-rc-setting/3-scan-time.md)
# 2.3. 扫描时间

嵌入式PLC中阶梯文件单次循环执行所需的时间将在HRLadder底部状态栏中显示为“扫描时间”。随着阶梯程序中步骤数量的增加，执行所需的时间也会增加，从而降低I/O响应速度。
[__SOURCE](3-relay/README.md)
# 3. 继电器
[__SOURCE](3-relay/1-relay-is.md)
# 3.1 继电器的意义

一种状态相当于开/关接触的设备，用于确定是否传输电信号，被称为开关。同时，继电器是一种可以自动操作的开关，它是通过电力而非手动进行操作的。

最初，继电器是一种使用线圈的磁力控制接触的物理设备。然而，在计算机化的可编程逻辑控制器（PLC）中，继电器是一个由软件控制的逻辑概念。从意义上讲，继电器被用作一种变量，它不仅可以存储由1位组成的开/关状态，还可以存储由多个位组成的字节、字、双字或实值。
[__SOURCE](3-relay/2-relay-expression.md)
# 3.2 指定继电器

以下显示了如何在 ${cont_model} 机器人控制器的嵌入式可编程逻辑控制器 (PLC) 中指定继电器。

`[FB{block-index}.]{relay-type}[{data-type}]{signal-index}`

例如，继电器可以如下指定。

Y1501  
FB3.DIW21

### block-index  
输入和输出继电器 (DI, DO, X, Y) 被分组为 10 个现场总线块，对象名称范围从 FB0 到 FB9。对于物理输入和输出，每个块将映射到每个现场总线设备。  
一个现场总线块的大小为 120 字节 (=960 位)。

您还可以将 FB 的某些区域映射到对象名称，从 FN0 到 FN63。  
请参见下面的链接以获取有关如何设置 FN 区域的说明。

[操作手册：7.3.2.12 fn 块分配](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/zh-tp630/7-system/3-control-parameter/2-io-signal-setting/12-fn-block?cont_model=${cont_model})

### relay-type  
有 12 种不同的类型，如下所示。  
每一种将在后面详细解释。

- 数字输入 (DI)：这是可以在 HRScript 中使用或用于分配各种输入的逻辑输入信号。
- 数字输出 (DO)：这是可以在 HRScript 中使用或用于分配各种输出的逻辑输出信号。
- 系统输入 (SI)：这是与公司的系统板接口的专用输入信号。
- 系统输出 (SO)：这是与公司的系统板接口的专用输出信号。
- X：这是通过现场总线设备从控制器外部输入的物理输入信号。
- Y：这是通过现场总线设备输出到控制器外部的物理输出信号。
- 内存 (M)：这可用于存储数据，并且可以从 HRScript 访问。
- 系统 (S)：这用于读取或写入控制器中的系统值。参见 [3.4 S 继电器](./4-sw-relay/README.md)。
- 辅助 (R)：这是用于临时存储的辅助继电器。
- 保持 (K)：这是用于临时存储的辅助继电器。即使断电值也会被存储。
- 定时器 (T)：用于定时器操作的继电器，当值为 0 时接点为打开。
- 计数器 (C)：用于计数器操作的继电器，当值为 0 时接点为打开。

<style type="text/css">
  .relay-table {
    border-collapse: collapse;
    /* width를 지정하지 않거나 auto로 두면 내용물에 폭이 딱 맞춰집니다 */
    width: auto; 
    font-family: sans-serif;
    font-size: 12px;
  }
  
  .relay-table th, 
  .relay-table td {
    border: 1px solid #a0a0a0;
    /* 상하 패딩 6px, 좌우 패딩 2px (완전 0보다 가독성을 위해 2px 추천) */
    padding: 6px 2px;
    text-align: center;
    /* 내용이 길어도 줄바꿈되지 않고 한 줄로 나오게 하여 폭을 압축 */
    white-space: nowrap; 
    font-size: 12px;
  }

  .relay-table th {
    background-color: #efefef;
    color: black;
    font-weight: bold;
  }

  /* 홀수 줄 배경색 (선택사항: 가독성 향상) */
  .relay-table tbody tr:nth-child(odd) {
    background-color: #ffffff;
  }
  .relay-table tbody tr:nth-child(even) {
    background-color: #f9f9f9;
  }
</style>

<table class="relay-table">
  <thead>
    <tr>
      <th>继电器<br>名称</th>      <th>点数</th>      <th>继电器 <br>(位)</th>      <th>继电器 <br>(字节)</th>      <th>继电器 <br>(字)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>DI</td>      <td>9600 位 (1200 字节)</td>      <td>FB0.DI0-FB9.DI959</td>      <td>FB0.DIB0 ~ FB9.DIB119</td>      <td>FB0.DIW0 ~ FB9.DIW118</td> 
    </tr>
    <tr>
      <td>DO</td>      <td>9600 位 (1200 字节)</td>      <td>FB0.DO0-FB9.DO959</td>      <td>FB0.DOB0 ~ FB9.DOB119</td>      <td>FB0.DOW0 ~ FB9.DOW118</td>
    </tr>
    <tr>
      <td>SI</td>      <td>960 位 (120 字节)</td>      <td>SI0-SI959</td>      <td>SIB0 ~ SIB119</td>      <td>SIW0 ~ SIW118</td>
    </tr>
    <tr>
      <td>SO</td>      <td>960 位 (120 字节)</td>      <td>SO0-SO959</td>      <td>SOB0 ~ SOB119</td>      <td>SOW0 ~ SOW118</td>
    </tr>
    <tr>
      <td>X</td>      <td>9600 位 (1200 字节)</td>      <td>FB0.X0-FB9.X959</td>      <td>FB0.XB0 ~ FB9.XB119</td>      <td>FB0.XW0 ~ FB9.XW118</td>
      </tr>      
    <tr>
      <td>Y</td>      <td>9600 位 (1200 字节)</td>      <td>FB0.Y0-FB9.Y959</td>      <td>FB0.YB0 ~ FB9.YB119</td>      <td>FB0.YW0 ~ FB9.YW118</td>
    </tr>
    <tr>
      <td>M</td>      <td>160000 位 (20000 字节)</td>      <td>M0-M159999</td>      <td>MB0-MB19999</td>      <td>MW0 ~ MW19998</td>
    </tr>
    <tr>
      <td>S</td>      <td>160000 位 (20000 字节)</td>      <td>S0-S159999</td>      <td>SB0-SB19999</td>      <td>SW0 ~ SW19998</td>
    </tr>
    <tr>
      <td>R</td>      <td>1024 位 (128 字节)</td>      <td>R0-R1023</td>      <td>RB0 ~ RB127</td>      <td>RW0 ~ RW126</td>
    </tr>
    <tr>
      <td>K</td>      <td>1024 位 (128 字节)</td>      <td>K0-K1023</td>      <td>KB0 ~ KB127</td>      <td>KW0 ~ KW126</td>
    </tr>
    <tr>
      <td>T</td>      <td>256 DWORD (1024 字节)</td>      <td>T0-T255</td>      <td>-</td>      <td>-</td>
    </tr>
    <tr>
      <td>C</td>      <td>256 DWORD (1024 字节)</td>      <td>C0-C255</td>      <td>-</td>      <td>-</td>
    </tr>
  </tbody>
</table>

<div class="page-break"></div>

### data-type  
有五种不同的类型，如下所示。

* 无指定：位，1 位
* B：有符号字节，8 位
* W：有符号字，16 位
* L：有符号长，32 位
* F：浮点实数，32 位

<br>  
它们只是表示相同内存空间的不同数据类型，而不是单独的内存空间。例如，DO[0-15]、DOB[0-1]和DOW[0]都是相同的输出信号。

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
    <td class="tg-kftd">长</td>
    <td colspan="4">DOL0</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">浮点</td>
    <td colspan="4">DOF0</td>
    <td>...</td>
  </tr>
</tbody>
</table>

<div class="page-break"></div>

### signal-index

这是继电器类型内的基于 0 的索引。DO 的索引以位为单位给出，而 DOB、DOW、DOL 和 DOF 的索引以字节为单位给出。

<br>
<br>

字段总线对象名称可以部分跳过，如下所示。例如，DO961 与 FB1.DO1 具有相同的指定。

| **对象名称** | **DO 指定** | **FB.DO 指定** |
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

DI 和 DO 分别是逻辑输入和输出，可以通过机器人语言和 I/O 分配访问。
[__SOURCE](3-relay/3-io/README.md)
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
[__SOURCE](3-relay/3-io/1-so.md)
# 3.3.1 SO - 系统输出

<style type="text/css">
table  {border-collapse:collapse;}
td {
    border-color:gray;
    border-style:solid;
    border-width:1px;
    padding: 1px 4px;
    height: auto !important;
}
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
	<tr>
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
		<td>接收到系统错误</td>
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
	</tr>
	<tr>
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
	</tr>
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
		<td>so112</td>
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
		<td>刹车控制 3</td>
	</tr>
	<tr>
		<td>so131</td>
		<td>刹车控制 4</td>
	</tr>
	<tr>
		<td>so132</td>
		<td>刹车控制 5</td>
	</tr>
	<tr>
		<td>so133</td>
		<td>刹车控制 6</td>
	</tr>
	<tr>
		<td>so134</td>
		<td>刹车控制 7</td>
	</tr>
	<tr>
		<td>so135</td>
		<td>刹车控制 8</td>
	</tr>
	<tr>
		<td rowspan=2>sob17</td>
		<td>so138</td>
		<td>动态刹车</td>
	</tr>
	<tr>
		<td>so139</td>
		<td>动态刹车模式</td>
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
		<td>ch1 - 脉冲计数类型 (0=上升, 1=上升/下降)</td>
	</tr>
	<tr>
		<td>so161</td>
		<td>ch1- 通讯类型 (0=线路驱动, 1=开漏)</td>
	</tr>
	<tr>
		<td>so162</td>
		<td>ch2 - 脉冲计数类型 (0=上升, 1=上升/下降)</td>
	</tr>
	<tr>
		<td>so163</td>
		<td>ch2- 通讯类型 (0=线路驱动, 1=开漏)</td>
	</tr>
</tbody>

</table>

<div class="page-break"></div>
[__SOURCE](3-relay/3-io/2-si.md)
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
		<td>升降轴/臂限制</td>
	</tr>
	<tr>
		<td>si1</td>
		<td>主轴限制</td>
	</tr>
	<tr>
		<td>si2</td>
		<td>附加轴限制</td>
	</tr>
	<tr>
		<td>si3</td>
		<td>外部轴限制</td>
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
		<td>紧急停止 (外部)</td>
	</tr>
	<tr>
		<td>si7</td>
		<td>安全链</td>
	</tr>
	<tr>
		<td rowspan=7>sib1</td>
		<td>si8</td>
		<td>模式开关 (自动)</td>
	</tr>
	<tr>
		<td>si9</td>
		<td>模式开关 (手动)</td>
	</tr>
	<tr>
		<td>si10</td>
		<td>模式开关 (远程)</td>
	</tr>	
	<tr>
		<td>si11</td>
		<td>TP使能开关</td>
	</tr>	
	<tr>
		<td>si12</td>
		<td>安全防护 (自动)</td>
	</tr>	
	<tr>
		<td>si13</td>
		<td>安全防护 (自动外部)</td>
	</tr>	
	<tr>
		<td>si14</td>
		<td>安全防护 (通用)</td>
	</tr>	
	<tr>
		<td rowspan=8>sib2</td>
		<td>si16</td>
		<td>预充电</td>
	</tr>
	<tr>
		<td>si17</td>
		<td>电动机电源</td>
	</tr>
	<tr>
		<td>si18</td>
		<td>放电</td>
	</tr>	
	<tr>
		<td>si19</td>
		<td>电动机开启 (TP)</td>
	</tr>	
	<tr>
		<td>si20</td>
		<td>启动 (TP)</td>
	</tr>	
	<tr>
		<td>si21</td>
		<td>停止 (TP)</td>
	</tr>	
	<tr>
		<td>si22</td>
		<td>OP已安装</td>
	</tr>	
	<tr>
		<td>si23</td>
		<td>电动机开启(外部)</td>
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
	<tr>
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
		<td>过压</td>
	</tr>
	<tr>
		<td>si43</td>
		<td>欠压</td>
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
	<tr>
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
		<td>刹车电源故障</td>
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
		<td>刹车状态 1</td>
	</tr>
	<tr>
		<td>si65</td>
		<td>刹车状态 2</td>
	</tr>
	<tr>
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
		<td>过压</td>
	</tr>
	<tr>
		<td>si75</td>
		<td>欠压</td>
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
		<td>预充电继电器开启</td>
	</tr>
	<tr>
		<td>si105</td>
		<td>动态电阻过热</td>
	</tr>
	<tr>
		<td>si106</td>
		<td>过压</td>
	</tr>
	<tr>
		<td>si107</td>
		<td>欠压</td>
	</tr>
	<tr>
		<td>si108</td>
		<td>动态刹车状态</td>
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
	</tr>
	<tr>
		<td rowspan=2>sib15</td>
		<td>si120</td>
		<td>刹车电源故障</td>
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
		<td>刹车状态 1</td>
	</tr>
	<tr>
		<td>si129</td>
		<td>刹车状态 2</td>
	</tr>
	<tr>
		<td>si130</td>
		<td>刹车状态 3</td>
	</tr>
	<tr>
		<td>si131</td>
		<td>刹车状态 4</td>
	</tr>
	<tr>
		<td>si132</td>
		<td>刹车状态 5</td>
	</tr>
	<tr>
		<td>si133</td>
		<td>刹车状态 6</td>
	</tr>
	<tr>
		<td>si134</td>
		<td>刹车状态 7</td>
	</tr>
	<tr>
		<td>si135</td>
		<td>刹车状态 8</td>
	</tr>
	<tr>
		<td rowspan=8>sib17</td>
		<td>si136</td>
		<td>预充电继电器开启</td>
	</tr>
	<tr>
		<td>si137</td>
		<td>动态电阻过热</td>
	</tr>
	<tr>
		<td>si138</td>
		<td>过压</td>
	</tr>
	<tr>
		<td>si139</td>
		<td>欠压</td>
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
		<td>用户 5 (BD640T)</td>
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
		<td>ch1 - 脉冲计数器 (16位)</td>
	</tr>
	<tr>
		<td rowspan=1>sib44<br>sib45</td>
		<td></td>
		<td>ch2 - 脉冲计数器 (16位)</td>
	</tr>
	<tr>
		<td rowspan=4>sib46</td>
		<td>si368</td>
		<td>ch1- 线路错误</td>
	</tr>
	<tr>
		<td>si369</td>
		<td>ch1- 限位开关</td>
	</tr>
	<tr>
		<td>si370</td>
		<td>ch2- 线路错误</td>
	</tr>
	<tr>
		<td>si371</td>
		<td>ch2- 限位开关</td>
	</tr>
</tbody>

</table>
[__SOURCE](3-relay/4-sw-relay/README.md)
# 3.4 S 继电器

在 ${cont_model} 控制器中，各种状态的值映射到 S 继电器。通过向某些 S 继电器写入值，也可以改变 ${cont_model} 的状态。

因此，可以通过例如过程可编程逻辑控制器 (PLC) 或个人计算机 (PC) 的外部设备，通过现场总线、Modbus 等读取 S 继电器的值来远程监控 ${cont_model} 控制器的状态，并通过向 S 继电器写入值来远程控制 ${cont_model} 控制器。

S 继电器的区域可大致分为两个部分，如下所示。

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
		<td>可选项目区域 (插槽)</td>
	</tr>
</table>

<br>

### 固定区域
经常使用的基本项目分配到预定的地址。无法通过设置更改或分配项目。固定区域的映射将在下一节中描述。

<br>

### 可选项目区域
该区域由 900 个插槽组成，每个插槽 20 字节。每个插槽的配置将由要放入前导字的命令值决定。每个命令的映射将在以下部分中描述。

<div class="page-break"></div>

<table class="tg">
<thead>
	<tr>
		<th>插槽索引</th>
		<th>s 索引:偏移</th>
		<th>字段</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td rowspan=10>插槽 0</td>
		<td>2000:0</td>
		<td>命令 (惯例：获取为偶数，设置为奇数)</td>
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
		<td rowspan=3>插槽 899</td>
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
# 3.4.1 S relay - 固定区域

请参阅下面显示的表格，了解 SB0-SB1999 区域的固定项。

<style type="text/css">
table  {border-collapse:collapse;}
td {
    border-color:gray;
    border-style:solid;
    border-width:1px;
    padding: 1px 4px;
    height: auto !important;
}
.grayed {background-color:lightgray;}
</style>

<div class="page-break"></div>

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
		<td>如果在操作中发生进位，则开启</td>
		<td>如果 BCD 操作不可行，则开启</td>
		<td>1 秒时钟</td>
		<td>0.2 秒时钟</td>
		<td>0.1 秒时钟</td>
		<td>仅在一次扫描中开启</td>
		<td>始终关闭</td>
		<td>始终开启</td>		
		<td></td>
	</tr>
	<tr>
		<td>SB1</td>
		<td class='grayed'></td>
		<td>当标签为 0 或以下，或跳转的标签不存在时开启</td>
		<td>如果标签重复，则开启</td>
		<td>如果标签数量超过 100，则开启</td>
		<td>如果标签不是常量，则开启</td>
		<td class='grayed'></td>
		<td>4 秒时钟</td>
		<td>2 秒时钟</td>
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
		<td>如果没有子梯级被调用，则开启</td>
		<td>当扫描时间超过 5 秒时开启</td>
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
		<td>T/P 启动完成</td>
		<td></td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

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
		<td>PLC 执行模式</td>
		<td>0=停止, 1=R.停止, 2=R.运行,<br>
		 3= 运行, 4=关闭, 5=无程序</td>
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
		<td>软件版本：第一</td>
		<td>例如，在 V60.05-08 的情况下，60</td>
	</tr>
	<tr>
		<td>SB15</td>
		<td>软件版本：第二</td>
		<td>例如，在 V60.05-08 的情况下，5</td>
	</tr>
	<tr>
		<td>SB16</td>
		<td>软件版本：小修正</td>
		<td>例如，在 V60.05-08 的情况下，8</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW18</td>
		<td>扫描时间</td>
		<td>毫秒</td>
	</tr>
	<tr>
		<td>SW20</td>
		<td>赋值时间</td>
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
		<td>梯形图中的总步数</td>
		<td></td>
	</tr>
	<tr>
		<td>SW28</td>
		<td>占用比率</td>
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
		<td>当前用户坐标编号</td>
		<td></td>
	</tr>
	<tr>
		<td>SB40</td>
		<td>当前工具编号</td>
		<td></td>
	</tr>
	<tr>
		<td>SB41</td>
		<td>机器人状态</td>
		<td>0=停止, 1=运行, 2=等待</td>
	</tr>
	<tr>
		<td>SB42</td>
		<td>播放速度</td>
		<td>%</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW44</td>
		<td>步进前进/后退最大速度</td>
		<td>毫米/秒</td>
	</tr>
	<tr>
		<td>SW46</td>
		<td>工具尖端移动速度</td>
		<td>毫米/秒</td>
	</tr>
	<tr>
		<td>SW48</td>
		<td>错误/警告编号</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
</tbody>
</table>

<div class="page-break"></div>

<table class="tg">
<tbody>
	<tr>
		<td>SW50</td>
		<td>错误/警告辅助信息</td>
		<td></td>
	</tr>
	<tr>
		<td>SW62</td>
		<td>间接地址指定（继电器-2）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW64</td>
		<td>间接地址指定（继电器-4）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW66</td>
		<td>间接地址指定（继电器-6）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW68</td>
		<td>间接地址指定（继电器-8）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW70</td>
		<td>间接地址指定（继电器-10）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW72</td>
		<td>间接地址指定（继电器-12）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW74</td>
		<td>间接地址指定（继电器-14）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW76</td>
		<td>间接地址指定（继电器-16）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW78</td>
		<td>间接地址指定（继电器-18）</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB88</br>
		...</br>
		SB99</td>
		<td>教示器键输入状态</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
		<tr>
		<td>SB111</td>
		<td>运行时间选择</td>
		<td>1=总计（初始化后），<br>
		2=总计（通电后），<br>
		3=最后一个周期，<br>
		4=当前周期
			</td>
	</tr>
	<tr>
		<td>SL112</td>
		<td>电机开启（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL116</td>
		<td>电机开启（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL120</td>
		<td>运行时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL124</td>
		<td>运行时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL128</td>
		<td>移动时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL132</td>
		<td>移动时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL136</td>
		<td>周期计数</td>
		<td></td>
	</tr>
	<tr>
		<td>SL140</td>
		<td>等待，DI 等待时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL144</td>
		<td>等待，DI 等待时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL148</td>
		<td>延迟等待时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL152</td>
		<td>延迟等待时间（毫秒）</td>
		<td></td>
	</tr>
	</tbody>
</table>

<div class="page-break"></div>

<table class="tg">
<tbody>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB159</td>
		<td>轴信息选择</td>
		<td>1 = 当前位置信息 
		<br>(轴角度)，<br>
		2 = 当前位置信息 
		<br>(基坐标)，<br>
		3 = 当前位置信息 
		<br>(基/用户坐标)<br>
		6 = 轴速度,<br>
		7 = 电机速度<br>
		8 = 电机速度指令 <br>
		在速度控制时（rpm）<br>
		10 = 负载因子(I/Ir)，<br>
		11 = 负载因子(I/Ip)，<br>
		13 = 负载因子（连续）<br>
		15 = 编码器温度<br>
		18 = 累积距离<br>
		每个轴<br>
		111 = 位置偏差<br>
		（当前），<br>
		112 = 位置偏差<br>
		（最大）<br>
		124 = 编码器通信故障计数</td>
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
		<tr>
		<td>SL200</td>
		<td>每个轴的控制状态<br>
		（0=关闭, 1=开启）</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	</tbody>
</table>

<div class="page-break"></div>

<table class="tg">
<tbody>
	<tr>
		<td>SW210</br>
		...</br>
		SW280</td>
		<td>程序编号
		<td>（主任务 = sw210,<br>
		子任务 1 = sw220,<br>
		子任务 2 = sw230,<br> 
		子任务 3 = sw240,<br>
		子任务 4 = sw250,<br>
		子任务 5 = sw260,<br>
		子任务 6 = sw270,<br>
		子任务 7 = sw280）</td>
	</tr>
	<tr>
		<td>SW212</br>
		...</br>
		SW282</td>
		<td>步骤编号</td>
		<td>（主任务 = sw212,<br>
		子任务 1 = sw222,<br>
		子任务 2 = sw232,<br>
		子任务 3 = sw242,<br>
		子任务 4 = sw252,<br>
		子任务 5 = sw262,<br>
		子任务 6 = sw272,<br>
		子任务 7 = sw282）</td></td>
	</tr>
	<tr>
		<td>SW214</br>
		...</br>
		SW284</td>
		<td>功能编号</td>
		<td>（主任务 = sw214,<br>
		子任务 1 = sw224,<br>
		 子任务 2 = sw234,<br>
		 子任务 3 = sw244,<br>
		子任务 4 = sw254,<br>
		子任务 5 = sw264,<br>
		子任务 6 = sw274,<br>
		子任务 7 = sw284）</td>
	</tr>
	<tr>
		<td>SW216</br>
		...</br>
		SW286</td>
		<td>主程序编号</td>
		<td>（主任务 = sw216,<br>
		子任务 1 = sw226,<br>
		 子任务 2 = sw236,<br>
		 子任务 3 = sw246,<br>
		子任务 4 = sw256,<br>
		子任务 5 = sw266,<br>
		子任务 6 = sw276,<br>
		子任务 7 = sw286）</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW500</td>
		<td>枪的编号</td>
		<td>0=当前选择的枪,<br>
		1-16</td>
	</tr>
	<tr>
		<td>SW502</td>
		<td>枪搜索状态</td>
		<td>1=完成, 0=未完成</td>
	</tr>
	<tr>
		<td>SW504</td>
		<td>移动电极<br>
		磨损量 x 100</td>
		<td></td>
	</tr>
	<tr>
		<td>SW506</td>
		<td>固定电极<br>
		磨损量 x 100</td>
		<td></td>
	</tr>
	<tr>
		<td>SW508</td>
		<td>加压力<br>
		指令值 x 10</td>
		<td></td>
	</tr>
	<tr>
		<td>SW510</td>
		<td>加压力<br>
		当前值 x 10</td>
		<td></td>
	</tr>
</tbody>
</table>
</tbody>
</table>

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/2-slot-task-info.md)
# 3.4.2 S relay - TASK_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>获取任务信息 (100)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
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
# 3.4.3 S relay - OP_TIME

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_OP_TIME (110)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
		<td>时间基准<br>1=自初始化以来, 2=自开机以来, 3=自上一个循环以来, 4=当前循环</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>param. 3</td>
		<td>项目<br>1=电机开启, 2=运行时间, 3=移动时间, 4=等待时间, 5=延迟时间, 11=点焊时间 (焊接机 1), 12=(焊接机 2), 13=(焊接机 3), 14=(焊接机 4)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>result</td>
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

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/4-slot-axis-info.md)
# 3.4.4 S relay - AXIS_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_AXIS_INFO (120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>类型<br>
		1 = 当前位置信息（轴角），2 = 当前位置信息（基坐标），3 = 当前位置信息（基/用户坐标）<br>
		6 = 轴速度，7 = 马达速度<br>
		8 = 当速度控制时的马达速度命令（rpm）<br>
		10 = 负载因子(I/Ir)，11 = 负载因子(I/Ip)，13 = 负载因子（持续）<br>
		15 = 编码器温度<br>
		18 = 每个轴的累计距离<br>
		111 = 位置偏差（当前），112 = 位置偏差（最大）<br>
		124 = 编码器通信失败计数<br>
	    </td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
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
		<td rowspan=3>result</td>
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

<div class="page-break"></div>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>SET_AXIS_INFO (121)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>类型<br>8 = 当速度控制时的马达速度命令（rpm）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
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
		<td rowspan=3>result</td>
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

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/5-slot-tp-keypad.md)
# 3.4.5 S 继电器 - TP_KEYPAD

Supported from V60.30-07

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
		<th>7</th>
		<th>6</th>
		<th>5</th>
		<th>4</th>
		<th>3</th>
		<th>2</th>
		<th>1</th>
		<th>0</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
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
		<td class='jog'>Step<br>FWD</td>
		<td class='jog'>Step<br>BWD</td>
		<td>u1</td>
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
		<td class='opkey'>mode2</td>
		<td class='opkey'>mode1</td>
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
		<td class='ent'>ENTER</td>
		<td class='ent'>ESC</td>
		<td class='num'>9</td>
		<td class='num'>8</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>[7]</td>
		<td class='spkey'>速度<br>.低</td>
		<td class='spkey'>速度<br>.高</td>
		<td class='spkey'>REC</td>
		<td class='spkey'>步骤</td>
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

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/6-slot-tp-app.md)
# 3.4.6 S relay - TP_APP

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GETSET_TP_APP (140)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>get</td>
		<td>当前教导挂件应用程序的快捷键编号（1-9）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>set</td>
		<td>需要读取或控制的教导挂件目标应用程序的快捷键编号（1-9）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>get</td>
		<td>教导挂件目标应用程序的当前状态值<br>(-1=无操作, 0=未执行, 1=已激活, 2=已停用)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>set</td>
		<td>对教导挂件目标应用程序的控制<br>
(0: 无操作, 1: 已激活, 2: 已停用, 8: 已执行, 9: 强制结束)<br>
* 每次值变化时将执行一次。</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/7-slot-date-time.md)
# 3.4.7 S relay - DATE_TIME

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
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
		<td>年份 (例如: 2022)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>月份 (1-12)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>日期 (1-31)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>小时 (0-23)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>分钟 (0-59)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>秒 (0-59)</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/8-slot-cur-spotgun-no.md)
# 3.4.8 S relay - CUR_SPOTGUN_NO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_CUR_SPOTGUN_NO (2000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=12>result</td>
		<td>当前喷枪号码 (主喷枪)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>当前条件号码 (主条件)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>7</td>
		<td>当前序列号码 (主序列)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>当前喷枪号码 (从喷枪 #1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>当前条件号码 (从条件 #1)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>11</td>
		<td>当前序列号码 (从序列 #1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>12</td>
		<td>当前喷枪号码 (从喷枪 #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>13</td>
		<td>当前条件号码 (从条件 #2)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>15</td>
		<td>当前序列号码 (从序列 #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>16</td>
		<td>当前喷枪号码 (从喷枪 #3)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>17</td>
		<td>当前条件号码 (从条件 #3)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>19</td>
		<td>当前序列号码 (从序列 #3)</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_SPOTWELD_INFO (2010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 2</td>
		<td>枪编号 (1-4)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td rowspan=5>result</td>
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
		<td>固定电极消耗量 x 10</td>
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
</table>

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/10-slot-arcweld-info.md)
# 3.4.10 S realy - ARCWELD_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {
    border-color:gray;
    border-style:solid;
    border-width:1px;
    padding: 1px 4px;
    height: auto !important;
}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_ARCTWELD_INFO (3000) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
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
		<td>焊机错误</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>送丝速度</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
从 V60.32-00 开始支持以下服务。
<br>
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_ARCTWELD_INFO (3001) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>馈送电机电流</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>接缝跟踪数据</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>焊接工艺</td>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_ARCTWELD_INFO (3002) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>焊机总操作时间(秒)</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊机固件版本 - 低位(Vx.x.255)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>焊机固件版本 - 中位(Vx.255.x)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>焊机固件版本 - 高位(V255.x.x)</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_ARCTWELD_INFO (3004) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>
			0x01 = WCR(焊丝接触继电器) <br>
			0x02 = 火炬碰撞 <br>
			0x04 = 电源正常 <br>
			0x08 = 焊丝卡住 <br>
			0x10 = 焊机错误 <br>
			0x20 = 工艺激活 <br>
			0x40 = 通信准备就绪 <br>
			0x80 = 焊丝使用可能 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 火炬状态 <br>
			0x02 = 逐步状态 <br>
			0x04 = 收回状态 <br>
			0x08 = 气体检查 <br>
			0x10 = 协调可用 <br>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_ARCTWELD_INFO (3005) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
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
		<td>作业/程序号</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>操作模式</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>协调代码</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_ARCTWELD_INFO (3006) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>脉冲动态补偿</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊丝回缩</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>工艺控制</td>
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
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_ARCTWELD_INFO (3007) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>焊丝材料</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>焊丝直径</td>
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
		<td>双运作模式</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_ARCTWELD_INFO (3009) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>
			0x01 = 弧开启 <br>
			0x02 = 机器人准备就绪 <br>
			0x04 = 主火炬选择 <br>
			0x08 = 气体开启 <br>
			0x10 = 焊丝进给 <br>
			0x20 = 焊丝收回 <br>
			0x40 = 焊机错误复位 <br>
			0x80 = 焊丝卡住检查 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 焊接仿真 <br>
			0x02 = 引弧<br>
			0x04 = 提升弧使用 <br>
			0x08 = 超脉冲使用 <br>
			0x10 = 在线状态 <br>
			0x20 = 作业模式激活 <br>
			0x40 = 电压设置模式 <br>
			0x80 = 电流设置模式 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>
			0x01 = 机器人火炬碰撞 <br>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_ARCTWELD_INFO (3010) - 状态</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>当前电弧控制编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>当前接触感应编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>当前编织控制编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>当前LVS控制编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>当前弧控制编号。</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/11-slot-conveyor-info.md)
# 3.4.11 S relay - CONVEYOR_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>获取输送带信息 (4000)</td>
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
		<td rowspan=7>result</td>
		<td>输送带脉冲</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>工件位置</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>输送带速度</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>工件数量</td>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>获取输送带信息_LIN (4010)</td>
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
		<td rowspan=2>result</td>
		<td>线性输送带水平角度</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>线性输送带垂直角度</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>获取输送带信息_CIR (4020)</td>
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
		<td rowspan=2>result</td>
		<td>圆形输送带角度 (X 轴)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>圆形输送带角度 (Y 轴)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>获取输送带信息_CIR2 (4040)</td>
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
		<td rowspan=3>result</td>
		<td>圆形输送带中心 (X)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>圆形输送带中心 (Y)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>圆形输送带中心 (Z)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/12-slot-sys-var.md)
# 3.4.12 S realy - SYSTEM_VARIABLE

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>


### 获取和设置系统变量

{% hint style="info" %}
在版本低于 V70.00-00 的情况下，要设置系统变量，请检查命令是否已更改并操作。 <br>
换句话说，当命令值更改为 161 时，它将立即运行。  

{% endhint %}

#### 获取系统变量
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_SYS_VAR (160)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>项（设置数据的）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4 ~ 18</td>
		<td>param n</td>
		<td>获取值</td>
		<td></td>
	</tr>
</tbody>
</table>
<br>

#### 设置系统变量
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>SET_SYS_VAR (161)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>项（设置数据的）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4 ~ 18</td>
		<td>param n</td>
		<td>设置值</td>
		<td></td>
	</tr>
</tbody>
</table>
<br>
<br>

#### <mark style="color:green;">播放速度</mark>
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>42 = 播放速度</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 1</td>
		<td>值</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
信息） <br>
- 在版本低于 V70.00-00 的情况下不支持获取。 <br>
<br>

#### <mark style="color:green;">当前工具编号</mark>
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>40 = 工具编号</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 1</td>
		<td>值</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
信息） <br>
- 在版本低于 V70.00-00 的情况下不支持获取。 <br>
<br>

#### <mark style="color:green;">步进前进/后退最大速度</mark>
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>44 = 步进前进/后退最大速度</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 1</td>
		<td>值</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
信息） <br>
- 在版本低于 V70.00-00 的情况下不支持获取。 <br>
- 在版本低于 V60.32-07 的情况下不支持设置。 <br>
<br>

<div class="page-break"></div>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>获取硬件信息 (170)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td rowspan=6>result</td>
		<td>cpu 温度 * 10</td>
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

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/README.md)
# 3.4.14 S relay - CIFX PCI Communication

#### CIFX PCI Communication Common Relay
* command 1000: 通用状态
* command 1001: 通用控制

<br>

#### CIFX PCI Communication Protocol Relay
* command 1010: Profibus-DP 主站
* command 1012: DeviceNet 主站
* command 1014: EtherNet/IP 主站
* command 1016: Profinet IO 主站
* command 1018: EtherCAT 主站

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/1-slot-common-info.md)
# 3.4.14.1 S relay - CIFX PCI Communication Status

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<br>

### CIFX PCI Common Status

<br>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>状态 1 = 1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>4</td>
		<td>通道状态</td>
		<td class='grayed'></td>
		<td>重启所需启用</td>
		<td>重启所需</td>
		<td>配置新</td>
		<td>配置锁</td>
		<td>总线开启</td>
		<td>运行</td>
		<td>准备好</td>
	</tr>
	<tr>
		<td>8</td>
		<td>4</td>
		<td>通信状态</td>
		<td colspan=8>0 = 未知, <br> 1 =  未配置, <br> 2 = 停止, <br> 3 = 空闲, <br> 4 = 工作</td>
	</tr>
	<tr>
		<td>12</td>
		<td>4</td>
		<td>通信错误代码</td>
		<td colspan=8>0 = 无错误, <br> 非零 =  错误代码 (32位十六进制)</td>
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


<div class="page-break"></div>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
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
		<td colspan=8></td>
	</tr>
</tbody>
</table>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
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

<div class="page-break"></div>

### CIFX PCI Master Only

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>状态 4 = 4</td>
	</tr>
	<tr>
		<td>4</td>
		<td>4</td>
		<td>从状态</td>
		<td colspan=8>0 = 未知, <br> 1 = OK, <br> 2 = 失败</td>
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
		<td>已配置从设备数量</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>16</td>
		<td>4</td>
		<td>活动从设备数量</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
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

<div class="page-break"></div>
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
		<td colspan=8>插槽编号 = 1 ~ 3</td>
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
		<td colspan=8>当信号变化为 0 -> 1 时重置</td>
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
</table>

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/3-slot-profibus-dp-info.md)
# 3.4.14.3 S relay - Profibus-DP Master 状态

<style>
.my-custom-table table  {border-collapse:collapse;}
.my-custom-table td {border-color:gray;border-style:solid;border-width:1px;font-size: 11px}
.my-custom-table th:nth-child(1)
{
    width: 2%;
} 
.my-custom-table th:nth-child(2)
{
    width: 3%;
} 
.relay-table td:nth-child(1) {
    width: 1%;
}
.relay-table td:nth-child(2) {
    width: 1%;
}
.relay-table td:nth-child(3) {
    width: 3%;
}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<br>

<table class="my-custom-table">
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
		<td>1</td>
		<td>全局位 <br> (Profibus 主站)</td>
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
		<td>主状态</td>
		<td colspan=8>0x00 = 离线， <br> 0x40 = 停止， <br> 0x80 = 清除， <br> 0xC0 = 操作</td>
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
</table>

	
<br>

{% hint style="info" %}
如果您想监控从站是否处于活动状态，请检查“IO 交换中的从站列表”。
{% endhint %}

<div class="page-break"></div>

<table class="my-custom-table">
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>已配置从站列表 = 2</td>
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

<div class="page-break"></div>


<table class="my-custom-table">
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>IO 交换中的从站列表 = 3</td>
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

<div class="page-break"></div>

<table class="my-custom-table">
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
<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>配置从设备列表 = 5</td>
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

<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
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

<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
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
<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/4-slot-devicenet-info.md)
# 3.4.14.4 S relay - DeviceNet Master Status

<style>
.my-custom-table table  {border-collapse:collapse;}
.my-custom-table td {border-color:gray;border-style:solid;border-width:1px;font-size: 11px}
.my-custom-table th:nth-child(1)
{
    width: 2%;
} 
.my-custom-table th:nth-child(2)
{
    width: 3%;
} 
.relay-table td:nth-child(1) {
    width: 1%;
}
.relay-table td:nth-child(2) {
    width: 1%;
}
.relay-table td:nth-child(3) {
    width: 3%;
}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
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
		<td>参数 1</td>
		<td colspan=8>插槽号码 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>状态 = 1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>1</td>
		<td>全局位 <br> (Profibus 主站)</td>
		<td>检查重复的 MAC ID</td>
		<td>重复的 MAC ID</td>
		<td>主机未就绪</td>
		<td>总线事件错误</td>
		<td>致命错误</td>
		<td>非交换错误</td>
		<td>自动清除错误</td>
		<td>控制错误</td>
	</tr>
	<tr>
		<td>5</td>
		<td>1</td>
		<td>主状态</td>
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
		<td colspan=8>仅限 DeviceNet 主站 <br> 52 = 未知过程数据握手模式, <br> 53 = 波特率错误, <br> 54 = MAC ID 错误, <br> 57 = 重复的 MAC ID, <br> 58 = 没有设备, <br> 210 = 没有配置, <br> 212 = 读取配置失败, <br> 220 = 用户看门狗失败, <br> 221 = 用户数据无响应, <br> 223 = 主控停止 (CAN 总线关闭), <br> 226 = 该设备不是主站</td>
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
\.		如果您想监控从站是否处于活动状态，请查看“IO 交换中的从站列表”。
{% endhint %}

<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
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
		<td>参数 1</td>
		<td colspan=8>插槽号码 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>激活 / 未激活的从站列表 = 2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>激活的从站列表</td>
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
		<td rowspan=8>8</td>
		<td rowspan=8>未激活的从站列表</td>
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

<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
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
		<td>参数 1</td>
		<td colspan=8>插槽号码 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>从站列表 (显式消息 / IO 交换) = 3</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>激活的显式消息从站列表</td>
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
		<td rowspan=8>8</td>
		<td rowspan=8>IO 交换中的从站列表</td>
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


<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
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
		<td>参数 1</td>
		<td colspan=8>插槽号码 = 1 ~ 3</td>
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
<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>描述或比特索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>比特 7</td>
		<td class='powderblued'>比特 6</td>
		<td class='powderblued'>比特 5</td>
		<td class='powderblued'>比特 4</td>
		<td class='powderblued'>比特 3</td>
		<td class='powderblued'>比特 2</td>
		<td class='powderblued'>比特 1</td>
		<td class='powderblued'>比特 0</td>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>已配置从设备列表 = 5</td>
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


<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>描述或比特索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>比特 7</td>
		<td class='powderblued'>比特 6</td>
		<td class='powderblued'>比特 5</td>
		<td class='powderblued'>比特 4</td>
		<td class='powderblued'>比特 3</td>
		<td class='powderblued'>比特 2</td>
		<td class='powderblued'>比特 1</td>
		<td class='powderblued'>比特 0</td>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>已激活从设备列表 = 6</td>
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


<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>描述或比特索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>比特 7</td>
		<td class='powderblued'>比特 6</td>
		<td class='powderblued'>比特 5</td>
		<td class='powderblued'>比特 4</td>
		<td class='powderblued'>比特 3</td>
		<td class='powderblued'>比特 2</td>
		<td class='powderblued'>比特 1</td>
		<td class='powderblued'>比特 0</td>
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
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
# 3.4.14.5 S relay - EtherNet/IP Master Status

<style>
.my-custom-table table  {border-collapse:collapse;}
.my-custom-table td {border-color:gray;border-style:solid;border-width:1px;font-size: 11px}
.my-custom-table th:nth-child(1)
{
    width: 2%;
} 
.my-custom-table th:nth-child(2)
{
    width: 3%;
} 
.relay-table td:nth-child(1) {
    width: 1%;
}
.relay-table td:nth-child(2) {
    width: 1%;
}
.relay-table td:nth-child(3) {
    width: 3%;
}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>比特 7</td>
		<td class='powderblued'>比特 6</td>
		<td class='powderblued'>比特 5</td>
		<td class='powderblued'>比特 4</td>
		<td class='powderblued'>比特 3</td>
		<td class='powderblued'>比特 2</td>
		<td class='powderblued'>比特 1</td>
		<td class='powderblued'>比特 0</td>
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
		<td colspan=8>状态 = 1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>4</td>
		<td>警报计数</td>
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
		<td colspan=8>警报，警告，错误</td>
	</tr>
</tbody>
</table>

	
<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>比特 7</td>
		<td class='powderblued'>比特 6</td>
		<td class='powderblued'>比特 5</td>
		<td class='powderblued'>比特 4</td>
		<td class='powderblued'>比特 3</td>
		<td class='powderblued'>比特 2</td>
		<td class='powderblued'>比特 1</td>
		<td class='powderblued'>比特 0</td>
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
		<td>错误代码参数</td>
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

<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>比特 7</td>
		<td class='powderblued'>比特 6</td>
		<td class='powderblued'>比特 5</td>
		<td class='powderblued'>比特 4</td>
		<td class='powderblued'>比特 3</td>
		<td class='powderblued'>比特 2</td>
		<td class='powderblued'>比特 1</td>
		<td class='powderblued'>比特 0</td>
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
\.		如果您想监控从站是否处于活动状态，请检查“IO 交换中的从站列表”。
{% endhint %}

<div class="page-break"></div>


<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>比特 7</td>
		<td class='powderblued'>比特 6</td>
		<td class='powderblued'>比特 5</td>
		<td class='powderblued'>比特 4</td>
		<td class='powderblued'>比特 3</td>
		<td class='powderblued'>比特 2</td>
		<td class='powderblued'>比特 1</td>
		<td class='powderblued'>比特 0</td>
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


<div class="page-break"></div>

<table class="my-custom-table">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>比特 7</td>
		<td class='powderblued'>比特 6</td>
		<td class='powderblued'>比特 5</td>
		<td class='powderblued'>比特 4</td>
		<td class='powderblued'>比特 3</td>
		<td class='powderblued'>比特 2</td>
		<td class='powderblued'>比特 1</td>
		<td class='powderblued'>比特 0</td>
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
		<td colspan=8>IO 交换中的从站列表 = 6</td>
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


<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/6-slot-profinet-io-info.md)
# 3.4.14.6 S relay - Profinet IO Master Status

<style>
.my-custom-table table  {border-collapse:collapse;}
.my-custom-table td {border-color:gray;border-style:solid;border-width:1px;font-size: 11px}
.my-custom-table th:nth-child(1)
{
    width: 2%;
} 
.my-custom-table th:nth-child(2)
{
    width: 3%;
} 
.relay-table td:nth-child(1) {
    width: 1%;
}
.relay-table td:nth-child(2) {
    width: 1%;
}
.relay-table td:nth-child(3) {
    width: 3%;
}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<br>

{% hint style="info" %}
\.		如果您想监控从站是否处于活动状态，请检查“IO交换中的从站列表”。
{% endhint %}

<br>

<table class="my-custom-table">
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
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

<div class="page-break"></div>

<table class="my-custom-table">
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>IO 交换中的从站列表 = 6</td>
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

<div class="page-break"></div>

<table class="my-custom-table">
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
		<td colspan=8>插槽号 = 1 ~ 3</td>
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
<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/14-slot-cifx-info/7-slot-ethercat-info.md)
# 3.4.14.7 S relay - EtherCAT Master Status

<style>
.my-custom-table table  {border-collapse:collapse;}
.my-custom-table td {border-color:gray;border-style:solid;border-width:1px;font-size: 11px}
.my-custom-table th:nth-child(1)
{
    width: 2%;
} 
.my-custom-table th:nth-child(2)
{
    width: 3%;
} 
.relay-table td:nth-child(1) {
    width: 1%;
}
.relay-table td:nth-child(2) {
    width: 1%;
}
.relay-table td:nth-child(3) {
    width: 3%;
}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<br>

{% hint style="info" %}
\.		如果您想监控从设备是否处于活动状态，请检查“IO交互中的从设备列表”。
{% endhint %}

<br>

<table class="my-custom-table">
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
		<td colspan=8>获取EtherCAT状态 = 1018</td>
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
		<td colspan=8>已配置的从设备列表 = 5</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>Node 7</td>
		<td>Node 6</td>
		<td>Node 5</td>
		<td>Node 4</td>
		<td>Node 3</td>
		<td>Node 2</td>
		<td>Node 1</td>
		<td>Node 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>Node 15</td>
		<td>Node 14</td>
		<td>Node 13</td>
		<td>Node 12</td>
		<td>Node 11</td>
		<td>Node 10</td>
		<td>Node 9</td>
		<td>Node 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>Node 23</td>
		<td>Node 22</td>
		<td>Node 21</td>
		<td>Node 20</td>
		<td>Node 19</td>
		<td>Node 18</td>
		<td>Node 17</td>
		<td>Node 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>Node 31</td>
		<td>Node 30</td>
		<td>Node 29</td>
		<td>Node 28</td>
		<td>Node 27</td>
		<td>Node 26</td>
		<td>Node 25</td>
		<td>Node 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>Node 39</td>
		<td>Node 38</td>
		<td>Node 37</td>
		<td>Node 36</td>
		<td>Node 35</td>
		<td>Node 34</td>
		<td>Node 33</td>
		<td>Node 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>Node 47</td>
		<td>Node 46</td>
		<td>Node 45</td>
		<td>Node 44</td>
		<td>Node 43</td>
		<td>Node 42</td>
		<td>Node 41</td>
		<td>Node 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>Node 55</td>
		<td>Node 54</td>
		<td>Node 53</td>
		<td>Node 52</td>
		<td>Node 51</td>
		<td>Node 50</td>
		<td>Node 49</td>
		<td>Node 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>Node 63</td>
		<td>Node 62</td>
		<td>Node 61</td>
		<td>Node 60</td>
		<td>Node 59</td>
		<td>Node 58</td>
		<td>Node 57</td>
		<td>Node 56</td>
	</tr>
		<tr>
		<td>12</td>
		<td>Node 71</td>
		<td>Node 70</td>
		<td>Node 69</td>
		<td>Node 68</td>
		<td>Node 67</td>
		<td>Node 66</td>
		<td>Node 65</td>
		<td>Node 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>Node 79</td>
		<td>Node 78</td>
		<td>Node 77</td>
		<td>Node 76</td>
		<td>Node 75</td>
		<td>Node 74</td>
		<td>Node 73</td>
		<td>Node 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>Node 87</td>
		<td>Node 86</td>
		<td>Node 85</td>
		<td>Node 84</td>
		<td>Node 83</td>
		<td>Node 82</td>
		<td>Node 81</td>
		<td>Node 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>Node 95</td>
		<td>Node 94</td>
		<td>Node 93</td>
		<td>Node 92</td>
		<td>Node 91</td>
		<td>Node 90</td>
		<td>Node 89</td>
		<td>Node 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>Node 103</td>
		<td>Node 102</td>
		<td>Node 101</td>
		<td>Node 100</td>
		<td>Node 99</td>
		<td>Node 98</td>
		<td>Node 97</td>
		<td>Node 96</td>
	</tr>
		<tr>
		<td>17</td>
		<td>Node 111</td>
		<td>Node 110</td>
		<td>Node 109</td>
		<td>Node 108</td>
		<td>Node 107</td>
		<td>Node 106</td>
		<td>Node 105</td>
		<td>Node 104</td>
	</tr>
		<tr>
		<td>18</td>
		<td>Node 119</td>
		<td>Node 118</td>
		<td>Node 117</td>
		<td>Node 116</td>
		<td>Node 115</td>
		<td>Node 114</td>
		<td>Node 113</td>
		<td>Node 112</td>
	</tr>
		<tr>
		<td>19</td>
		<td>Node 127</td>
		<td>Node 126</td>
		<td>Node 125</td>
		<td>Node 124</td>
		<td>Node 123</td>
		<td>Node 122</td>
		<td>Node 121</td>
		<td>Node 120</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

<table class="my-custom-table">
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
		<td colspan=8>获取EtherCAT状态 = 1018</td>
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
		<td colspan=8>IO交互中的从设备列表 = 6</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>Node 7</td>
		<td>Node 6</td>
		<td>Node 5</td>
		<td>Node 4</td>
		<td>Node 3</td>
		<td>Node 2</td>
		<td>Node 1</td>
		<td>Node 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>Node 15</td>
		<td>Node 14</td>
		<td>Node 13</td>
		<td>Node 12</td>
		<td>Node 11</td>
		<td>Node 10</td>
		<td>Node 9</td>
		<td>Node 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>Node 23</td>
		<td>Node 22</td>
		<td>Node 21</td>
		<td>Node 20</td>
		<td>Node 19</td>
		<td>Node 18</td>
		<td>Node 17</td>
		<td>Node 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>Node 31</td>
		<td>Node 30</td>
		<td>Node 29</td>
		<td>Node 28</td>
		<td>Node 27</td>
		<td>Node 26</td>
		<td>Node 25</td>
		<td>Node 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>Node 39</td>
		<td>Node 38</td>
		<td>Node 37</td>
		<td>Node 36</td>
		<td>Node 35</td>
		<td>Node 34</td>
		<td>Node 33</td>
		<td>Node 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>Node 47</td>
		<td>Node 46</td>
		<td>Node 45</td>
		<td>Node 44</td>
		<td>Node 43</td>
		<td>Node 42</td>
		<td>Node 41</td>
		<td>Node 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>Node 55</td>
		<td>Node 54</td>
		<td>Node 53</td>
		<td>Node 52</td>
		<td>Node 51</td>
		<td>Node 50</td>
		<td>Node 49</td>
		<td>Node 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>Node 63</td>
		<td>Node 62</td>
		<td>Node 61</td>
		<td>Node 60</td>
		<td>Node 59</td>
		<td>Node 58</td>
		<td>Node 57</td>
		<td>Node 56</td>
	</tr>
		<tr>
		<td>12</td>
		<td>Node 71</td>
		<td>Node 70</td>
		<td>Node 69</td>
		<td>Node 68</td>
		<td>Node 67</td>
		<td>Node 66</td>
		<td>Node 65</td>
		<td>Node 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>Node 79</td>
		<td>Node 78</td>
		<td>Node 77</td>
		<td>Node 76</td>
		<td>Node 75</td>
		<td>Node 74</td>
		<td>Node 73</td>
		<td>Node 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>Node 87</td>
		<td>Node 86</td>
		<td>Node 85</td>
		<td>Node 84</td>
		<td>Node 83</td>
		<td>Node 82</td>
		<td>Node 81</td>
		<td>Node 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>Node 95</td>
		<td>Node 94</td>
		<td>Node 93</td>
		<td>Node 92</td>
		<td>Node 91</td>
		<td>Node 90</td>
		<td>Node 89</td>
		<td>Node 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>Node 103</td>
		<td>Node 102</td>
		<td>Node 101</td>
		<td>Node 100</td>
		<td>Node 99</td>
		<td>Node 98</td>
		<td>Node 97</td>
		<td>Node 96</td>
	</tr>
		<tr>
		<td>17</td>
		<td>Node 111</td>
		<td>Node 110</td>
		<td>Node 109</td>
		<td>Node 108</td>
		<td>Node 107</td>
		<td>Node 106</td>
		<td>Node 105</td>
		<td>Node 104</td>
	</tr>
		<tr>
		<td>18</td>
		<td>Node 119</td>
		<td>Node 118</td>
		<td>Node 117</td>
		<td>Node 116</td>
		<td>Node 115</td>
		<td>Node 114</td>
		<td>Node 113</td>
		<td>Node 112</td>
	</tr>
		<tr>
		<td>19</td>
		<td>Node 127</td>
		<td>Node 126</td>
		<td>Node 125</td>
		<td>Node 124</td>
		<td>Node 123</td>
		<td>Node 122</td>
		<td>Node 121</td>
		<td>Node 120</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

<table class="my-custom-table">
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
		<td colspan=8>获取EtherCAT状态 = 1018</td>
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
		<td colspan=8>诊断从设备列表 = 7</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>Node 7</td>
		<td>Node 6</td>
		<td>Node 5</td>
		<td>Node 4</td>
		<td>Node 3</td>
		<td>Node 2</td>
		<td>Node 1</td>
		<td>Node 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>Node 15</td>
		<td>Node 14</td>
		<td>Node 13</td>
		<td>Node 12</td>
		<td>Node 11</td>
		<td>Node 10</td>
		<td>Node 9</td>
		<td>Node 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>Node 23</td>
		<td>Node 22</td>
		<td>Node 21</td>
		<td>Node 20</td>
		<td>Node 19</td>
		<td>Node 18</td>
		<td>Node 17</td>
		<td>Node 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>Node 31</td>
		<td>Node 30</td>
		<td>Node 29</td>
		<td>Node 28</td>
		<td>Node 27</td>
		<td>Node 26</td>
		<td>Node 25</td>
		<td>Node 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>Node 39</td>
		<td>Node 38</td>
		<td>Node 37</td>
		<td>Node 36</td>
		<td>Node 35</td>
		<td>Node 34</td>
		<td>Node 33</td>
		<td>Node 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>Node 47</td>
		<td>Node 46</td>
		<td>Node 45</td>
		<td>Node 44</td>
		<td>Node 43</td>
		<td>Node 42</td>
		<td>Node 41</td>
		<td>Node 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>Node 55</td>
		<td>Node 54</td>
		<td>Node 53</td>
		<td>Node 52</td>
		<td>Node 51</td>
		<td>Node 50</td>
		<td>Node 49</td>
		<td>Node 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>Node 63</td>
		<td>Node 62</td>
		<td>Node 61</td>
		<td>Node 60</td>
		<td>Node 59</td>
		<td>Node 58</td>
		<td>Node 57</td>
		<td>Node 56</td>
	</tr>
		<tr>
		<td>12</td>
		<td>Node 71</td>
		<td>Node 70</td>
		<td>Node 69</td>
		<td>Node 68</td>
		<td>Node 67</td>
		<td>Node 66</td>
		<td>Node 65</td>
		<td>Node 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>Node 79</td>
		<td>Node 78</td>
		<td>Node 77</td>
		<td>Node 76</td>
		<td>Node 75</td>
		<td>Node 74</td>
		<td>Node 73</td>
		<td>Node 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>Node 87</td>
		<td>Node 86</td>
		<td>Node 85</td>
		<td>Node 84</td>
		<td>Node 83</td>
		<td>Node 82</td>
		<td>Node 81</td>
		<td>Node 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>Node 95</td>
		<td>Node 94</td>
		<td>Node 93</td>
		<td>Node 92</td>
		<td>Node 91</td>
		<td>Node 90</td>
		<td>Node 89</td>
		<td>Node 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>Node 103</td>
		<td>Node 102</td>
		<td>Node 101</td>
		<td>Node 100</td>
		<td>Node 99</td>
		<td>Node 98</td>
		<td>Node 97</td>
		<td>Node 96</td>
	</tr>
		<tr>
		<td>17</td>
		<td>Node 111</td>
		<td>Node 110</td>
		<td>Node 109</td>
		<td>Node 108</td>
		<td>Node 107</td>
		<td>Node 106</td>
		<td>Node 105</td>
		<td>Node 104</td>
	</tr>
		<tr>
		<td>18</td>
		<td>Node 119</td>
		<td>Node 118</td>
		<td>Node 117</td>
		<td>Node 116</td>
		<td>Node 115</td>
		<td>Node 114</td>
		<td>Node 113</td>
		<td>Node 112</td>
	</tr>
		<tr>
		<td>19</td>
		<td>Node 127</td>
		<td>Node 126</td>
		<td>Node 125</td>
		<td>Node 124</td>
		<td>Node 123</td>
		<td>Node 122</td>
		<td>Node 121</td>
		<td>Node 120</td>
	</tr>
</tbody>
</table>
<div class="page-break"></div>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>获取_IP_信息 (172)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>局域网 (1~3)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=6>result</td>
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

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/16-slot-mech-info.md)
# 3.4.16 S 继电器 - MECH_INFO

Supported from V60.30-01.

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

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/17-slot-tool-info.md)
# 3.4.17 S relay - TOOL_INFO

获取工具数据中设置的信息。 <br>
支持从 V60.30-01 开始。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_TOOL_INFO (174)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>工具编号</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param. 2</td>
		<td>工具数据<br>0 = 长度, 1=角度, 2=中心, 3=惯性</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>result</td>
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

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/18-slot-ucrd-info.md)
# 3.4.18 S relay - UCRD_INFO

获取用户坐标系统中注册的信息。 <br>
支持版本 V60.30-01。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_UCRD_INFO (176)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>用户坐标编号</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param. 2</td>
		<td>用户坐标数据<br>0 = 长度, 1=角度</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=6>result</td>
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

<div class="page-break"></div>
[__SOURCE](3-relay/4-sw-relay/19-slot-monopump.md)
# 3.4.19 S relay - MONOPUMP

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_MONITOR_INFO (4100)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
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
		<td>rpm 当前值</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>压力 (bar)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>流量总量 (cc) - 车辆类型的总值</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_MANUAL_OPER1 (4110)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td>流量 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>流量 (固定量模式) (cc)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>回吸流量 (cc/s)</td>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_MANUAL_OPER2 (4112)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td>延迟时间 (s)</td>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>SET_MANUAL_OPER (4111)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 2</td>
		<td>设置数据的项 <br>
		1 = 流量 (cc/s) <br>
		2 = 流量 (固定量模式) (cc) <br>
		3 = 回吸流量 (cc/s) <br>
		4 = 回吸时间 (s) <br>
		5 = 延迟时间 (s) <br>
		6 = 补充流量 (cc/s) <br>
		7 = 补充时间 (s)
		</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>param 3</td>
		<td>值</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>10</td>
		<td>param 4</td>
		<td>设置 = 1, 设置值后强制初始化为 0</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>MANUAL_OPER (4113)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 2</td>
		<td>操作项 <br>
		1 = 固定速度放料 <br>
		2 = 固定量放料 <br>
		3 = 停止放料 <br>
		启动操作后强制初始化为 0 <br>
		</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_COND_INFO1 (4120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>cnd_no (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td></td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>流量 (固定量模式) (cc)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>回吸流量 (cc/s)</td>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_COND_INFO2 (4122)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>cnd_no (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td>延迟时间 (s)</td>
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
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>SET_COND_INFO (4121)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>cnd_no (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 2</td>
		<td>设置数据的项 <br>
		2 = 流量 (固定量模式) (cc) <br>
		3 = 回吸流量 (cc/s) <br>
		4 = 回吸时间 (s) <br>
		5 = 延迟时间 (s) <br>
		6 = 补充流量 (cc/s) <br>
		7 = 补充时间 (s)
		</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>param 3</td>
		<td>值</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>10</td>
		<td>param 4</td>
		<td>设置 = 1, 设置值后强制初始化为 0</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
[__SOURCE](3-relay/5-relative-addr.md)
# 3.5 为继电器指定间接地址

SW62-SW79 是用于指定间接地址的系统内存。无论继电器类型如何，如果在继电器地址中指定的值介于 -2 和 -18 之间，则设置的值将导致存储在 SW62-SW79 中的指定继电器地址。



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

下面呈现的嵌入式可编程逻辑控制器 (PLC) 示例是使用 FOR/NEXT 指令和间接地址指定方法创建的，将输出信号 Y1-Y128 对应于输入信号 X1-X128。

![](../_assets/rel-addr-for-next.png)
[__SOURCE](3-relay/6-timer-counter.md)
# 3.6 定时器与计数器继电器

(1) 所有定时器和计数器继电器仅支持向下计数。  
*	定时器基准可以由用户以10毫秒单位设置。  
*	由于定时器值在内部处理为32位值，因此可以计数到2,147,483,647 [毫秒]（大约597小时）。 
<br>
<br>

(2) 定时器与计数器的值具有以下含义：  
<table class="tg">
<thead>
	<tr>
		<th>定时器与计数器值</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>0</td>
		<td>接触开启（=计数完成）</td>
	</tr>
	<tr>
		<td>-1</td>
		<td>接触关闭</td>
	</tr>
	<tr>
		<td>其他</td>
		<td>接触关闭；定时与计数（进行中）</td>
	</tr>
</tbody>
</table>
<br>

(3) 如果定时器与计数器继电器连接的 rung 处于非活动状态，  
*	TON: TL（定时器）的值变为-1。  
*	CTD: CL（计数器）的值持续保持。 
<br>
<br>

(4) 当定时器与计数器继电器连接的 rung 处于活动状态时， 
*	TON <br> 
    如果 TL 的值小于0，则 TL 的初始值存储为“定时器基准 x 预设 x 10”，如果 TL 的值大于0，则每5毫秒减少5。 

*	CTD <br>
    如果 CL 的值小于0，则初始 CL 值为预设值。如果 CL 的值大于0，则每次 CL 从非活动变为活动时，值减少1。 
[__SOURCE](4-instruction/README.md)
# 4. Instructions

A ladder program consists of multiple rungs, and each rung consists of multiple instructions.

The embedded PLC performs logical I/O operations while sequentially executing instructions in the program.

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table>
<thead>
  <tr>
    <td rowspan="11">梯子项目</td>
    <td rowspan="7">梯子程序</td>
    <td rowspan="3">横档</td>
    <td>指令</td>
  </tr>
  <tr>
    <td>指令</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">横档</td>
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
    <td rowspan="3">梯子程序</td>
    <td rowspan="2">横档</td>
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

An instruction consists of three elements, as shown below.

<table>
<thead>
  <tr>
    <th>指令 (助记符)</th>
    <th>操作类型</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>操作数</td>
    <td>操作的参数。<br>根据指令，可以指定一个或多个操作数，但有些指令没有操作数。</td>
  </tr>
  <tr>
    <td>注释</td>
    <td>为程序的可读性附加的描述。注释不会影响操作。</td>
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
    <td>梯子</td>
    <td>├─┤</td>
    <td>梯子</td>
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

### * 逻辑检查指令：如果检查结果为真，则梯子处于活动状态。如果为假，则梯子处于非活动状态。 

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
		<td>检查接触是否关闭（接触A）</td>
	</tr>
	<tr>
		<td>XIO</td>
		<td>检查是否打开</td>
		<td>-|/|-</td>
		<td>检查接触是否打开（接触B）</td>
	</tr>
	<tr>
		<td>INV</td>
		<td>反转</td>
		<td>-//-</td>
		<td>反转梯子的结果（反转）</td>
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

<div class="page-break"></div>

### * 输出指令

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
		<td>梯子的状态（活动：ON/非活动：OFF）将被输出</td>
	</tr>
	<tr>
		<td>OTL</td>
		<td>输出保持</td>
		<td>-(L)-</td>
		<td>如果梯子处于活动状态，则输出信号将以ON（高）状态输出</td>
	</tr>
	<tr>
		<td>OTU</td>
		<td>输出释放</td>
		<td>-(U)-</td>
		<td>如果梯子处于活动状态，则输出信号将以OFF（低）状态输出</td>
	</tr>
	<tr>
		<td>OSR</td>
		<td>单次上升</td>
		<td>-(OSR)-</td>
		<td>如果梯子处于活动状态，则输出信号将在一次扫描的持续时间内仅输出为ON状态</td>
	</tr>
	<tr>
		<td>RES</td>
		<td>重置</td>
		<td>-(RES)-</td>
		<td>如果梯子处于活动状态，则计时器或计数器将被重置</td>
	</tr>
</tbody>
</table>

### * 计时器和计数器指令

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
		<td>开机延迟时间</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>计时器仅在梯子处于活动状态时工作</td>
	</tr>
	<tr>
		<td>CTD</td>
		<td>倒计时</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>梯子的激活（非活动 -> 活动）将被倒计时</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

### * 算术运算指令

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
		<td>如果梯子处于活动状态，则进行加法 (+) 操作</td>
	</tr>
	<tr>
		<td>SUB</td>
		<td>减法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行减法 (-) 操作</td>
	</tr>
	<tr>
		<td>MUL</td>
		<td>乘法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行乘法 (x) 操作</td>
	</tr>
	<tr>
		<td>DIV</td>
		<td>除法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行除法 (/) 操作</td>
	</tr>
	<tr>
		<td>POW</td>
		<td>幂</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行幂 (^) 操作</td>
	</tr>
	<tr>
		<td>AND</td>
		<td>按位与</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行按位与 (&) 操作</td>
	</tr>
	<tr>
		<td>OR</td>
		<td>按位或</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行按位或 (|) 操作</td>
	</tr>
</tbody>
</table>

### * 数据转换指令

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
		<td>如果梯子处于活动状态，则整数将被转换为BCD</td>
	</tr>
	<tr>
		<td>FRD</td>
		<td>将BCD转换为整数</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则BCD将被转换为整数</td>
	</tr>
	<tr>
		<td>SEG</td>
		<td>7段</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将进行7段值的转换</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

### * 移动和复制指令

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
		<td>如果梯子处于活动状态，将复制一条数据</td>
	</tr>
	<tr>
		<td>COP</td>
		<td>复制数据</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将复制多条数据</td>
	</tr>
	<tr>
		<td>CCOP</td>
		<td>条件复制数据</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>根据梯子的状态，将复制多条数据</td>
	</tr>
	<tr>
		<td>ROT</td>
		<td>旋转输出</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将进行顺序输出</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

### * 块控制指令

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
		<td>如果梯子处于活动状态，将发生重复执行直到Next</td>
	</tr>
	<tr>
		<td>NEXT</td>
		<td>NEXT 循环</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果计数在重复次数内，将跳转到FOR指令</td>
	</tr>
	<tr>
		<td>LBL</td>
		<td>标签</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>根据JMP指令，指定跳转的位置</td>
	</tr>
	<tr>
		<td>JMP</td>
		<td>跳跃</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将跳转到LBL位置<br>
		（如果Label&lt;0，将跳过-n NEXTs）</td>
	</tr>
	<tr>
		<td>CALL</td>
		<td>调用</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将调用子梯子</td>
	</tr>
	<tr>
		<td>END</td>
		<td>结束</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，子梯子将结束</td>
	</tr>
</tbody>
</table>
[__SOURCE](4-instruction/2-xic.md)
# 4.2 XIC (检查是否关闭): Examining if Closed

### Description
如果操作数的位值为 1，则梯级将被激活。如果为 0，则将被停用。

<br>

### Types that can be used as an operand
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
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
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

### Example of use

当运行开关，也就是输入 X2 的接点 A，处于按下状态 (1 = 激活) 时，内部状态继电器 M5 正常 (1)，则“运行”指示灯输出 Y5 将被打开。

![](../_assets/xic.png)
[__SOURCE](4-instruction/3-xio.md)
# 4.3 XIO (检查是否打开): 检查是否打开

### Description
如果操作数的位值为0，则梯形图将被激活。如果为1，它将被禁用。

<br>

### 可以用作操作数的类型
(对 X 不可用)
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
    <th>常数<br>32bit</th>
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

当“暂停”按钮，即输入 X1 的接点 B，处于按下状态 (0 = 激活) 时，制动输出 Y8 将被打开。  

![](../_assets/xio.png)
[__SOURCE](4-instruction/4-inv.md)
# 4.4 INV (反转): 反转

### 描述
反转 (活动 <-> 不活动) 梯级的先前结果。

<br>

### 使用示例

根据德摩根定律，处理一次反转将使 /(AxB) 等于 /A+/B 或 /(A+B) 等于 /Ax/B，从而允许一个简单的配置，使用没有分支的 AND 逻辑，而不是使用具有多个分支的 OR 逻辑的配置。因此，以下两个梯级的逻辑将产生相同的结果，因为 (X1+X2+X3) 等于 /(/X1x/X2x/X3)。

![](../_assets/inv.png)
[__SOURCE](4-instruction/5-equ.md)
# 4.5 EQU (Equal): 检查是否相等

### Description
如果两个值进行比较并发现相等，则该梯级将被激活（接点激活）。

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
    <td class='hd'>来源 a</td>
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

如果输入 XB3 的值等于 100，则输出 Y7 将被打开。否则，它将被关闭。

![](../_assets/equ.png)
[__SOURCE](4-instruction/6-neq.md)
# 4.6 NEQ (不等于): 检查是否不等于

### 描述
如果比较两个值并发现它们不相等，则该梯级将被激活（接触激活）。

<br>

### 可以作为操作数使用的类型
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

如果输入 XB4 的值不等于 50，则输出 Y8 将被打开。否则，它将被关闭。

![](../_assets/neq.png)
[__SOURCE](4-instruction/7-les.md)
# 4.7 LES (小于): 检查是否小于

### 描述
如果“源 a”的值小于“源 b”的值，则该梯级将被激活（接触激活）。

<br>

### 可用作操作数的类型
(对 X 不可能)
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
    <th>常数<br>32bit</th>
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

如果输入 XB7 的值小于 70，则输出 Y9 将被打开。如果大于或等于 70，输出将被关闭。

![](../_assets/les.png)
[__SOURCE](4-instruction/8-grt.md)
# 4.8 GRT (大于): 检查是否大于

### Description
如果“源 a”的值大于“源 b”的值，则该行将被激活（接触激活）。

<br>

### Types that can be used as an operand
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
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
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
<tbody>
  <tr>
    <td class='hd'>source b</td>
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

### Example of use

如果输入 XB8 的值大于 80，则输出 Y10 将被打开。如果小于或等于 80，则输出将被关闭。

![](../_assets/grt.png)
[__SOURCE](4-instruction/9-leq.md)
# 4.9 LEQ (小于或等于)：检查是否小于或等于

### 描述
如果“源 a”的值小于或等于“源 b”的值，则该梯级将被激活（接触激活）。

<br>

### 可以用作操作数的类型
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

如果输入 XB9 的值小于或等于 90，则输出 Y11 将被打开。如果大于 90，则输出将被关闭。

![](../_assets/leq.png)
[__SOURCE](4-instruction/10-geq.md)
# 4.10 GEQ (大于或等于): 检查是否大于或等于

### 描述
如果“源 a”的值大于或等于“源 b”的值，则该梯级将变为活动状态（接触活动）。

<br>

### 可以用作操作数的类型
(对 X 不适用)
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

如果输入 XB9 的值大于或等于 100，则输出 Y12 将被打开。如果小于 100，则输出将被关闭。

![](../_assets/geq.png)
[__SOURCE](4-instruction/11-ote.md)
# 4.11 OTE (Output Energize): 激活输出


### Description
输出信号将根据梯级的状态进行输出。换句话说，如果梯级处于激活状态，则输出信号将以 ON（高）状态输出；如果梯级处于非激活状态，则输出信号将以 OFF（低）状态输出。

<br>

### Types that can be used as an operand
(不适用于 X，DO 位支持从 V60.30-07)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
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

### Example of use

Y12 将在输入 DO12 的状态下输出。

![](../_assets/ote.png)
[__SOURCE](4-instruction/12-otl.md)
# 4.12 OTL (输出锁存): 锁存输出


### 描述
如果梯级处于活动状态，输出信号将输出为 ON（高）状态。但是，如果梯级处于非活动状态，输出将保持不变。

<br>

### 可以作为操作数使用的类型
（对于 X，不可能，DO 位支持从 V60.30-07）
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

如果输入 DO13 处于 ON 状态，Y13 将处于 ON 状态。即使之后 DO13 切换到 OFF 状态，Y13 仍将保持在 ON 状态。

![](../_assets/otl.png)
[__SOURCE](4-instruction/13-otu.md)
# 4.13 OTU (输出取消): 取消输出

### 描述
如果梯级处于活动状态，输出信号将以关闭（低）状态输出。如果梯级处于非活动状态，输出将保持不变。

<br>

### 可以用作操作数的类型
（对于 X，不可能，DO 位从 V60.30-07 支持）
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

当输入 DO14 处于 ON 状态时，Y14 将处于 OFF 状态。即使 DO14 随后切换到 OFF 状态，Y14 也将保持在 OFF 状态。

![](../_assets/otu.png)
[__SOURCE](4-instruction/14-osr.md)
# 4.14 OSR (One Shot Rising): One-Shot-Rising 输出

### 描述
如果该梯级处于活动状态，输出信号仅会在一次扫描的持续时间内输出。换句话说，当梯级从非活动状态切换到活动状态时，相应的继电器将仅在一次扫描的持续时间内处于ON状态。

<br>

### 可以用作操作数的类型
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

如果输入 X17 处于 ON 状态，内部状态继电器 M17 将处于 ON 状态。M17 将保持在 ON 状态，直到相关扫描完成，如果开始新的扫描，它将切换为 OFF 状态。

![](../_assets/osr.png)
[__SOURCE](4-instruction/15-res.md)
# 4.15 重置 (RES): 重置


### 描述
 如果 rung 处于活动状态，定时器 (T) 或计数器 (C) 继电器值将被清除 (-1)。

<br>

### 可用作操作数的类型
(不适用于 X)
<style type="text/css">
table  {border-collapse:collapse;table-layout: fixed;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>继电器<br>类型</th>
    <th colspan="2">输入<br>X, DO</th>
    <th colspan="2">输出<br>Y, DI, R, K</th>
    <th colspan="2">内存<br>M, S</th>
    <th colspan="2">定时器<br>T</th>
    <th colspan="2">计数<br>C</th>
    <th>常量<br>32bit</th>
  </tr>
  <tr>
    <th>数据<br>类型</th>
    <th>位</th>
    <th>B,W,<br>L,F</th>
    <th>位</th>
    <th>B,W,<br>L,F</th>
    <th>位</th>
    <th>B,W,<br>L,F</th>
    <th>位</th>
    <th>B,W,<br>L,F</th>
    <th>位</th>
    <th>B,W,<br>L,F</th>
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

如果内部状态继电器 M18 处于 ON 状态，定时器继电器 T28 将被清除为 -1。

![](../_assets/res.png)
[__SOURCE](4-instruction/16-ton.md)
# 4.16 延时定时器 (TON): 定时器

### 描述
在计算该梯形图活跃期间的时间后，设定的时间 (定时器基数 x 预设值 x 10) [ms] 后，相关定时器继电器将处于 ON（高）状态。然而，如果梯形图处于非活跃状态，相关定时器继电器将立即清除 (-1)。 
注意) T 的值以 1 ms 为单位。

<br>

### 可用作操作数的类型
(对 X 不可用)
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
    <td class='hd'>定时器基数(1/100s)</td>
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
    <td class='hd'>预设值</td>
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

当输入 DO34 在 ON 状态下持续一秒后，T32 的定时器继电器将处于 ON 状态。此时，输出 Y34 将处于 ON 状态。

![](../_assets/ton.png)
[__SOURCE](4-instruction/17-ctd.md)
# 4.17 倒计时 (CTD): 计数器


### 描述
梯级的上升（从不活动变为活动）将被倒计时。
如果相关的 C 值变为 0，相关计数器将处于 ON（高）状态，不再进行计数。
当梯级处于活动状态但相关 C 的值为负时，预设值将被存储在 C 中。
注意）即使梯级不活动，C 也不会被清除（-1）。要清除，必须执行 RES 指令。

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
    <th colspan="2">输出<br>Y, DI</th>
    <th colspan="2">内存<br>M, S</th>
    <th colspan="2">计数<br>C</th>
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

如果内部状态继电器 M19 从 OFF 状态切换到 ON 状态，C20 的值从 3 开始，继续减少 1。当 C20 的值变为 0 时，计数器继电器将处于 ON 状态。此时，输出 Y35 将处于 ON 状态。

![](../_assets/ctd.png)
[__SOURCE](4-instruction/18-add.md)
# 4.18 Add (ADD): 添加


### Description
如果梯级处于活动状态，则“源 a”的值与“源 b”的值将相加，结果值将设置在“目标”继电器中。如果操作结果发生溢出，设置 S7=1 将发生。

<br>

### 可以用作操作数的类型
(对于 X 不可行)
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

当输入 DO36 激活时，将向 XB3 的值添加 50，结果值将设置在内部状态继电器 MB3 中。

![](../_assets/add.png)
[__SOURCE](4-instruction/19-sub.md)
# 4.19 减法 (SUB): 减法

### 描述
如果这个梯级是活动的，"source b" 的值将从 "source a" 的值中减去，结果值将被设置在 "destination" 继电器中。

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
<tbody>
  <tr>
    <td class='hd'>source b</td>
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
    <td class='hd'>destination</td>
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

如果输入 DO37 处于活动状态，将从 XB3 的值中减去 10，并将结果值设置在内部状态继电器 MB3 中。

![](../_assets/sub.png)
[__SOURCE](4-instruction/20-mul.md)
# 4.20 Multiply (MUL): 乘法

### Description
如果 rung 是活动的，"source a" 的值将乘以 "source b" 的值，结果值将设置在 "destination" 继电器中。
如果操作结果发生溢出，将会设置 S7=1。

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
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
<tbody>
  <tr>
    <td class='hd'>source b</td>
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
    <td class='hd'>destination</td>
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

### Example of use

如果输入 DO38 是活动的，XB3 的值将乘以 3，结果值将设置在内部状态继电器 MB3 中。

![](../_assets/mul.png)
[__SOURCE](4-instruction/21-div.md)
# 4.21 分割 (DIV): 分割


### 描述
如果梯级处于活动状态，"source a" 的值将被 "source b" 的值划分，结果值将设置在 "destination" 继电器中。
如果 "source b" 的值为 0 或操作结果发生溢出，将发生设定 S7=1。

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
<tbody>
  <tr>
    <td class='hd'>source b</td>
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
    <td class='hd'>destination</td>
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

如果输入 DO39 处于活动状态，XB3 的值将被 4 划分，结果值将设置在内部状态继电器 MB3 中。

![](../_assets/div.png)
[__SOURCE](4-instruction/22-pow.md)
# 4.22 Power (POW): 功率


### Description
如果梯级处于活动状态，"source a"的值将被提升到"source b"的值的幂，结果值将被设置在"destination"继电器中。如果操作结果发生溢出，将设置S7=1。

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
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
<tbody>
  <tr>
    <td class='hd'>source b</td>
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
    <td class='hd'>destination</td>
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

### Use of example

如果输入DO40处于活动状态，XB3的值将被提升到2的幂，结果值将被设置在内部状态继电器MB3中。 

![](../_assets/pow.png)
[__SOURCE](4-instruction/23-tod.md)
# 4.23 TOD (转换为BCD)：转换为BCD

### 描述
如果梯级处于活动状态，“源”的值将被转换为BCD值，转换后的值将存储在“目的地”中。此指令在使用以BCD格式显示值的7段显示器的设备时会很方便。如果“目的地”的数据类型为字节（B）格式，则“源”的值将转换为两位数字。如果它是字（W）格式，则“源”的值将转换为四位数字。然而，如果“源”的值大于要转换的位数，则将发生设置S6=1。

<br>

### 可以用作操作数的类型
(无法用于X，无符号整数u)
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

如果输入DO42处于活动状态，XB3的值将被转换为BCD值，转换后的值将设置在内部状态继电器MB3中。 
(注意：二进制编码十进制（BCD）是指其4位代码值可以有从0到9的值的数字。也就是说，对于BCD数字，0-F中代表4位的数字A-F不被使用。)
如果& H7B（123）被转换为BCD值，转换后的值将是& H23（35），并且因为& H7B（123）大于& H63（99），所以将发生设置S6=1。

![](../_assets/tod.png)
[__SOURCE](4-instruction/24-frd.md)
# 4.24 FRD (Convert from BCD to Integer): 转换为整数


### Description
如果梯级处于活动状态，"source" 的 BCD 值将被转换为整数，并且转换后的值将存储在 "destination" 中。 
当以 BCD 格式输出的凸轮开关的值作为输入接收时，可以方便地使用此指令。
如果 "source" 的值不是 BCD 值，将发生设置 S6=1。
此外，如果 "source" 是字（W）格式，而 "destination" 是字节（B）格式，则要转换的 "source" 的最大值将是 &H9999。因此，转换为整数的结果将是 9999 (&H270F)，这将导致字节范围 &Hff 被超出，因而发生溢出。在这种情况下，将发生设置 S=6。

<br>

### Types that can be used as an operand
(not possible for X, unsigned integers for u)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source</td>
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
    <td class='hd'>destination</td>
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

### Example of use

如果输入 DO43 处于活动状态，XB3 的值 (BCD) 将被转换为整数，转换后的值将被设置在内部状态继电器 MB3 中。
如果 &H23(35) 被转换为整数，则该整数将是 &H17(23)。

![](../_assets/frd.png)
[__SOURCE](4-instruction/25-seg.md)
# 4.25 SEG (7-segment): 转换为 7-segment 值

### 描述
如果梯级处于活动状态，“源”的值将被转换为 7-segment 值（8 位），并将转换后的值存储在“目标”中。
如果“目标”是字（W）格式，将在“目标”中存储两个 7-segment 格式的值（8 位）。

<br>

### 可用作操作数的类型
(对于 X，不可能为无符号整数 u)
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

如果输入 DO44 活动，则与 XB3 的值相对应的 7-segment 值将设置在内部状态继电器 MW3 中。
对于 &H17，值 &H0607 结合 SEGD_1(SEGM_B|SEGM_C = 0x02|0x04 = 0x06)=&H06 和 
SEGD_7(SEGM_A|SEGM_B|SEGM_C = 0x01|0x02|0x04 = 0x07)=&H07 将存储在内部状态继电器 MW3 中。

![](../_assets/seg.png)

<br>

### 7-segment 数据

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
# 4.26 MOV (移动): Moving


### 说明
如果梯形图的 rung 是激活状态，“source”的值将被复制到“destination”。 如果“source”是字（W）格式，而“destination”是字节（B）格式，则“source”的值的低字节将仅被复制到“destination”。 因为嵌入式可编程逻辑控制器（PLC）的所有数据都作为有符号数据处理，如果“source”是字节（B）格式且其值为 -1(&Hff)，则该值将作为 -1(&HFFFF) 复制到字（W）格式的“destination”（&H00ff 变为 255 的值。）


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
    <td class='hd'>source</td>
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
    <td class='hd'>destination</td>
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

如果输入 DO55 处于活动状态，55 将被设置在内部状态继电器 MB2 中。

![](../_assets/mov.png)
[__SOURCE](4-instruction/27-cop.md)
# 4.27 复制数据 (COP)：复制


### 描述
如果梯形图的 rung 是活动的，将从“源”位置复制值到“目标”位置，复制的数量为“长度”的数量。
如果“源”是一个数字，则“目标”将根据“长度”的数量填充“源”的值。在这种情况下，当“目标”处于位格式时，如果“源”的值为 0，则“目标”将填充为 OFF；如果“源”的值不为 0，则“目标”将填充为 ON。
如果“源”是一个继电器，则“源”和“目标”的数据类型应该相同。也就是说，如果“源”是位格式，则“目标”也应该是位格式；如果“源”是字节 (B) 格式，则“目标”也应该是字节 (B) 格式；如果“源”是字 (W) 格式，则“目标”也应该是字 (W) 格式。
如果“源”+“长度”大于“源”继电器的最大数量，或者“目标”+“长度”大于“目标”继电器的最大数量，则仅会复制到继电器的最大数量。


<br>

### 可用作操作数的类型
(对 X 不可能)
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

如果输入 DO56 激活，则从输入 DOB2 复制与 8 字节对应的值到输出 YB2，作为与 8 字节对应的值。

![](../_assets/cop.png)
[__SOURCE](4-instruction/28-ccop.md)
# 4.28 条件复制数据 (CCOP)：条件复制

### 描述
根据梯级的状态，将从“源 a”或“源 b”的位置复制值到“目标”的位置，数量与“长度”相等。
如果“源”是数字，则“目标”将根据“长度”的值填充相应的值。在这种情况下，当“目标”处于位格式时，如果相应的值为0，“目标”将填充为OFF；如果相应的值不为0，“目标”将填充为ON。
如果“源”是继电器，则“源”和“目标”的数据类型应相同。也就是说，如果“源”是位格式，则“目标”应该是位格式；如果“源”是字节（B）格式，则“目标”应该是字节（B）格式；如果“源”是字（W）格式，则“目标”也应该是字（W）格式。
如果“源” + “长度”大于“源”继电器的最大数量，或者“目标” + “长度”大于“目标”继电器的最大数量，则复制将仅执行到最大继电器的数量。

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

如果输入 DO57 被激活，则相应于 4 字节的值将从输入 DOB2 复制到输出 YB2，作为相应于 4 字节的值。相反，如果输入 DO57 被激活，则相应于 4 字节的值将从输入 DOB12 复制到输出 YB2，作为相应于 4 字节的值。

![](../_assets/ccop.png)
[__SOURCE](4-instruction/29-rot.md)
# 4.29 ROT (旋转输出): 旋转输出


### 描述
如果 rung 是活动的，除了 0 以外的继电器值将在 "计数" 范围内从 "起始继电器" 输入到 "输出继电器"，持续时间为 "重复时间"。如果 "复位继电器" 有信号输入，"起始继电器" 将根据 "计数" 的数量填充 0，计时器的值将初始化为 "重复时间" 的值，"输出继电器" 将输出 0。此指令可非常方便用于需要在只有一个设备可用于输出错误号的情况下，输出指定时间内的错误号，即使有多种类型的错误可能发生。

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
    <th colspan="2">计时器<br>T</th>
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
    <td class='hd'>起始继电器</td>
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
    <td class='hd'>计时器继电器</td>
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
    <td class='hd'>临时继电器</td>
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

如果存在与错误条件 1 至 3 相关的一个或多个错误，错误号将存储在 MW50-MW55。这里，当输入 DO58 活动时，ROT 指令生成的错误号将存储在 MW70 中 2 秒，同时该数字将通过 TOD 指令转换为 BCD 值，并依次在连接到 YB3 的显示设备上显示。如果连接用于外部错误复位信号的 X3 有输入信号，存储错误号的 MW51-MW55 的内容将清除为 0，并且 MW70 和 MW80 也将清除为 0，显示设备相应地指示为 0。

![](../_assets/rot.png)
[__SOURCE](4-instruction/30-for.md)
# 4.30 FOR (FOR): 重复块


### 描述
如果 rung 是活动的，直到 Next 指令的块将被反复执行，而 "idx" 继电器值从 "init" 值以 "step" 值的大小增加到 "final" 值。
当执行 FOR 指令时，"init" 值应无条件替代为 "idx" 继电器。
FOR/NEXT 指令可以嵌套最多 10 次。例如：→ FOR() FOR() FOR() ... .NEXT NEXT NEXT
在 "step" 值大于 0 的状态下，如果 "init" 值大于 "final" 值，则不会发生任何执行。相反，将跳转到 Next 指令。
在 "step" 值小于 0 的状态下，如果 "init" 值小于 "final" 值，则不会发生任何执行。相反，将跳转到 Next 指令。
"final" 和 "step" 可以指定为变量。然而，仅在 FOR 指令开始时的值将被使用。
在特殊情况下，要在 FOR 指令中途离开，可以使用后面将要描述的 JMP（负数）指令（请参阅 JMP 指令的描述）。
注意：FOR 指令没有任何额外的分支处理。
注意：有关 NEXT 指令的更多详细信息，请参阅 [4.31 NEXT (NEXT)](./31-next)

<br>

### 可以用作操作数的类型
（X 不可用）
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
    <td class='hd'>结束</td>
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
    <td class='hd'>步长</td>
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

指令 {XIC(DO-2), OTL(Y-2)} 将在 SW62 中的值从 1 增加到 4 的同时反复执行。  
换句话说，在 "idx" 使用相对寻址的继电器状态（SW62-SW79）中，XIC 指令的 DO 继电器和 OTL 指令的 Y 继电器都是 "-2"，SW62 中的值将被应用。因此，与 DO1-DO4 中高状态信号的数字对应的 Y 继电器将以高状态输出，而没有输入的数字的 Y 输出将保持其先前状态。  
注意：相对寻址是指在相关继电器被设置为 -2 到 -9 范围内的数字时，继电器地址将指定为存储在 SW62-SW79 中的值，无论其类型如何。


![](../_assets/for.png)
[__SOURCE](4-instruction/31-next.md)
# 4.31 NEXT (NEXT): 下一个块

### 描述
该操作将根据 FOR 指令的“步长”执行。  
如果“步长”值大于 0，执行将重复进行，直到“idx”继电器值小于或等于“final”值。  
如果“步长”值小于 0，执行将重复进行，直到“idx”继电器值大于或等于“final”值。  
如果在没有 FOR 指令的情况下执行 NEXT 指令，则会忽略 NEXT 指令。  
注意：  
FOR/NEXT 指令没有用于分支的任何额外处理。因此，如果 FOR 指令记录在分支内，而 NEXT 指令记录在分支外或另一个分支内，FOR 指令将无法正确工作。  
注意：有关 FOR 指令的更多详细信息，请参考 [4.30 FOR (FOR)](./30-for)

<br>

### 使用示例

请参阅 FOR 指令使用的示例。
[__SOURCE](4-instruction/32-lbl.md)
# 4.32 LBL (标签): 指定标签


### 描述
使用JMP指令跳转的标签位置将指定为一个大于0的数字（const）。 
LBL指令将指定该位置，无论梯级是否处于活动状态。
注意：有关JMP指令的更多详情，请参阅 [4.33 JMP (跳转)](./33-jmp)

<br>

### 可以用作操作数的类型
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
    <th>const.<br>32位</th>
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

因为这些指令将与JMP命令一起使用，所以请参考JMP指令的描述。
[__SOURCE](4-instruction/33-jmp.md)
# 4.33 JMP (Jump): 跳转

### 描述
如果该 rung 是活动状态，则会跳转到与“label”中指定的标签值匹配的 LBL 指令所在的位置。特别地，如果“label”指定为小于 0 的值，则可以作为离开 FOR 指令中间的特性使用（按负数指定的数量跳过）。
注意事项 1：  
如果标签的位置在 JMP 指令的上方，并且在 JMP 指令前没有条件，则可能会发生无限循环，这将需要您的注意。当发生此情况时，设置将是 S16=1，因为扫描时间超过 5 秒。
注意事项 2：  
在 FOR/NEXT 指令块中使用 JMP（正数）指令离开该块可能会导致块控制出错。在这种情况下，需要编写一种方法，通过使用 JMP 指令（负数）跳转到 NEXT 指令。
注意：有关 LBL 指令的更多详情，请参阅 [4.32 LBL (Label)](./32-lbl)

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

如果输入 DO19 是活动的，将会根据 JMP 指令的“label 99”跳转到相关的 LBL 指令。这意味着指令 {XIC(DO20), OTE(Y20)} 将不会被执行。  
如果输入 DO19 是非活动的，则 JMP 指令将不会被执行，因此在下一个 rung 中写的 {XIC(DO20), OTE(Y20)} 指令将被执行。


![](../_assets/jmp.png)
[__SOURCE](4-instruction/34-call.md)
# 4.34 CALL (Call): 调用子梯级程序


### 描述
如果梯级处于活动状态，将调用由“文件编号”指定的编号（1到99）的子梯级程序。
子梯级程序最多可以有99个文件名，范围从 S01xxxx.LAD 到 S99xxxx.LAD，对于文件名的“xxxx”部分，用户可以任意添加最多15个字符。

<br>

### 可以用作操作数的类型
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

当输入DO21处于活动状态时，将按顺序调用编号从S01xxxx.LAD到S99xxxx.LAD的文件。
执行CALL指令的结果是，如果与该数字相关的子梯级程序不存在，或者数字的值超出了1到99的范围，将发生设置S17=1。然而，如果CALL指令正常执行，则将发生设置S17=0。因此，在应该有必要的子梯级的情况下，可以通过在调用后使用S17来检测错误。  
如果在主梯级程序中使用CALL指令调用编号从1到99的子梯级，并为每个应用分配子梯级编号是可能的，我们可以预期通过控制器根据每个应用自动加载必要的子梯级程序，从而执行与应用相关的梯级程序。


![](../_assets/call.png)
[__SOURCE](4-instruction/35-end.md)
# 4.35 END (End): 结束梯形程序

### Description
如果程序段处于活动状态，则当前正在执行的梯形程序将被结束。 
如果当前梯形程序是子梯形程序，则将返回主梯形程序。然而，如果当前梯形程序是主梯形程序，则它的执行将被结束，主梯形程序将从头开始执行。

<br>

### Example of use

如果输入 DO22 处于活动状态，则梯形程序将通过 END 指令结束，之后写出的程序段的指令将不会被执行。
如果输入 DO22 处于非活动状态，则 END 指令将不会被执行，从而允许之后写出的程序段的指令自然执行。

![](../_assets/end.png)
[__SOURCE](4-instruction/36-and.md)
# 4.36 位运算与 (AND): 位操作和

### 描述
如果梯级处于活动状态，“源 a”的值和“源 b”的值将进行按位与操作，结果值将设置在“目的地”继电器中。(支持版本为 60.28-00 和 HRLadder v2.86b1)

<br>

### 可以作为操作数使用的类型
(对 X 不可行)
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

### 使用示例

当输入 DO36 处于活动状态时，MB0 将与 &HFF 的值进行按位与操作，结果值将设置在内部状态继电器 MW8 中。

![](../_assets/and.png)
[__SOURCE](4-instruction/37-or.md)
# 4.37 位运算或 (OR)：位运算或

### 描述
如果梯级处于活动状态，"源 a" 的值和 "源 b" 的值将进行位运算或操作，结果值将设置在 "目标" 继电器中。 (支持版本为 60.28-00 和 HRLadder v2.86b1)

<br>

### 可以用作操作数的类型
(对 X 不可用)
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

当输入 DO36 处于活动状态时，DOW2 将对值 &H0F0F 进行位运算或操作，并且结果值将设置在内部状态继电器 DIL8 中。

![](../_assets/or.png)
[__SOURCE](5-diff-hi5a-hi6.md)
<script id="page-config" type="application/json">
{
	"permittedStrs": ["Hi6", "Hi7"]
}
</script>

# 5. Hi5a与Hi6/Hi7之间嵌入式PLC的区别

Hi6/Hi7控制器的嵌入式PLC功能与Hi5a控制器的嵌入式PLC功能相似，并且使用相同的HRLadder或相同的梯形编辑器。 
因此，已经熟悉Hi5a控制器嵌入式PLC功能的用户可以仅通过查看Hi6/Hi7控制器中的不同部分快速从本手册中学习。

以下内容包含不同部分的列表。

<br>

#### HRLadder在线连接

HRLadder v2.80或更高版本支持Hi6/Hi7控制器。
HRLadder早于v2.80的版本在按下在线按钮时通过自动识别控制器类型来允许远程连接。
但是，对于HRLadder v2.80或更高版本，您需要在项目的属性中选择控制器类型，然后按下在线按钮。

![](_assets/hrladder-prj-prop.png)

![](_assets/hrladder-prj-prop2.png)

<br>

#### 继电器类型

##### Hi5a

支持MW1-MW1000的M继电器。
存在特殊继电器SP。
专用输入和输出信号包含在SW中。

##### Hi6/Hi7

M继电器大幅扩展至MW0-MW19998，因此您可以将其用作其他继电器的替代品。
SP继电器集成在[S继电器-固定区域](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/zh/3-relay/4-sw-relay/1-fixed-area?cont_model=${cont_model})的特殊标志区域中。
对于专用输入和输出信号，将提供SI和SO支持。

<br>

#### 索引

##### Hi5a
索引从1开始。
字、长和浮动的索引增加1。 
例如，DO16-DO23与DOW1相同。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table class="tg">
<tbody>
  <tr>
    <td class="tg-kftd">bit</td>
    <td>DO1~DO8</td>
    <td>DO9~DO16</td>
    <td>DO17~DO24</td>
    <td>DO25~DO32</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">byte</td>
    <td>DOB1</td>
    <td>DOB2</td>
    <td>DOB3</td>
    <td>DOB4</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">word</td>
    <td colspan="2">DOW1</td>
    <td colspan="2">DOW2</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">long</td>
    <td colspan="4">DOL1</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">float</td>
    <td colspan="4">DOF1</td>
    <td>...</td>
  </tr>
</tbody>
</table>

<br>

##### Hi6/Hi7
索引从0开始。
字、长和浮动的索引将通过匹配字节位置增加。
例如，DOW以DOW0、DOW2、DOW4、DOW6...的形式增加，而DOL以DOL0、DOL4、DOL8...的形式增加。
如下面的图所示，DO16-DO23与DOW2相同。

参见[3.2 指定继电器](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/zh/3-relay/2-relay-expression?cont_model=${cont_model})

<br>

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table class="tg">
<tbody>
  <tr>
    <td class="tg-kftd">bit</td>
    <td>DO0~DO7</td>
    <td>DO8~DO15</td>
    <td>DO16~DO23</td>
    <td>DO24~DO31</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">byte</td>
    <td>DOB0</td>
    <td>DOB1</td>
    <td>DOB2</td>
    <td>DOB3</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">word</td>
    <td colspan="2">DOW0</td>
    <td colspan="2">DOW2</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">long</td>
    <td colspan="4">DOL0</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">float</td>
    <td colspan="4">DOF0</td>
    <td>...</td>
  </tr>
</tbody>
</table>

<br>

#### 系统继电器（SW 继电器）

##### Hi5a

在大多数情况下，每个监控项目都有一个固定的SW继电器索引地址。
然而，在索引地址中，SW220-249用于10个多功能插槽，并且可以将所需代码（在系统变量、主板存储空间、模拟输入/输出、日期/时间和GE变量的代码中）放入所需插槽并进行监控。

- 大多数项目: 固定区域
- 一些项目: 可选项目区域（插槽）

<br>

##### Hi6/Hi7

SB0-SB1999的区域是[S继电器固定区域](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/zh/3-relay/4-sw-relay/1-fixed-area?cont_model=${cont_model})，每个项目都有固定的索引地址，与Hi5a一样。

然而，SB2000-的区域是[可选项目区域](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/zh/3-relay/4-sw-relay/README?cont_model=${cont_model})，其中有大约900个多功能插槽，允许通过插入所需项目的指令进行使用。

几乎所有项目都将通过可选项目区域进行监控。

- 大多数项目: 可选项目区域（插槽）
- 一些项目: 固定区域