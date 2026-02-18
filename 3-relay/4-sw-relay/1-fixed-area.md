# 3.4.1 S 继电器 - 固定区域

请参考下表中提供的 SB0-SB1999 区域的固定项目。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.bit { width: 10%; }
</style>

### 特殊标志区域

<table class="tg">
<thead>
	<tr>
		<th class='bit'>继电器</th>
		<th class='bit'>bit7</th>
		<th class='bit'>bit6</th>
		<th class='bit'>bit5</th>
		<th class='bit'>bit4</th>
		<th class='bit'>bit3</th>
		<th class='bit'>bit2</th>
		<th class='bit'>bit1</th>
		<th class='bit'>bit0</th>		
		<th class='bit'>备注</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>SB0</td>
		<td>如果在操作中发生进位则开启</td>
		<td>如果无法进行 BCD 操作则开启</td>
		<td>1秒时钟</td>
		<td>0.2秒时钟</td>
		<td>0.1秒时钟</td>
		<td>仅在一个扫描周期内开启</td>
		<td>始终关闭</td>
		<td>始终开启</td>		
		<td></td>
	</tr>
	<tr>
		<td>SB1</td>
		<td class='grayed'></td>
		<td>当标签为 0 或更低时，或没有跳转标签时则开启</td>
		<td>如果标签重复则开启</td>
		<td>如果标签数量超过 100 则开启</td>
		<td>如果标签不是常数则开启</td>
		<td class='grayed'></td>
		<td>4秒时钟</td>
<td>2秒时钟</td>
		<td></td>
	</tr>
	<tr>
		<td>SB2</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td>当没有通过Call调用的子梯形图时开启</td>
		<td>当扫描时间超过5秒时开启</td>
		<td></td>
	</tr>
	<tr>
		<td>SB3</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td>自我诊断完成</td>
		<td>T/P启动完成</td>
		<td></td>
	</tr>
</tbody>
</table>

<br>

### 基本信息区域

<table class="tg">
<thead>
	<tr>
		<th>继电器</th>
		<th>描述</th>
		<th>备注</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>SB4</th>
		<td>PLC执行模式<br>
		(0=停止, 1=R.停止, 2=R.运行, 3=运行, 4=关闭, 5=无程序)</td>
		<td></td>
	</tr>
<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
<tr>
	<td>SW6</td>
	<td>日期/时间：年份</td>
</tr>
<tr>
	<td>SB8</td>
	<td>日期/时间：月份</td>
	<td></td>
</tr>
<tr>
	<td>SB9</td>
	<td>日期/时间：日期</td>
	<td></td>
</tr>	
<tr>
	<td>SB10</td>
	<td>日期/时间：小时</td>
	<td></td>
</tr>	
<tr>
	<td>SB11</td>
	<td>日期/时间：分钟</td>
	<td></td>
</tr>	
<tr>
	<td>SB12</td>
	<td>日期/时间：秒</td>
	<td></td>
</tr>	
<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
<tr>
	<td>SB14</td>
	<td>软件版本：第一<br>
	例如，在 V60.05-08 的情况下，SB14:60, SB15:5, SB16:8</td>
	<td></td>
</tr>
<tr>
	<td>SB15</td>
	<td>软件版本：第二</td>
	<td></td>
</tr>
<tr>
	<td>SB16</td>
	<td>软件版本：小修复</td>
	<td></td>
</tr>
<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
<tr>
	<td>SW18</td>
<td>扫描时间</td>
<td>毫秒</td>
</tr>
<tr>
<td>SW20</td>
<td>分配时间</td>
<td>微秒</td>
</tr>
<tr>
<td>SW22</td>
<td>最大占用时间</td>
<td>毫秒</td>
</tr>
<tr>
<td>SW24</td>
<td>平均占用时间</td>
<td>毫秒</td>
</tr>
<tr>
<td>SW26</td>
<td>梯子中的总步骤数</td>
<td></td>
</tr>
<tr>
<td>SW28</td>
<td>占用比例</td>
<td>%</td>
</tr>
<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td>SB30</td>
<td>枪输出状态</td>
<td></td>
</tr>
<tr>
<td>SB39</td>
<td>当前用户坐标号</td>
<td></td>
</tr>
<tr>
<td>SB40</td>
<td>当前工具编号</td>
<td></td>
</tr>
<tr>
<td>SB41</td>
<td>机器人状态 (0=停止, 1=运行, 2=等待)</td>
<td></td>
</tr>
<tr>
<td>SB42</td>
		<td>播放速度</td>
		<td>%</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW44</td>
		<td>手动速度</td>
		<td>mm/s</td>
	</tr>
	<tr>
		<td>SW46</td>
		<td>工具尖端移动速度</td>
		<td>mm/s</td>
	</tr>
	<tr>
		<td>SW48</td>
		<td>错误/警告编号</td>
		<td></td>
	</tr>
	<tr>
		<td>SW50</td>
		<td>错误/警告辅助信息</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW60</td>
		<td>间接地址指定 1</td>
		<td></td>
	</tr>
	<tr>
		<td>SW62</td>
		<td>间接地址指定 2</td>
		<td></td>
	</tr>
	<tr>
		<td>SW64</td>
		<td>间接地址指定 3</td>
		<td></td>
	</tr>
	<tr>
		<td>SW66</td>
		<td>间接地址指定 4</td>
		<td></td>
	</tr>
	<tr>
		<td>SW68</td>
		<td>间接地址指定 5</td>
		<td></td>
</tr>
	<tr>
		<td>SW70</td>
		<td>间接地址指定 6</td>
		<td></td>
	</tr>
	<tr>
		<td>SW72</td>
		<td>间接地址指定 7</td>
		<td></td>
	</tr>
	<tr>
		<td>SW74</td>
		<td>间接地址指定 8</td>
		<td></td>
	</tr>
	<tr>
		<td>SW76</td>
		<td>间接地址指定 9</td>
		<td></td>
	</tr>
	<tr>
		<td>SW78</td>
		<td>间接地址指定 10</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB88</br>
		...</br>
		SB99</td>
		<td>教学挂件按键输入状态</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW100</td>
		<td>主程序编号</td>
		<td>主任务</td>
	</tr>
	<tr>
		<td>SW102</td>
		<td>步骤编号</td>
		<td>主任务</td>
	</tr>
	<tr>
		<td>SW104</td>
		<td>功能编号</td>
		<td>主任务</td>
	</tr>
<tr>
		<td>SW106</td>
		<td>主程序编号</td>
		<td>主任务</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB109</td>
		<td>运行时间选择<br>
		(1=总计（初始化后），2=总计（电源输入后），3=上一个周期，4=当前周期)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL110</td>
		<td>电机开启（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL114</td>
		<td>电机开启（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL118</td>
		<td>运行时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL122</td>
		<td>运行时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL126</td>
		<td>移动时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL130</td>
		<td>移动时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL134</td>
		<td>周期计数</td>
		<td></td>
	</tr>
	<tr>
		<td>SL138</td>
		<td>等待，二进制等待时间（天）</td>
```html
<td></td>
	</tr>
	<tr>
		<td>SL142</td>
		<td>等待，延迟时间 (毫秒)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL146</td>
		<td>延迟等待时间 (天)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL150</td>
		<td>延迟等待时间 (毫秒)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB159</td>
		<td>轴信息选择<br>
		1=当前的位置 (轴角度)， 2=当前的位置 (基坐标)， 3=当前的位置 (基/用户坐标)，<br> 6=轴速度， 7=电机速度<br>
		 10=负载因子(I/Ir)， 11=负载因子(I/Ip)， 13=负载因子（连续），<br> 15=编码器温度<br>
		 18=每个轴的累计距离)</td>
		<td></td>
	</tr>
	<tr>
		<td>SF160</td>
		<td>轴 1 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF164</td>
		<td>轴 2 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF168</td>
		<td>轴 3 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF172</td>
		<td>轴 4 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF176</td>
		<td>轴 5 的相关值</td>
		<td></td>
```
```html
</tr>
	<tr>
		<td>SF180</td>
		<td>轴 6 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF184</td>
		<td>轴 7 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF188</td>
		<td>轴 8 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF192</td>
		<td>轴 9 的相关值</td>
		<td></td>
	</tr>
	<tr>
		<td>SF196</td>
		<td>轴 10 的相关值</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
</tbody>
</table>
```