# 3.4.17 S relay - TOOL_INFO

Get the information set in the tool data. <br>
Supported from V60.30-01.

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
		<td>GET_TOOL_INFO (174)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>Tool number</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param. 2</td>
		<td>Tool data<br>0 = Length, 1=Angle, 2=Center, 3=Inertia</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>result</td>
		<td>Tool weight</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>Tool data X</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>Tool data Y</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>Tool data Z</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
