# 3.4.19 S 릴레이 - MONOPUMP

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
		<td>GET_MONITOR_INFO (4100)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>gun_no (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>流量 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>rpm 命令</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>rpm 当前</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>压力 (bar)</td>
<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>流量（cc） - 车辆类型的总值</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>GET_MANUAL_OPER1 (4110)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪编号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>结果</td>
		<td>流量（cc/s）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>流量（固定量模式）（cc）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>回吸流量（cc/s）</td>
		<td>f4</td>
</tr>
	<tr>
		<td>16</td>
		<td>回吸时间 (s)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>GET_MANUAL_OPER2 (4112)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪编号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>结果</td>
		<td>延迟时间 (s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>补充流速 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>补充时间 (s)</td>
		<td>f4</td>
	</tr>
<tr>
		<td>16</td>
		<td></td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>SET_MANUAL_OPER (4111)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>设定数据项 <br>
		1 = 流量 (cc/s) <br>
		2 = 流量 (固定量模式) (cc) <br>
		3 = 吸回流量 (cc/s) <br>
		4 = 吸回时间 (s) <br>
		5 = 延迟时间 (s) <br>
		6 = 重新填充流量 (cc/s) <br>
		7 = 重新填充时间 (s)
		</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>参数 3</td>
```
		<td>值</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>10</td>
		<td>参数 4</td>
		<td>设置 = 1，设置值后强制初始化为 0</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>MANUAL_OPER (4113)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪编号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>操作项 <br>
		1 = 固定速度放电 <br>
		2 = 固定数量放电 <br>
		3 = 停止放电 <br>
		操作开始后强制初始化为 0 <br>
		</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
```
<br>

<table class="tg">
<thead>
	<tr>
		<th>S偏移</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_COND_INFO1 (4120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>条件号 (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>结果</td>
		<td></td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>流量（固定量模式）(cc)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>回吸流量（cc/s）</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
<td>吸回时间 (秒)</td>
<td>f4</td>
</tr>
</tbody>
</table>

<br>

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
		<td>GET_COND_INFO2 (4122)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>条件号 (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>结果</td>
		<td>延迟时间 (秒)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>补充流量 (cc/s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
<td>补充时间 (s)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td></td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>

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
		<td>SET_COND_INFO (4121)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>枪号 (1~2)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>条件编号 (1~8)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>参数 2</td>
		<td>设置数据项 <br>
		2 = 流量 (固定量模式) (cc) <br>
		3 = 吸回流量 (cc/s) <br>
		4 = 吸回时间 (s) <br>
		5 = 延迟时间 (s) <br>
		6 = 充填流量 (cc/s) <br>
		7 = 充填时间 (s)
		</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>参数 3</td>
		<td>值</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>10</td>
		<td>参数 4</td>
		<td>设置 = 1，设置值后强制初始化为 0</td>
		<td>s1</td>
	</tr>
</tbody>
</table>