# 3.4.4 S 继电器 - AXIS_INFO

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
		<td>GET_AXIS_INFO (120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>类型<br>1 = 当前坐标（轴角度），2 = 当前坐标（基坐标），3 = 当前坐标（基/用户坐标），<br> 6 = 轴速度,
7 = 电机速度，8 = 速度控制时的电机速度命令（rpm）<br> 10 = 负载系数 (I/Ir)，11 = 负载系数 (I/Ip)，12 = 负载系数（持续），<br>
15 = 编码器（温度），<br> 18 = 每个轴的累计距离</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>起始轴编号（1-）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>-</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>结果</td>
		<td>相关值（对于起始轴 + 轴 0）</td>
		<td>f4</td>
</tr>
	<tr>
		<td>12</td>
		<td>相关值（用于起始轴 + 轴 1）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>相关值（用于起始轴 + 轴 2）</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
<br>
<br>

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
		<td>SET_AXIS_INFO (121)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>类型<br>8 = 当速度控制时的电机速度命令（rpm）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>起始轴号（1-）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>-</td>
<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>结果</td>
		<td>相关值（对于起始轴 + 轴 0）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>相关值（对于起始轴 + 轴 1）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>相关值（对于起始轴 + 轴 2）</td>
		<td>f4</td>
	</tr>
</tbody>
</table>