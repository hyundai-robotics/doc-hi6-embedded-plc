# 4.4.4 S 릴레이 - AXIS_INFO

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
		<td>type<br>1 = 현재위치(축각도), 2 = 현재위치(베이스좌표계), 6 = 축속도,
7 = 모터속도, 10 = 부하율(I/Ir), 11 = 부하율(I/Ip), 12 = 부하율(연속),
15 = 엔코더(온도), 18 = 축별누적거리</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
		<td>시작 축 번호 (1~)</td>
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
		<td>(시작축 + 0축) 해당값</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>(시작축 + 1축) 해당값</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>(시작축 + 2축) 해당값</td>
		<td>f4</td>
	</tr>
</tbody>
</table>