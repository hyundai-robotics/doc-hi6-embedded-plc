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