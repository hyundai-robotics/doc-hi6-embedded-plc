# 3.4.13 S realy - HW_INFO

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
		<td>GET_HW_INFO (170)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td rowspan=6>result</td>
		<td>cpu temperature * 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>main board temperature * 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>system board temperature * 10</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>
