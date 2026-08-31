# 3.4.20 S 릴레이 - FORCE_CTRL

V70.04-00부터 지원됩니다.

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
		<td>GET_FORCE_CTRL (4200)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>1 = 힘센서 입력</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param. 2</td>
		<td>데이터<br>0=길이(x, y, z), 1=각도(rx, ry, rz)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=6>result</td>
		<td>데이터 1</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>데이터 2</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>데이터 3</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
  
<div class="page-break"></div>