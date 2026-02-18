# 3.4.9 S realy - SPOTWELD_INFO

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
		<td>GET_SPOTWELD_INFO (2010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>枪编号 (1-4)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td rowspan=5>结果</td>
		<td>枪搜索状态 (1=完成, 0=未完成)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>移动电极消耗量 x 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
<<<SOURCE_MARKDOWN_START>>>		<td>固定电极消耗量 x 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>挤压力指令值 x 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>挤压力电流值 x 10</td>
		<td>s2</td>
	</tr>
</tbody>
</table><<<SOURCE_MARKDOWN_END>>>