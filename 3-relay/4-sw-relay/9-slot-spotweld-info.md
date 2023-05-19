# 3.4.9 S realy - SPOTWELD_INFO

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
		<td>GET_SPOTWELD_INFO (2010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>task_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 2</td>
		<td>gun_no (1–4)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td rowspan=5>result</td>
		<td>gun search state (1=complete, 0=incomplete)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>moving electrode consumption amount × 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>fixed electrode consumption amount × 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>squeeze force instruction value × 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>squeeze force current value × 10</td>
		<td>s2</td>
	</tr>
</tbody>
</table>