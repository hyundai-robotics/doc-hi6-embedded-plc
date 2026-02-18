# 3.4.10 S realy - ARCWELD_INFO

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
		<td>GET_ARCTWELD_INFO (3000) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
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
<<<SOURCE_MARKDOWN_START>>>
		<td>焊机错误</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>送线速度</td>
		<td>f4</td>
	</tr>
</tbody>
</table>



<br>
以下服务从 V60.32-00 开始支持。
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
		<td>GET_ARCTWELD_INFO (3001) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>送线电机电流</td>
		<td>f4</td><<<<SOURCE_MARKDOWN_END>>>
</tr>
	<tr>
		<td>8</td>
		<td>缝合跟踪数据</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>焊接过程</td>
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
		<td>GET_ARCTWELD_INFO (3002) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊工编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双工编号 (0~1)</td>
		<td>s1</td>
	</tr>
<td>4</td>
		<td rowspan=5>结果</td>
		<td>焊接机总操作时间（秒）</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊接机固件版本 - 低位（Vx.x.255）</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>焊接机固件版本 - 中位（Vx.255.x）</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>焊接机固件版本 - 高位（V255.x.x）</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
<table class="tg">
<thead>
	<tr>
		<th>S 偏移量</th>
		<th>字段</th>
		<th>描述</th>
		<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3004) - 输入</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>
			0x01 = WCR(接触继电器) <br>
			0x02 = 火炬碰撞 <br>
			0x04 = 电源正常 <br>
			0x08 = 电线卡住 <br>
			0x10 = 焊机错误 <br>
			0x20 = 过程激活 <br>
			0x40 = 通信准备 <br>
			0x80 = 电线使用可能 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 火炬状态 <br>
			0x02 = 微步状态 <br>
			0x04 = 回缩状态 <br>
			0x08 = 气体检查 <br>
			0x10 = 协同可用 <br>
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
		<td>GET_ARCTWELD_INFO (3005) - 输出</td>
<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双胞胎编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
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
		<td>作业/程序编号</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>操作模式</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>协同代码</td>
		<td>s2</td>
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
```html
<th>类型</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>0</td>
		<td>命令</td>
		<td>GET_ARCTWELD_INFO (3006) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>welder_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>脉冲动态修正</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>焊丝回缩</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>过程控制</td>
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
```
```html
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
		<td>GET_ARCTWELD_INFO (3007) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>电线材料</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>电线直径</td>
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
```
```html
<td>双工模式</td>
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
		<td>GET_ARCTWELD_INFO (3009) - 输出</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>双工编号 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>
			0x01 = 弧开启 <br>
			0x02 = 机器人就绪 <br>
			0x04 = 主焊炬选择 <br>
			0x08 = 气体开启 <br>
			0x10 = 焊丝进给 <br>
			0x20 = 焊丝回缩 <br>
			0x40 = 焊机错误重置 <br>
			0x80 = 焊丝粘连检查 <br>
		</td>
		<td>s1</td>
```
</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 焊接模拟 <br>
			0x02 = 引弧 <br>
			0x04 = 提升弧使用 <br>
			0x08 = 超脉冲使用 <br>
			0x10 = 在线状态 <br>
			0x20 = 工作模式激活 <br>
			0x40 = 电压设定模式 <br>
			0x80 = 电流设定模式 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>
			0x01 = 机器人焊枪碰撞 <br>
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
		<td>GET_ARCTWELD_INFO (3010) - 状态</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>参数 1</td>
		<td>焊机编号 (0~1)</td>
		<td>s1</td>
</tr>
	<tr>
		<td>3</td>
		<td>参数 2</td>
		<td>twin_no (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>结果</td>
		<td>当前弧控制状态编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>当前触摸传感状态编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>当前编织状态编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>当前lvs状态编号。</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>当前弧控制状态编号。</td>
		<td>s2</td>
	</tr>
</tbody>
</table>