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