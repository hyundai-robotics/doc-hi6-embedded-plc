# 3.4.8 S 继电器 - CUR_SPOTGUN_NO

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
		<td>GET_CUR_SPOTGUN_NO (2000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>task_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=12>结果</td>
		<td>当前点焊枪编号 (主枪)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>当前条件编号 (主 cnd)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>7</td>
		<td>当前序列编号 (主 seq)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>当前点焊枪编号 (从枪 #1)</td>
<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>当前条件编号 (从设备 cnd #1)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>11</td>
		<td>当前序列编号 (从设备 seq #1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>12</td>
		<td>当前点焊枪编号 (从设备 gun #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>13</td>
		<td>当前条件编号 (从设备 cnd #2)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>15</td>
		<td>当前序列编号 (从设备 seq #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>16</td>
		<td>当前点焊枪编号 (从设备 gun #3)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>17</td>
		<td>当前条件编号 (从设备 cnd #3)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>19</td>
		<td>当前序列编号 (从设备 seq #3)</td>
		<td>s1</td>
	</tr>
</tbody>
</table>