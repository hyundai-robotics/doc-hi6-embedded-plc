# 3.4.5 S 继电器 - TP_KEYPAD

Supported from V60.30-07

<style type="text/css">
	table  {border-collapse:collapse;}
	th, td {
		border: 1px solid black;
		text-align: center;
		width: 9%;
		height: 3rem;
	}
	.grayed {
		background-color: lightgray;
	}
	.jog {
		color: black;
		background-color: rgb(255, 240, 200);
	}
	.fkey {
		color: black;
		background-color: rgb(210, 230, 200);
	}
	.opkey {
		color: black;
		background-color: rgb(240, 240, 150);
	}
	.spkey {
		color: black;
		background-color: rgb(250, 180, 170);
	}
	.num {
		color: black;
		background-color: rgb(240, 240, 240);
	}
	.arrow {
		color: black;
		background-color: lightgreen;
	}
	.ent {
		color: black;
		background-color: rgb(185, 250, 255);
	}
</style>

<table class="tg">
<thead>
	<tr>
		<th>SB offset</th>
		<th>byte\bit</th>
		<th>7</th>
		<th>6</th>
		<th>5</th>
		<th>4</th>
		<th>3</th>
		<th>2</th>
		<th>1</th>
		<th>0</th>
		<th>type</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>command</td>
		<td colspan='8'>GET_TP_KEYPAD (130)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>-</td>
		<td colspan='8'></td>
		<td></td>
	</tr>
	<tr>
		<td>3</td>
		<td>[0]</td>
		<td class='jog'>J4-</td>
		<td class='jog'>J5-</td>
		<td class='jog'>J1-</td>
		<td class='jog'>J2-</td>
		<td class='jog'>J3-</td>
		<td class='jog'>J1+</td>
		<td class='jog'>J2+</td>
		<td class='jog'>J3+</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>[1]</td>
		<td class='ent'>SHIFT</td>
		<td class='arrow'>&larr;</td>
		<td class='jog'>J6-</td>
		<td class='jog'>J4+</td>
		<td class='jog'>J5+</td>
		<td class='jog'>J6+</td>
		<td class='jog'>Step<br>FWD</td>
		<td class='jog'>Step<br>BWD</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>[2]</td>
		<td>设置</td>
		<td></td>
		<td>机器人<br>移动</td>
		<td></td>
		<td></td>
		<td>SHIFT+1</td>
		<td>SHIFT+3</td>
		<td>SHIFT+2</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>[3]</td>
		<td class='fkey'>F7</td>
		<td class='fkey'>F6</td>
		<td class='fkey'>F5</td>
		<td class='fkey'>F4</td>
		<td class='fkey'>F3</td>
		<td class='fkey'>F2</td>
		<td class='fkey'>F1</td>
		<td></td>
		<td>u1</td>
	</tr>
	<tr>
		<td>7</td>
		<td>[4]</td>
		<td>退格</td>
		<td>虚拟<br>TP</td>
		<td class='ent'>CTRL</td>
		<td class='opkey'>mode2</td>
		<td class='opkey'>mode1</td>
		<td class='opkey'>停止</td>
		<td class='opkey'>开始</td>
		<td class='opkey'>电机<br>开启</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>[5]</td>
		<td class='num'>7</td>
		<td class='num'>6</td>
		<td class='num'>5</td>
		<td class='num'>4</td>
		<td class='num'>3</td>
		<td class='num'>2</td>
		<td class='num'>1</td>
		<td class='num'>0</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>[6]</td>
		<td class='arrow'>&darr;</td>
		<td class='arrow'>&uarr;</td>
		<td class='arrow'>&rarr;</td>
		<td class='ent'>R</td>
		<td class='ent'>ENTER</td>
		<td class='ent'>ESC</td>
		<td class='num'>9</td>
		<td class='num'>8</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>[7]</td>
		<td class='spkey'>速度<br>.低</td>
		<td class='spkey'>速度<br>.高</td>
		<td class='spkey'>REC</td>
		<td class='spkey'>步骤</td>
		<td class='spkey'>机械</td>
		<td class='spkey'>枪</td>
		<td class='spkey'>坐标</td>
		<td></td>
		<td>u1</td>
	</tr>
	<tr>
		<td>11</td>
		<td>[8]</td>
		<td class='spkey'>历史</td>
		<td class='num'>.</td>
		<td></td>
		<td>对齐<br>移动</td>
		<td class='jog'>J8+</td>
		<td class='jog'>J8-</td>
		<td class='jog'>J7+</td>
		<td class='jog'>J7-</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>12</td>
		<td>[9]</td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td>u1</td>
	</tr>
	<tr>
		<td>13</td>
		<td>[10]</td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td></td>
		<td>u1</td>
	</tr>
	<tr>
		<td>14</td>
		<td>[11]</td>
		<td colspan='8'>序列号</td>
		<td>u1</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>