# 3.4.6 S relay - TP_APP

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
		<td>当前教导挂件应用程序的快捷键编号（1-9）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>set</td>
		<td>需要读取或控制的教导挂件目标应用程序的快捷键编号（1-9）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>get</td>
		<td>教导挂件目标应用程序的当前状态值<br>(-1=无操作, 0=未执行, 1=已激活, 2=已停用)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>set</td>
		<td>对教导挂件目标应用程序的控制<br>
(0: 无操作, 1: 已激活, 2: 已停用, 8: 已执行, 9: 强制结束)<br>
* 每次值变化时将执行一次。</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>