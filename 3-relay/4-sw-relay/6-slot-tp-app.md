# 3.4.6 S 릴레이 - TP_APP

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
		<td>GETSET_TP_APP (140)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>get</td>
		<td>현재 TP app의 단축키 번호 (1~9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>set</td>
		<td>상태를 읽거나 제어할 대상 TP app의 단축키 번호 (1~9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>get</td>
		<td>대상 TP app의 상태 현재값<br>(-1=없음, 0=미실행, 1=활성, 2=비활성)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>set</td>
		<td>대상 TP app 상태 제어<br>
(0:동작없음, 1:활성, 2:비활성, 8: 실행, 9:강제종료)<br>
* 값이 변할 때마다 1번씩만 수행됨.</td>
		<td>s2</td>
	</tr>
</tbody>
</table>