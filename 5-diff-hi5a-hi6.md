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