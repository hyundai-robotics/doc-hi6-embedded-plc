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
		<td>the shortcut key number for the teach pendant’s current app (1–9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>set</td>
		<td>the shortcut key number for the teach pendant’s target app whose state needs to be read or controlled (1–9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>get</td>
		<td>the current state value of the teach pendant’s target app<br>(-1=no operation, 0=not executed, 1=activated, 2=inactivated)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>set</td>
		<td>controlling of the teach pendant’s target app<br>
(0: no operation, 1: activated, 2: inactivated, 8: executed, 9:forced ending)<br>
* will be performed once every time the value changes.</td>
		<td>s2</td>
	</tr>
</tbody>
</table>