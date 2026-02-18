# 3.4.6 S 继电器 - TP_APP

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
		<td>GETSET_TP_APP (140)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>获取</td>
		<td>教导挂件当前应用的快捷键编号 (1-9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>设置</td>
		<td>教导挂件目标应用的快捷键编号，状态需要被读取或控制 (1-9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>获取</td>
		<td>教导挂件目标应用的当前状态值<br>(-1=无操作, 0=未执行, 1=已激活, 2=未激活)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>设置</td>
		<td>控制教导挂件的目标应用<br>
(0: 无操作, 1: 已激活, 2: 未激活, 8: 已执行, 9: 强制结束)<br>
* 每当值变化时将执行一次。</td>
		<td>s2</td>
</tr>
</tbody>
</table>