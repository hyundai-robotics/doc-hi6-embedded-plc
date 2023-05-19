# 3.4.2 S relay - TASK_INFO

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
		<td>GET_TASK_INFO (100)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>task_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>task in activated state</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>task program number</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>task step number</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>task function number</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>task main program number</td>
		<td>s2</td>
	</tr>	
</tbody>
</table>