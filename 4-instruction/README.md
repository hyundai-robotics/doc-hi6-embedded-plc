# 4. Instructions

A ladder program consists of multiple rungs, and each rung consists of multiple instructions.

The embedded PLC performs logical I/O operations while sequentially executing instructions in the program.

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table>
<thead>
  <tr>
    <td rowspan="11">梯子项目</td>
    <td rowspan="7">梯子程序</td>
    <td rowspan="3">横档</td>
    <td>指令</td>
  </tr>
  <tr>
    <td>指令</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">横档</td>
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
    <td rowspan="3">梯子程序</td>
    <td rowspan="2">横档</td>
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

An instruction consists of three elements, as shown below.

<table>
<thead>
  <tr>
    <th>指令 (助记符)</th>
    <th>操作类型</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>操作数</td>
    <td>操作的参数。<br>根据指令，可以指定一个或多个操作数，但有些指令没有操作数。</td>
  </tr>
  <tr>
    <td>注释</td>
    <td>为程序的可读性附加的描述。注释不会影响操作。</td>
  </tr>
</tbody>
</table>