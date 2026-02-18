# 3.4.10 S 继电器 - CONVEYOR_INFO

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
		<td>GET_CONVEYOR_INFO (4000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>conv_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=7>结果</td>
		<td>输送机脉冲</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>工件位置</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>输送机速度</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>工件数量</td>
```html
<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>限位开关输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>原始脉冲</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>编码器分辨率</td>
		<td>s4</td>
	</tr>
</tbody>
</table>

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
		<td>GET_CONVEYOR_INFO_LIN (4010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>conv_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>结果</td>
		<td>线性输送机水平角度</td>
		<td>f4</td>
```
</tr>
	<tr>
		<td>8</td>
		<td>线性输送机垂直角度</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

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
		<td>GET_CONVEYOR_INFO_CIR (4020)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>conv_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>结果</td>
		<td>圆形输送机角度 (X 轴)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>圆形输送机角度 (Y 轴)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S offset</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td>GET_CONVEYOR_INFO_CIR2 (4040)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=3>结果</td>
		<td>圆形输送机中心 (X)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>圆形输送机中心 (Y)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>圆形输送机中心 (Z)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>