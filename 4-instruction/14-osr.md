# 4.14 OSR (One Shot Rising): 一次上升输出

### 描述
如果梯级处于活动状态，输出信号仅会在一次扫描的持续时间内输出。换句话说，当梯级从非活动状态切换到活动状态时，相关继电器将在一次扫描的持续时间内处于ON状态。

<br>

### 可用作操作数的类型
（对于X，不可能，DO位从V60.30-07开始支持）
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

如果输入 X17 处于开启状态，内部状态继电器 M17 将处于开启状态。M17 会保持在开启状态，直到相关扫描完成，如果启动新的扫描，它将切换到关闭状态。

![](../_assets/osr.png)