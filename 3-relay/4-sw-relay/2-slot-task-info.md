# 3.4.2 S 릴레이 - TASK_INFO

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
		<td>GET_TASK_INFO (100)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>task_no (0~7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>task 활성화 상태</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>task 프로그램 번호</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>task 스텝 번호</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>task 펑션 번호</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>task 메인 프로그램 번호</td>
		<td>s2</td>
	</tr>	
</tbody>
</table>