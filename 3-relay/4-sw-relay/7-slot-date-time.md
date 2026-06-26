# 3.4.7 S relay - DATE_TIME

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
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_DATE_TIME (150)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td rowspan=6>结果</td>
		<td>年份 (例如: 2022)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>月份 (1-12)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>日期 (1-31)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>小时 (0-23)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>分钟 (0-59)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>秒 (0-59)</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>