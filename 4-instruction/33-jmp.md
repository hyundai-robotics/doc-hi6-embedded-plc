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