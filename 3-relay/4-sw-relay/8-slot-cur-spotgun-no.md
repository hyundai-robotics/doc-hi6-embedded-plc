# 3.4.8 S 릴레이 - CUR_SPOTGUN_NO

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
		<td>task_no (0~7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=12>result</td>
		<td>현재 스폿건 번호 (master gun)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>현재 조건 번호 (master cnd)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>7</td>
		<td>현재 시퀀스 번호 (master seq)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>현재 스폿건 번호 (slave gun #1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>현재 조건 번호 (slave cnd #1)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>11</td>
		<td>현재 시퀀스 번호 (slave gun #1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>12</td>
		<td>현재 스폿건 번호 (slave gun #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>13</td>
		<td>현재 조건 번호 (slave cnd #2)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>15</td>
		<td>현재 시퀀스 번호 (slave gun #2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>16</td>
		<td>현재 스폿건 번호 (slave gun #3)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>17</td>
		<td>현재 조건 번호 (slave cnd #3)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>19</td>
		<td>현재 시퀀스 번호 (slave gun #3)</td>
		<td>s1</td>
	</tr>
</tbody>
</table>