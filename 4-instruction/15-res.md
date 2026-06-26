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