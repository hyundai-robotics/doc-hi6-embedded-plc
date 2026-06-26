# 4.34 CALL (Call): 调用子梯级程序


### 描述
如果梯级处于活动状态，将调用由“文件编号”指定的编号（1到99）的子梯级程序。
子梯级程序最多可以有99个文件名，范围从 S01xxxx.LAD 到 S99xxxx.LAD，对于文件名的“xxxx”部分，用户可以任意添加最多15个字符。

<br>

### 可以用作操作数的类型
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
    <th colspan="2">内存<br>M, S</th>
    <th>常数<br>32位</th>
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

当输入DO21处于活动状态时，将按顺序调用编号从S01xxxx.LAD到S99xxxx.LAD的文件。
执行CALL指令的结果是，如果与该数字相关的子梯级程序不存在，或者数字的值超出了1到99的范围，将发生设置S17=1。然而，如果CALL指令正常执行，则将发生设置S17=0。因此，在应该有必要的子梯级的情况下，可以通过在调用后使用S17来检测错误。  
如果在主梯级程序中使用CALL指令调用编号从1到99的子梯级，并为每个应用分配子梯级编号是可能的，我们可以预期通过控制器根据每个应用自动加载必要的子梯级程序，从而执行与应用相关的梯级程序。


![](../_assets/call.png)