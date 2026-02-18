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