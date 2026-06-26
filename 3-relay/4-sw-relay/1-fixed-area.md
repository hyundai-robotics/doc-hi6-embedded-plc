# 3.4.1 S relay - 固定区域

请参阅下面显示的表格，了解 SB0-SB1999 区域的固定项。

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

<div class="page-break"></div>

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
		<td>如果在操作中发生进位，则开启</td>
		<td>如果 BCD 操作不可行，则开启</td>
		<td>1 秒时钟</td>
		<td>0.2 秒时钟</td>
		<td>0.1 秒时钟</td>
		<td>仅在一次扫描中开启</td>
		<td>始终关闭</td>
		<td>始终开启</td>		
		<td></td>
	</tr>
	<tr>
		<td>SB1</td>
		<td class='grayed'></td>
		<td>当标签为 0 或以下，或跳转的标签不存在时开启</td>
		<td>如果标签重复，则开启</td>
		<td>如果标签数量超过 100，则开启</td>
		<td>如果标签不是常量，则开启</td>
		<td class='grayed'></td>
		<td>4 秒时钟</td>
		<td>2 秒时钟</td>
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
		<td>如果没有子梯级被调用，则开启</td>
		<td>当扫描时间超过 5 秒时开启</td>
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
		<td>T/P 启动完成</td>
		<td></td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

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
		<td>PLC 执行模式</td>
		<td>0=停止, 1=R.停止, 2=R.运行,<br>
		 3= 运行, 4=关闭, 5=无程序</td>
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
		<td>软件版本：第一</td>
		<td>例如，在 V60.05-08 的情况下，60</td>
	</tr>
	<tr>
		<td>SB15</td>
		<td>软件版本：第二</td>
		<td>例如，在 V60.05-08 的情况下，5</td>
	</tr>
	<tr>
		<td>SB16</td>
		<td>软件版本：小修正</td>
		<td>例如，在 V60.05-08 的情况下，8</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW18</td>
		<td>扫描时间</td>
		<td>毫秒</td>
	</tr>
	<tr>
		<td>SW20</td>
		<td>赋值时间</td>
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
		<td>梯形图中的总步数</td>
		<td></td>
	</tr>
	<tr>
		<td>SW28</td>
		<td>占用比率</td>
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
		<td>当前用户坐标编号</td>
		<td></td>
	</tr>
	<tr>
		<td>SB40</td>
		<td>当前工具编号</td>
		<td></td>
	</tr>
	<tr>
		<td>SB41</td>
		<td>机器人状态</td>
		<td>0=停止, 1=运行, 2=等待</td>
	</tr>
	<tr>
		<td>SB42</td>
		<td>播放速度</td>
		<td>%</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW44</td>
		<td>步进前进/后退最大速度</td>
		<td>毫米/秒</td>
	</tr>
	<tr>
		<td>SW46</td>
		<td>工具尖端移动速度</td>
		<td>毫米/秒</td>
	</tr>
	<tr>
		<td>SW48</td>
		<td>错误/警告编号</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
</tbody>
</table>

<div class="page-break"></div>

<table class="tg">
<tbody>
	<tr>
		<td>SW50</td>
		<td>错误/警告辅助信息</td>
		<td></td>
	</tr>
	<tr>
		<td>SW62</td>
		<td>间接地址指定（继电器-2）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW64</td>
		<td>间接地址指定（继电器-4）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW66</td>
		<td>间接地址指定（继电器-6）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW68</td>
		<td>间接地址指定（继电器-8）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW70</td>
		<td>间接地址指定（继电器-10）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW72</td>
		<td>间接地址指定（继电器-12）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW74</td>
		<td>间接地址指定（继电器-14）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW76</td>
		<td>间接地址指定（继电器-16）</td>
		<td></td>
	</tr>
	<tr>
		<td>SW78</td>
		<td>间接地址指定（继电器-18）</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB88</br>
		...</br>
		SB99</td>
		<td>教示器键输入状态</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
		<tr>
		<td>SB111</td>
		<td>运行时间选择</td>
		<td>1=总计（初始化后），<br>
		2=总计（通电后），<br>
		3=最后一个周期，<br>
		4=当前周期
			</td>
	</tr>
	<tr>
		<td>SL112</td>
		<td>电机开启（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL116</td>
		<td>电机开启（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL120</td>
		<td>运行时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL124</td>
		<td>运行时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL128</td>
		<td>移动时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL132</td>
		<td>移动时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL136</td>
		<td>周期计数</td>
		<td></td>
	</tr>
	<tr>
		<td>SL140</td>
		<td>等待，DI 等待时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL144</td>
		<td>等待，DI 等待时间（毫秒）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL148</td>
		<td>延迟等待时间（天）</td>
		<td></td>
	</tr>
	<tr>
		<td>SL152</td>
		<td>延迟等待时间（毫秒）</td>
		<td></td>
	</tr>
	</tbody>
</table>

<div class="page-break"></div>

<table class="tg">
<tbody>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB159</td>
		<td>轴信息选择</td>
		<td>1 = 当前位置信息 
		<br>(轴角度)，<br>
		2 = 当前位置信息 
		<br>(基坐标)，<br>
		3 = 当前位置信息 
		<br>(基/用户坐标)<br>
		6 = 轴速度,<br>
		7 = 电机速度<br>
		8 = 电机速度指令 <br>
		在速度控制时（rpm）<br>
		10 = 负载因子(I/Ir)，<br>
		11 = 负载因子(I/Ip)，<br>
		13 = 负载因子（连续）<br>
		15 = 编码器温度<br>
		18 = 累积距离<br>
		每个轴<br>
		111 = 位置偏差<br>
		（当前），<br>
		112 = 位置偏差<br>
		（最大）<br>
		124 = 编码器通信故障计数</td>
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
		<tr>
		<td>SL200</td>
		<td>每个轴的控制状态<br>
		（0=关闭, 1=开启）</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	</tbody>
</table>

<div class="page-break"></div>

<table class="tg">
<tbody>
	<tr>
		<td>SW210</br>
		...</br>
		SW280</td>
		<td>程序编号
		<td>（主任务 = sw210,<br>
		子任务 1 = sw220,<br>
		子任务 2 = sw230,<br> 
		子任务 3 = sw240,<br>
		子任务 4 = sw250,<br>
		子任务 5 = sw260,<br>
		子任务 6 = sw270,<br>
		子任务 7 = sw280）</td>
	</tr>
	<tr>
		<td>SW212</br>
		...</br>
		SW282</td>
		<td>步骤编号</td>
		<td>（主任务 = sw212,<br>
		子任务 1 = sw222,<br>
		子任务 2 = sw232,<br>
		子任务 3 = sw242,<br>
		子任务 4 = sw252,<br>
		子任务 5 = sw262,<br>
		子任务 6 = sw272,<br>
		子任务 7 = sw282）</td></td>
	</tr>
	<tr>
		<td>SW214</br>
		...</br>
		SW284</td>
		<td>功能编号</td>
		<td>（主任务 = sw214,<br>
		子任务 1 = sw224,<br>
		 子任务 2 = sw234,<br>
		 子任务 3 = sw244,<br>
		子任务 4 = sw254,<br>
		子任务 5 = sw264,<br>
		子任务 6 = sw274,<br>
		子任务 7 = sw284）</td>
	</tr>
	<tr>
		<td>SW216</br>
		...</br>
		SW286</td>
		<td>主程序编号</td>
		<td>（主任务 = sw216,<br>
		子任务 1 = sw226,<br>
		 子任务 2 = sw236,<br>
		 子任务 3 = sw246,<br>
		子任务 4 = sw256,<br>
		子任务 5 = sw266,<br>
		子任务 6 = sw276,<br>
		子任务 7 = sw286）</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW500</td>
		<td>枪的编号</td>
		<td>0=当前选择的枪,<br>
		1-16</td>
	</tr>
	<tr>
		<td>SW502</td>
		<td>枪搜索状态</td>
		<td>1=完成, 0=未完成</td>
	</tr>
	<tr>
		<td>SW504</td>
		<td>移动电极<br>
		磨损量 x 100</td>
		<td></td>
	</tr>
	<tr>
		<td>SW506</td>
		<td>固定电极<br>
		磨损量 x 100</td>
		<td></td>
	</tr>
	<tr>
		<td>SW508</td>
		<td>加压力<br>
		指令值 x 10</td>
		<td></td>
	</tr>
	<tr>
		<td>SW510</td>
		<td>加压力<br>
		当前值 x 10</td>
		<td></td>
	</tr>
</tbody>
</table>
</tbody>
</table>

<div class="page-break"></div>