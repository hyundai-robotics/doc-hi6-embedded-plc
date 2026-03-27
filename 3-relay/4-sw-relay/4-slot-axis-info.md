# 3.4.4 S relay - AXIS_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_AXIS_INFO (120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>type<br>
		1 = Current position (axis angle), 2 = Current position (base coordinate), 3 = Current position (base/user coordinate)<br>
		6 = Axis speed, 7 = Motor speed<br>
		8 = Motor speed command when speed control(rpm)<br>
		10 = Load factor(I/Ir), 11 = Load factor(I/Ip), 13 = Load factor(continuous)<br>
		15 = Encoder temperature<br>
		18 = Accumulated distance for each axis<br>
		111 = Position deviation(current), 112 = Position deviation(maximum)<br>
		124 = Encoder communication failure count<br>
	    </td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
		<td>start axis number (1-)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>-</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>result</td>
		<td>relevant value (for the start axis + axis 0)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>relevant value (for the start axis + axis 1)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>relevant value (for the start axis + axis 2)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
<br>
<br>

<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>field</th>
		<th>description</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>SET_AXIS_INFO (121)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>type<br>8 = motor speed command when speed control(rpm)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
		<td>start axis number (1-)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>-</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>result</td>
		<td>relevant value (for the start axis + axis 0)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>relevant value (for the start axis + axis 1)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>relevant value (for the start axis + axis 2)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>
