# 3.4.10 S relay - CONVEYOR_INFO

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
		<td>GET_CONVEYOR_INFO (4000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=7>result</td>
		<td>conveyor pulse</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>workpiece position</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>conveyor speed</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>workpiece count</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>limit switch input</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>raw pulse</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>encoder resolution</td>
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
		<td>GET_CONVEYOR_INFO_LIN (4010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>result</td>
		<td>linear conveyor horizontal angle</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>linear conveyor vertical angle</td>
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
		<td>GET_CONVEYOR_INFO_CIR (4020)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>result</td>
		<td>circular conveyor angle (X axis)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>circular conveyor angle (Y axis)</td>
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
		<td>GET_CONVEYOR_INFO_CIR2 (4040)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=3>result</td>
		<td>circular conveyor center (X)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>circular conveyor center (Y)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>circular conveyor center (Z)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
