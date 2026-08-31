# 3.4.18 S relay - FORCE_CTRL

Get information from force control. <br>
Supported from V70.04-00.

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
		<td>GET_FORCE_CTRL (4200)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>1 = Force from FT Sendor</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param. 2</td>
		<td>Data<br>0=Length(x, y, z), 1=Angle(rx, ry, rz)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=6>result</td>
		<td>Data 1</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>Data 2</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>Data 3</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>
