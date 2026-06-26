# 4.28 条件复制数据 (CCOP)：条件复制

### 描述
根据梯级的状态，将从“源 a”或“源 b”的位置复制值到“目标”的位置，数量与“长度”相等。
如果“源”是数字，则“目标”将根据“长度”的值填充相应的值。在这种情况下，当“目标”处于位格式时，如果相应的值为0，“目标”将填充为OFF；如果相应的值不为0，“目标”将填充为ON。
如果“源”是继电器，则“源”和“目标”的数据类型应相同。也就是说，如果“源”是位格式，则“目标”应该是位格式；如果“源”是字节（B）格式，则“目标”应该是字节（B）格式；如果“源”是字（W）格式，则“目标”也应该是字（W）格式。
如果“源” + “长度”大于“源”继电器的最大数量，或者“目标” + “长度”大于“目标”继电器的最大数量，则复制将仅执行到最大继电器的数量。

<br>

### 可以用作操作数的类型
(对于 X 不可能)
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
    <td class='hd'>源 a</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>源 b</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>目标</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>长度</td>
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

如果输入 DO57 被激活，则相应于 4 字节的值将从输入 DOB2 复制到输出 YB2，作为相应于 4 字节的值。相反，如果输入 DO57 被激活，则相应于 4 字节的值将从输入 DOB12 复制到输出 YB2，作为相应于 4 字节的值。

![](../_assets/ccop.png)