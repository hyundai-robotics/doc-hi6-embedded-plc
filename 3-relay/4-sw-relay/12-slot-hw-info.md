# 3.4.12 S 릴레이 - HW_INFO

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
		<td>cpu 온도 * 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>메인보드 온도 * 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>시스템보드 온도 * 10</td>
		<td>s2</td>
	</tr>
</tbody>
</table>