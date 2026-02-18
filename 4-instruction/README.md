# 4. 指示

梯形图程序由多个梯级组成，每个梯级由多个指令组成。

嵌入式 PLC 在顺序执行程序中的指令时执行逻辑输入/输出操作。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table>
<thead>
  <tr>
    <td rowspan="11">ladder project</td>
    <td rowspan="7">ladder program</td>
    <td rowspan="3">rung</td>
    <td>指令</td>
  </tr>
  <tr>
    <td>指令</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">rung</td>
    <td>指令</td>
  </tr>
  <tr>
    <td>指令</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td>...</td>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">ladder program</td>
    <td rowspan="2">rung</td>
    <td>指令</td>
  </tr>
  <tr>
    <td>指令</td>
  </tr>
  <tr>
<td>...</td>
    <td>...</td>
  </tr>
  <tr>
    <td>...</td>
    <td>...</td>
    <td>...</td>
  </tr>
</thead>
</table>

<br><br>

指令由三个元素组成，如下所示。

<table>
<thead>
  <tr>
    <th>指令（助记符）</th>
    <th>操作类型</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>操作数</td>
    <td>操作的参数。<br>根据指令，可以指定一个或多个操作数，但某些指令没有操作数。</td>
  </tr>
  <tr>
    <td>注释</td>
    <td>用于提高程序可读性的描述。注释不影响操作。</td>
  </tr>
</tbody>
</table>