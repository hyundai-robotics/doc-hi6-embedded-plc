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
    <td rowspan="11">ladder project</td>
    <td rowspan="7">ladder program</td>
    <td rowspan="3">rung</td>
    <td>instruction</td>
  </tr>
  <tr>
    <td>instruction</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">rung</td>
    <td>instruction</td>
  </tr>
  <tr>
    <td>instruction</td>
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
    <td>instruction</td>
  </tr>
  <tr>
    <td>instruction</td>
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
    <th>instruction (mnemonic)</th>
    <th>type of operation</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>operand</td>
    <td>Argument of an operation.<br>Depending on the instruction, one or multiple operands can be designated, but some instructions do not have operands.</td>
  </tr>
  <tr>
    <td>comments</td>
    <td>Description attached for the readability of a program. Comments do not affect operations.</td>
  </tr>
</tbody>
</table>


