# 3.4.13 S realy - HW_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>S 偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_HW_INFO (170)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td rowspan=6>结果</td>
		<td>CPU 温度 * 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>主板温度 * 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>系统板温度 * 10</td>
		<td>s2</td>
	</tr>
</tbody>
</table>