# 4.4.7 S 릴레이 - DATE_TIME

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
		<td>년 (e.g. 2022)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>월 (1~12)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>일 (1~31)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>시 (0~23)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>분 (0~59)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>초 (0~59)</td>
		<td>s2</td>
	</tr>
</tbody>
</table>