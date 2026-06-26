# 3.4.11 S relay - CONVEYOR_INFO

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
		<td>获取输送带信息 (4000)</td>
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
		<td rowspan=7>result</td>
		<td>输送带脉冲</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>工件位置</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>输送带速度</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>工件数量</td>
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
		<td>获取输送带信息_LIN (4010)</td>
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
		<td rowspan=2>result</td>
		<td>线性输送带水平角度</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>线性输送带垂直角度</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>获取输送带信息_CIR (4020)</td>
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
		<td rowspan=2>result</td>
		<td>圆形输送带角度 (X 轴)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>圆形输送带角度 (Y 轴)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>获取输送带信息_CIR2 (4040)</td>
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
		<td rowspan=3>result</td>
		<td>圆形输送带中心 (X)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>圆形输送带中心 (Y)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>圆形输送带中心 (Z)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>