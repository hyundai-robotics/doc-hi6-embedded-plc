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