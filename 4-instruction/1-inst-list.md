# 4.1 List of Instructions


<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

### * Rung and branch
<br>

<table>
<thead>
  <tr>
    <th>Mnemonic</th>
    <th>Name</th>
    <th>Symbol</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>RUNG</td>
    <td>Rung</td>
    <td>├─┤</td>
    <td>rung</td>
  </tr>
  <tr>
    <td>BST</td>
    <td>Branch Start</td>
    <td>┬─</td>
    <td>start of a branch</td>
  </tr>
  <tr>
    <td>BND</td>
    <td>Branch End</td>
    <td>─┬</td>
    <td>end of a branch</td>
  </tr>
  <tr>
    <td>NXB</td>
    <td>Nested Branch</td>
    <td>└,├</td>
    <td>nest of a branch</td>
  </tr>
</tbody>
</table>

<br><br>  

### * Logic examination instructions: If the examination result is true, the rung is active. If false, the rung is inactive. 
<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>XIC</td>
		<td>Examine if Closed</td>
		<td>-| |-</td>
		<td>examines if the contact is closed (contact A)</td>
	</tr>
	<tr>
		<td>XIO</td>
		<td>Examine if Open</td>
		<td>-|/|-</td>
		<td>examines if the contact is open (contact B)</td>
	</tr>
	<tr>
		<td>INV</td>
		<td>Inverting</td>
		<td>-//-</td>
		<td>inverts the result of the rung (inverting)</td>
	</tr>
	<tr>
		<td>EQU</td>
		<td>Inverting</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if equal (=)</td>
	</tr>
	<tr>
		<td>NEQ</td>
		<td>Inverting</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if not equal (<>)</td>
	</tr>
	<tr>
		<td>LES</td>
		<td>Less Than</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if less than (<)</td>
	</tr>
	<tr>
		<td>GRT</td>
		<td>Greater Than</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if greater than (>)</td>
	</tr>
	<tr>
		<td>LEQ</td>
		<td>Less Than or Equal</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if less than or equal (<=)</td>
	</tr>
	<tr>
		<td>GEQ</td>
		<td>Greater Than or Equal</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if greater than or equal (>=)</td>
	</tr>
</tbody>
</table>

<br><br>  

### * Output instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>OTE</td>
		<td>Output Energize</td>
		<td>-( )-</td>
		<td>the state of the rung (active: ON/inactive: OFF) will be outputted</td>
	</tr>
	<tr>
		<td>OTL</td>
		<td>Output Latch</td>
		<td>-(L)-</td>
		<td>if the rung is active, the output signal will be outputted in the ON (high) state</td>
	</tr>
	<tr>
		<td>OTU</td>
		<td>Output Unlatch</td>
		<td>-(U)-</td>
		<td>if the rung is active, the output signal will be outputted in the OFF (low) state</td>
	</tr>
	<tr>
		<td>OSR</td>
		<td>One Shot Rising</td>
		<td>-(OSR)-</td>
		<td>if the rung is active, the output signal will be outputed in the ON state only for the duration of one scan</td>
	</tr>
	<tr>
		<td>RES</td>
		<td>Reset</td>
		<td>-(RES)-</td>
		<td>if the rung is active, the timer or counter will be reset</td>
	</tr>
</tbody>
</table>



<br><br>  

### * Timer and counter instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TON</td>
		<td>Time ON delay</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>the timer operates only while the rung is active</td>
	</tr>
	<tr>
		<td>CTD</td>
		<td>Count Down</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>the rung's activation (inactive -> active) will be counted down</td>
	</tr>
</tbody>
</table>


<br><br>  

### * Arithmetic operation instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>ADD</td>
		<td>Add</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>addition (+) operation if the rung is active</td>
	</tr>
	<tr>
		<td>SUB</td>
		<td>Subtract</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>subtraction (-) operation if the rung is active</td>
	</tr>
	<tr>
		<td>MUL</td>
		<td>Multiply</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>multiplication (x) operation if the rung is active</td>
	</tr>
	<tr>
		<td>DIV</td>
		<td>Divide</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>division (/) operation if the rung is active</td>
	</tr>
	<tr>
		<td>POW</td>
		<td>Power</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>power (^) operation if the rung is active</td>
	</tr>
</tbody>
</table>




<br><br>  

### * Data conversion instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TOD</td>
		<td>convert an integer to BCD</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, the integer will be converted to BCD</td>
	</tr>
	<tr>
		<td>FRD</td>
		<td>convert BCD to an inetger</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, BCD will be converted to an integer</td>
	</tr>
	<tr>
		<td>SEG</td>
		<td>7-segment</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, conversion to a 7-segment value will occur</td>
	</tr>
</tbody>
</table>


<br><br>  

### * Move and Copy instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>MOV</td>
		<td>Move</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, one piece of data will be copied</td>
	</tr>
	<tr>
		<td>COP</td>
		<td>Copy data</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, multiple pieces of data will be copied</td>
	</tr>
	<tr>
		<td>CCOP</td>
		<td>Conditional copy data</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>multiple pieces of data will be copied depending on the state of the rung</td>
	</tr>
	<tr>
		<td>ROT</td>
		<td>Rotating output</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, sequential outputting will occur</td>
	</tr>
</tbody>
</table>

<br><br>  


### * Block control instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>FOR</td>
		<td>FOR loop</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, execution in repetition will occur until Next</td>
	</tr>
	<tr>
		<td>NEXT</td>
		<td>NEXT loop</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>jumping to the FOR instruction will occur if the count is within the repetition count</td>
	</tr>
	<tr>
		<td>LBL</td>
		<td>LabeL</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>a position to jump to according to the JMP instruction will be designated</td>
	</tr>
	<tr>
		<td>JMP</td>
		<td>Jump</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, jumping to the LBL position will occur<br>
		(skipping to -n NEXTs if Label&lt;0)</td>
	</tr>
	<tr>
		<td>CALL</td>
		<td>Call</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, a sub-ladder will be called</td>
	</tr>
	<tr>
		<td>END</td>
		<td>End</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, the sub-ladder will end</td>
	</tr>
</tbody>
</table>