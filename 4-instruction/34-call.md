# 4.34 CALL (Call): Calling a Sub-ladder Program


### Description
If the rung is active, the sub-ladder program with a number (1 to 99) designated by the "file number" will be called.
There can be up to 99 file names for the sub-ladder program, which can range from S01xxxx.LAD to S99xxxx.LAD, and for the "xxxx" section of the file name, the user can arbitrarily add up to 15 characters.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
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

### Example of use

When the input DO21 is active, files numbered from S01xxxx.LAD to S99xxxx.LAD will be called in rotation.
As a result of executing the CALL instruction, if no sub-ladder program relevant to the number exists or the value of the number is outside of the range of 1 to 99, the setting S17=1 will occur. However, if the CALL instruction is executed normally, the setting S17=0 will occur. Therefore, in cases where there should be a necessary sub-ladder, it is possible to detect errors by using S17 after calling.  
If calling the sub-ladders numbering from 1 to 99 with the CALL instruction in the main ladder program and assigning a sub-ladder number for each application are possible, we can expect a ladder program relevant to the application to be executed automatically by loading the necessary sub-ladder program via the controller depending on each application.


![](../_assets/call.png)
