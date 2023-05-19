# 4.26 MOV (Move): Moving


### Description
If the rung is active, the value of the "source" will be copied to the "destination."
If the "source" is in the word (W) format, and the "destination" is in the byte (B) format, only the lower byte of the value of the "source" will be copied to the "destination." 
Because all data of the embedded programmable logic controller (PLC) is processed as signed data, if the "source" is in the byte (B) format and its value is -1(&Hff), this value will be copied to the "destination," which is in the word (W) format, as -1(&HFFFF) (&H00ff becomes the value of 255.)



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
    <td class='hd'>source</td>
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
    <td class='hd'>destination</td>
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

### Example of use

If the input DO55 is active, 55 will be set in the internal state relay MB2.

![](../_assets/mov.png)
