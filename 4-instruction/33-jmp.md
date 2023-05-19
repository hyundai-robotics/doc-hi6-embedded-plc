# 4.33 JMP (Jump): Jumping


### Description
If the rung is active, there will be a jump to the location where the LBL instruction matching the value of the label designated in "label" is located. 
In particular, if "label" is specified as a value less than 0, it can be used as a feature for leaving the middle of a FOR instruction (skips according to the number specified in a negative number.)
Caution 1:  
If the location of the label is above the JMP instruction and there is no condition in front of the JMP instruction, infinite looping may occur, which will require your attention. When this occurs, the setting will be S16=1 because the scan time exceeded 5 seconds.
Caution 2:  
Leaving the block by using the JMP (positive number) instruction within the FOR/NEXT instruction block may cause the block control to go wrong. In that case, programming a way to skip to the NEXT instruction by using the JMP instruction (negative number) will be required.
Note: For more details on the LBL instruction, refer to [4.32 LBL (Label)](./32-lbl)

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

### Example of use

If the input DO19 is active, there will be a jump to the relevant LBL instruction according to the "label 99" of the JMP instruction. It means the instruction {XIC(DO20), OTE(Y20)} will not be executed.  
If the input DO19 is inactive, the JMP instruction will not be executed, so the {XIC(DO20), OTE(Y20)} instruction written in the next rung will be exeucted.


![](../_assets/jmp.png)
