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