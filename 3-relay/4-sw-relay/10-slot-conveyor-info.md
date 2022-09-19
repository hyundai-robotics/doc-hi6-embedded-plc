# 3.4.10 S 릴레이 - CONVEYOR_INFO

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
		<td>GET_CONVEYOR_INFO (4000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0~7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=7>result</td>
		<td>컨베이어 펄스</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>작업물 위치</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>컨베이어 속도</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>작업물 개수</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>리밋스위치 입력</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>raw 펄스</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>엔코더 분해능</td>
		<td>s4</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>GET_CONVEYOR_INFO_LIN (4010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0~7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>result</td>
		<td>직선컨베이어 수평각도</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>직선컨베이어 수직각도</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>GET_CONVEYOR_INFO_CIR (4020)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0~7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>result</td>
		<td>원형컨베이어 각도(X축)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>원형컨베이어 각도(Y축)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>GET_CONVEYOR_INFO_CIR2 (4040)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0~7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=3>result</td>
		<td>원형컨베이어 중심(X)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>원형컨베이어 중심(Y)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>원형컨베이어 중심(Z)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
