# 3.4.8 S relay - CUR_SPOTGUN_NO

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
		<td>GET_CUR_SPOTGUN_NO (2000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>任务编号 (0-7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=12>result</td>
		<td>当前喷枪号码 (主喷枪)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>当前条件号码 (主条件)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>7</td>
		<td>当前序列号码 (主序列)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>当前喷枪号码 (从喷枪 #1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>当前条件号码 (从条件 #1)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>11</td>
		<td>当前序列号码 (从序列 #1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>12</td>
		<td>当前喷枪号码 (从喷枪 #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>13</td>
		<td>当前条件号码 (从条件 #2)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>15</td>
		<td>当前序列号码 (从序列 #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>16</td>
		<td>当前喷枪号码 (从喷枪 #3)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>17</td>
		<td>当前条件号码 (从条件 #3)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>19</td>
		<td>当前序列号码 (从序列 #3)</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>