# 3.4.9 S 릴레이 - SPOTWELD_INFO

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
		<td>GET_SPOTWELD_INFO (2010)</td>
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
		<td>param 2</td>
		<td>gun_no (0=현재 선택된 건번호, 1~16)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td rowspan=5>result</td>
		<td>건서치 상태 (1=완료, 0=미완료)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>이동전극 마모량 x 100</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>고정전극 마모량 x 100</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>가압력 지령값 x 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>가압력 현재값 x 10</td>
		<td>s2</td>
	</tr>
</tbody>
</table>