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