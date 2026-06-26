# 3.4.4 S relay - AXIS_INFO

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
		<td>GET_AXIS_INFO (120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>类型<br>
		1 = 当前位置信息（轴角），2 = 当前位置信息（基坐标），3 = 当前位置信息（基/用户坐标）<br>
		6 = 轴速度，7 = 马达速度<br>
		8 = 当速度控制时的马达速度命令（rpm）<br>
		10 = 负载因子(I/Ir)，11 = 负载因子(I/Ip)，13 = 负载因子（持续）<br>
		15 = 编码器温度<br>
		18 = 每个轴的累计距离<br>
		111 = 位置偏差（当前），112 = 位置偏差（最大）<br>
		124 = 编码器通信失败计数<br>
	    </td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
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
		<td rowspan=3>result</td>
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

<div class="page-break"></div>

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
		<td>SET_AXIS_INFO (121)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>类型<br>8 = 当速度控制时的马达速度命令（rpm）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
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
		<td rowspan=3>result</td>
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

<div class="page-break"></div>