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