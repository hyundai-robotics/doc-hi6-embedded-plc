# 3.4.15 S realy - IP_INFO

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
		<td>GET_IP_INFO (172)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>局域网 (1~3)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=6>结果</td>
		<td>IP - 1</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>IP - 2</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>IP - 3</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>IP - 4</td>
<td>s2</td>
	</tr>
</tbody>
</table>