# 3.4.3 S relay - OP_TIME

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
		<td>GET_OP_TIME (110)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
		<td>时间基准<br>1=自初始化以来, 2=自开机以来, 3=自上一个循环以来, 4=当前循环</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>param. 3</td>
		<td>项目<br>1=电机开启, 2=运行时间, 3=移动时间, 4=等待时间, 5=延迟时间, 11=点焊时间 (焊接机 1), 12=(焊接机 2), 13=(焊接机 3), 14=(焊接机 4)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>result</td>
		<td>天数</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>毫秒</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>循环计数 / 焊接计数</td>
		<td>s4</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>