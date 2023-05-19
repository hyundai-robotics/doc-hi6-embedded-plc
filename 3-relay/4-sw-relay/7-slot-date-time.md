# 3.4.7 S relay - DATE_TIME

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
		<td>GET_DATE_TIME (150)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td rowspan=6>result</td>
		<td>year (e.g., 2022)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>month (1–12)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>date (1–31)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>hour (0–23)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>minute (0–59)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>second (0–59)</td>
		<td>s2</td>
	</tr>
</tbody>
</table>