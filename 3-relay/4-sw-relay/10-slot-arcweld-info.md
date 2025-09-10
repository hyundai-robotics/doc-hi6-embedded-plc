# 3.4.10 S realy - ARCWELD_INFO

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
		<td>GET_ARCTWELD_INFO (3000) - input</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>welding current</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>welding voltage</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>welder error</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>wire feeding speed</td>
		<td>f4</td>
	</tr>
</tbody>
</table>



<br>
The following services are supported from V60.32-00 onwards.
<br>
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
		<td>GET_ARCTWELD_INFO (3001) - input</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>feed motor current</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>seam tracking data</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>welding process</td>
		<td>s2</td>
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
		<td>GET_ARCTWELD_INFO (3002) - input</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>Welder total operation time(s)</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>Welder firmware version - Lower digit(Vx.x.255)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>Welder firmware version - Middle digit(Vx.255.x)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>Welder firmware version - High digit(V255.x.x)</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
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
		<td>GET_ARCTWELD_INFO (3004) - input</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>
			0x01 = WCR(wire contact relay) <br>
			0x02 = Torch collision <br>
			0x04 = Power source ok <br>
			0x08 = Wire sticked <br>
			0x10 = Welder error <br>
			0x20 = Process active <br>
			0x40 = Comm ready <br>
			0x80 = Wire use possible <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = Torch status <br>
			0x02 = Inching status <br>
			0x04 = Retract status <br>
			0x08 = Gas check <br>
			0x10 = Synergic avaliable <br>
			0x20 = Limit status <br>
			0x40 = Setting over range <br>
		</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
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
		<td>GET_ARCTWELD_INFO (3005) - output</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>welder current</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>welder voltage</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>Job/Prog no</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>Operation mode</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>Synergic code</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<br>
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
		<td>GET_ARCTWELD_INFO (3006) - output</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>Pulse dynamic corr.</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>Wire burnback</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>Process control</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>Arc force</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
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
		<td>GET_ARCTWELD_INFO (3007) - output</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>Wire material</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>Wire diameter</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>Gas type</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>7</td>
		<td>Welding mode</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>Twin oper mode</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
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
		<td>GET_ARCTWELD_INFO (3009) - output</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>
			0x01 = Arc on <br>
			0x02 = Robot ready <br>
			0x04 = Master torch select <br>
			0x08 = Gas on <br>
			0x10 = Wire inching <br>
			0x20 = Wire retract <br>
			0x40 = Welder error reset <br>
			0x80 = Wire stick check	<br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = Welding simulation <br>
			0x02 = Pilot arc<br>
			0x04 = Lift arc use <br>
			0x08 = Super pulse use <br>
			0x10 = Online status <br>
			0x20 = Job mode active <br>
			0x40 = Voltage set mode <br>
			0x80 = Current set mode <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>
			0x01 = Robot torch collision <br>
			0x02 = Robot error status <br>
		</td>
		<td>s1</td>
	</tr>	
</tbody>
</table>

<br>

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
		<td>GET_ARCTWELD_INFO (3010) - status</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>Current arcon cnd no.</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>Current touchsensing cnd no.</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>Current weaving cnd no.</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>Current lvs cnd no.</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>Current arccond cnd no.</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
