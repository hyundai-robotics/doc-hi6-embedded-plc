# 3.4.17 S 릴레이 - TOOL_INFO

툴 데이터에 설정된 정보를 얻습니다. <br>
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
		<td>GET_TOOL_INFO (174)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>툴 번호</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param. 2</td>
		<td>툴 데이터<br>0 = 길이, 1=각도, 2=중심, 3=이너셔</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>result</td>
		<td>툴 중량</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>툴 데이터 X값</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>툴 데이터 Y값</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>툴 데이터 Z값</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
  
<div class="page-break"></div>
