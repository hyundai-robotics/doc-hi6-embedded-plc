# 3.4.17 S relay - TOOL_INFO

获取工具数据中设置的信息。 <br>
支持从 V60.30-01 开始。

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
		<td>工具编号</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param. 2</td>
		<td>工具数据<br>0 = 长度, 1=角度, 2=中心, 3=惯性</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>result</td>
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

<div class="page-break"></div>