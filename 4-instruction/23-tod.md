# 4.23 TOD (Convert to BCD): Converting to BCD


### Description
If the rung is active, the value of the "source" will be converted to a BCD value, and the converted value will be stored in the "destination."
This instruction will be convenient when using a device that displays values ​​in a 7-segment display in the BCD format.
If the data type for the "destination" is in the byte (B) format, the value of the "source" will be converted to two digits. If it is in the word (W) format, the value of the "source" will be converted to four digits. However, if the value of the "source" is greater than the number of digits to convert to, the setting S6=1 will occur.

<br>

### Types that can be used as an operand
(not possible for X, unsigned integers for u)
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
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>u</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO42 is active, the value of XB3 will be converted to a BCD value, and the converted value will be set in the internal state relay MB3. 
(Note: Binary Coded Decimal (BCD) refers to numbers whose 4-bit code value can have a value ranging from 0 to 9. That is, for BCD numbers, A–F among the numbers 0–F that can be represented with 4 bits are not used.)
If &H7B(123) is converted to a BCD value, the converted value will be &H23(35), and because &H7B(123) is greater than &H63(99), the setting S6=1 will occur.


![](../_assets/tod.png)
