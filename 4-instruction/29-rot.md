# 4.29 ROT (旋转输出): 旋转输出


### 描述
如果 rung 是活动的，除了 0 以外的继电器值将在 "计数" 范围内从 "起始继电器" 输入到 "输出继电器"，持续时间为 "重复时间"。如果 "复位继电器" 有信号输入，"起始继电器" 将根据 "计数" 的数量填充 0，计时器的值将初始化为 "重复时间" 的值，"输出继电器" 将输出 0。此指令可非常方便用于需要在只有一个设备可用于输出错误号的情况下，输出指定时间内的错误号，即使有多种类型的错误可能发生。

<br>

### 可用作操作数的类型
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
    <th colspan="2">计时器<br>T</th>
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
    <th>位</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>起始继电器</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>计数</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>计时器继电器</td>
    <td>X</td>
    <td>X</td>
    <td>x</td>
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
    <td class='hd'>重复时间</td>
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
    <td class='hd'>输出继电器</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>复位继电器</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>临时继电器</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 使用示例

如果存在与错误条件 1 至 3 相关的一个或多个错误，错误号将存储在 MW50-MW55。这里，当输入 DO58 活动时，ROT 指令生成的错误号将存储在 MW70 中 2 秒，同时该数字将通过 TOD 指令转换为 BCD 值，并依次在连接到 YB3 的显示设备上显示。如果连接用于外部错误复位信号的 X3 有输入信号，存储错误号的 MW51-MW55 的内容将清除为 0，并且 MW70 和 MW80 也将清除为 0，显示设备相应地指示为 0。

![](../_assets/rot.png)