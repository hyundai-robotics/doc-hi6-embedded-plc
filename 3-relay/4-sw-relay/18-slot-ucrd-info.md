# 3.4.18 S relay - UCRD_INFO

Get information registered in the user coordinate system. <br>
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
		<td>GET_UCRD_INFO (176)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>User coordinate number</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param. 2</td>
		<td>User coordinate data<br>0 = Length, 1=Angle</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=6>result</td>
		<td>User coordinate data X</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>User coordinate data Y</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>User coordinate data Z</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
