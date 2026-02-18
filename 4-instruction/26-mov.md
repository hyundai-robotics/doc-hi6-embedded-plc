# 4.26 MOV (移动): 移动

### 描述
如果梯级处于活动状态，则“源”的值将被复制到“目标”。
如果“源”是字（W）格式，且“目标”是字节（B）格式，则“源”值的低字节将被复制到“目标”。
由于嵌入式可编程逻辑控制器（PLC）的所有数据都作为有符号数据处理，如果“源”是字节（B）格式且其值为-1（&Hff），则该值将以-1（&HFFFF）复制到“目标”，该“目标”为字（W）格式（&H00ff变为255的值）。

<br>

### 可以作为操作数使用的类型
（X不可能）
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
    <th>比特</th>
    <th>B,W,L,F</th>
    <th>比特</th>
    <th>B,W,L,F</th>
    <th>比特</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>源</td>
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
    <td class='hd'>目标</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果输入DO55处于活动状态，则将55设置在内部状态继电器MB2中。

![](../_assets/mov.png)