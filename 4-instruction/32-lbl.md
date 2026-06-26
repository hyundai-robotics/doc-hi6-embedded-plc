# 4.32 LBL (标签): 指定标签


### 描述
使用JMP指令跳转的标签位置将指定为一个大于0的数字（const）。 
LBL指令将指定该位置，无论梯级是否处于活动状态。
注意：有关JMP指令的更多详情，请参阅 [4.33 JMP (跳转)](./33-jmp)

<br>

### 可以用作操作数的类型
（X不可用）
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
    <th>const.<br>32位</th>
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
    <td class='hd'>标签</td>
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

因为这些指令将与JMP命令一起使用，所以请参考JMP指令的描述。