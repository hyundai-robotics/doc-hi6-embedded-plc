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
		<td>type<br>1 = current position (axis angle), 2 = current position (base coordinate), 6 = axis speed,
7 = motor speed, 10 = load factor (I/Ir), 11 = load factor (I/Ip), 12 = load factor (continuous),
15 = encoder (temperature), 18 = accumulated distance for each axis</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
		<td>start axis number (1–)</td>
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