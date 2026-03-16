# 3.4.18 S 릴레이 - UCRD_INFO

V60.30-01부터 지원됩니다.

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
		<td>사용자좌표계 번호</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param. 2</td>
		<td>사용자좌표계 데이터<br>0 = 길이, 1=각도</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=6>result</td>
		<td>사용자좌표계 데이터 X값</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>사용자좌표계 데이터 Y값</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>사용자좌표계 데이터 Z값</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
  
<div class="page-break"></div>