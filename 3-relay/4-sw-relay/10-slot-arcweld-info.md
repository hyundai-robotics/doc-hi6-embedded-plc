# 3.4.10 S 릴레이 - ARCWELD_INFO

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
		<td>GET_ARCTWELD_INFO (3000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>용접 전류</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>용접 전압</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>용접기 에러</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>와이어 피딩속도</td>
		<td>f4</td>
	</tr>
</tbody>
</table>