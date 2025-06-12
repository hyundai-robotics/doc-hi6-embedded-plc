# 3.4.19 S 릴레이 - MONOPUMP

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
		<td>GET_MONITOR_INFO (4100)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>토출비 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>rpm 지령값</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>rpm 현재값</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>압력 (bar)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>토출량 (cc) - 차종에 대한 합산 값</td>
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
		<td>GET_MANUAL_OPER1 (4110)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td>토출비 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>토출량(정액 모드) (cc)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>석백 토출비 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>석백 시간 (s)</td>
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
		<td>GET_MANUAL_OPER2 (4112)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td>지연시간 (s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>리필 토출비 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>리필 시간 (s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td></td>
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
		<td>SET_MANUAL_OPER (4111)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 2</td>
		<td>선택 항목 <br>
		1 = 토출비 (cc/s) <br>
		2 = 토출량(정액 모드) (cc) <br>
		3 = 석백 토출비 (cc/s) <br>
		4 = 석백 시간 (s) <br>
		5 = 지연시간 (s) <br>
		6 = 리필 토출비 (cc/s) <br>
		7 = 리필 시간 (s)
		</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>param 3</td>
		<td>설정값</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>10</td>
		<td>param 4</td>
		<td>설정 = 1, 값을 설정한 후 강제로 0으로 초기화</td>
		<td>s1</td>
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
		<td>MANUAL_OPER (4113)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 2</td>
		<td>동작 항목 <br>
		1 = 정속토출 <br>
		2 = 정량토출 <br>
		3 = 토출정지 <br>
		동작을 시작한 후 강제로 0으로 초기화 <br>
		</td>
		<td>s2</td>
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
		<td>GET_COND_INFO1 (4120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>cnd_no (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td></td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>토출량(정액 모드) (cc)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>석백 토출비 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>석백 시간 (s)</td>
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
		<td>GET_COND_INFO2 (4122)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>cnd_no (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td>지연시간 (s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>리필 토출비 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>리필 시간 (s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td></td>
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
		<td>SET_COND_INFO (4121)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>cnd_no (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 2</td>
		<td>선택 항목 <br>
		2 = 토출량(정액 모드) (cc) <br>
		3 = 석백 토출비 (cc/s) <br>
		4 = 석백 시간 (s) <br>
		5 = 지연시간 (s) <br>
		6 = 리필 토출비 (cc/s) <br>
		7 = 리필 시간 (s)
		</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>param 3</td>
		<td>설정값</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>10</td>
		<td>param 4</td>
		<td>설정 = 1, 값을 설정한 후 강제로 0으로 초기화</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
