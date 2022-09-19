# 3.4.8 S 릴레이 - CUR_SPOTGUN_NO

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
		<td>GET_CUR_SPOTGUN_NO (2000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>task_no (0~7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td>현재 스폿건 번호 (용접기 1, master gun)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>현재 스폿건 번호 (용접기 2, slave gun #1)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>현재 스폿건 번호 (용접기 3, slave gun #2)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>현재 스폿건 번호 (용접기 4, slave gun #3)</td>
		<td>s2</td>
	</tr>
</tbody>
</table>