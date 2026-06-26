# 3.4.10 S realy - ARCWELD_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {
    border-color:gray;
    border-style:solid;
    border-width:1px;
    padding: 1px 4px;
    height: auto !important;
}
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
		<td>GET_ARCTWELD_INFO (3000) - 输入</td>
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
		<td>焊接电流</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊接电压</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>焊机错误</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>送丝速度</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
从 V60.32-00 开始支持以下服务。
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
		<td>GET_ARCTWELD_INFO (3001) - 输入</td>
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
		<td>馈送电机电流</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>接缝跟踪数据</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>焊接工艺</td>
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
		<td>GET_ARCTWELD_INFO (3002) - 输入</td>
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
		<td>焊机总操作时间(秒)</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊机固件版本 - 低位(Vx.x.255)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>焊机固件版本 - 中位(Vx.255.x)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>焊机固件版本 - 高位(V255.x.x)</td>
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
		<td>GET_ARCTWELD_INFO (3004) - 输入</td>
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
			0x01 = WCR(焊丝接触继电器) <br>
			0x02 = 火炬碰撞 <br>
			0x04 = 电源正常 <br>
			0x08 = 焊丝卡住 <br>
			0x10 = 焊机错误 <br>
			0x20 = 工艺激活 <br>
			0x40 = 通信准备就绪 <br>
			0x80 = 焊丝使用可能 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 火炬状态 <br>
			0x02 = 逐步状态 <br>
			0x04 = 收回状态 <br>
			0x08 = 气体检查 <br>
			0x10 = 协调可用 <br>
			0x20 = 限制状态 <br>
			0x40 = 设置超出范围 <br>
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
		<td>GET_ARCTWELD_INFO (3005) - 输出</td>
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
		<td>焊机电流</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊机电压</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>作业/程序号</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>操作模式</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>协调代码</td>
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
		<td>GET_ARCTWELD_INFO (3006) - 输出</td>
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
		<td>脉冲动态补偿</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊丝回缩</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>工艺控制</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>弧力</td>
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
		<td>GET_ARCTWELD_INFO (3007) - 输出</td>
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
		<td>焊丝材料</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>焊丝直径</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>气体类型</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>7</td>
		<td>焊接模式</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>双运作模式</td>
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
		<td>GET_ARCTWELD_INFO (3009) - 输出</td>
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
			0x01 = 弧开启 <br>
			0x02 = 机器人准备就绪 <br>
			0x04 = 主火炬选择 <br>
			0x08 = 气体开启 <br>
			0x10 = 焊丝进给 <br>
			0x20 = 焊丝收回 <br>
			0x40 = 焊机错误复位 <br>
			0x80 = 焊丝卡住检查 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 焊接仿真 <br>
			0x02 = 引弧<br>
			0x04 = 提升弧使用 <br>
			0x08 = 超脉冲使用 <br>
			0x10 = 在线状态 <br>
			0x20 = 作业模式激活 <br>
			0x40 = 电压设置模式 <br>
			0x80 = 电流设置模式 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>
			0x01 = 机器人火炬碰撞 <br>
			0x02 = 机器人错误状态 <br>
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
		<td>GET_ARCTWELD_INFO (3010) - 状态</td>
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
		<td>当前电弧控制编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>当前接触感应编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>当前编织控制编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>当前LVS控制编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>当前弧控制编号。</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>