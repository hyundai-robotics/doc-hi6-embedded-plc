# 3.4.17 S 继电器 - 工具信息

获取工具数据中设定的信息。 <br>
支持版本 V60.30-01。

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
		<td>GET_TOOL_INFO (174)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>工具编号</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>工具数据<br>0 = 长度, 1=角度, 2=中心, 3=惯性</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>结果</td>
		<td>工具重量</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>工具数据 X</td>
		<td>f4</td>
</tr>
	<tr>
		<td>12</td>
		<td>工具数据 Y</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>工具数据 Z</td>
		<td>f4</td>
	</tr>
</tbody>
</table>