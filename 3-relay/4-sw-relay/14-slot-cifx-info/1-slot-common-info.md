# 3.4.14.1 S 继电器 - CIFX PCI 通信状态

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<br>

### CIFX PCI 通用状态

<br>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 CIFX 状态 = 1000</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>状态 1 = 1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>4</td>
		<td>通道状态</td>
		<td class='grayed'></td>
		<td>需要重启启用</td>
		<td>需要重启</td>
		<td>配置新 </td>
		<td>配置锁定</td>
		<td>总线打开</td>
		<td>运行</td>
		<td>准备好</td>
	</tr>
	<tr>
		<td>8</td>
		<td>4</td>
		<td>通信状态</td>
		<td colspan=8>0 = 未知, <br> 1 = 未配置, <br> 2 = 停止, <br> 3 = 空闲, <br> 4 = 操作</td>
	</tr>
	<tr>
		<td>12</td>
		<td>4</td>
		<td>通信错误代码</td>
		<td colspan=8>0 = 无错误, <br> 非零 = 错误代码 (32位十六进制)</td>
	</tr>
	<tr>
		<td>16</td>
		<td>2</td>
		<td>诊断结构版本</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>18</td>
		<td>2</td>
		<td>看门狗超时 (毫秒)</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>


<br>
<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>获取 CIFX 状态 = 1000</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>状态 2 = 2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>1</td>
		<td>输入数据握手模式</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>5</td>
```html
<td>-</td>
<td></td>
<td colspan=8></td>
</tr>
<tr>
<td>6</td>
<td>1</td>
<td>输出数据握手模式</td>
<td colspan=8></td>
</tr>
<tr>
<td>7</td>
<td>-</td>
<td></td>
<td colspan=8></td>
</tr>
<tr>
<td>8</td>
<td>4</td>
<td>主机系统看门狗</td>
<td colspan=8></td>
</tr>
<tr>
<td>12</td>
<td>4</td>
<td>通信错误计数</td>
<td colspan=8></td>
</tr>
<tr>
<td>16</td>
<td>-</td>
<td></td>
<td colspan=8></td>
</tr>
<tr>
<td>17</td>
<td>1</td>
<td>输入数据握手错误</td>
<td colspan=8></td>
</tr>
<tr>
<td>18</td>
<td>1</td>
<td>输出数据握手错误</td>
<td colspan=8></td>
</tr>
<tr>
<td>19</td>
<td>-</td>
<td></td>
```
<td colspan=8></td>
	</tr>
</tbody>
</table>


<br>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 CIFX 状态 = 1000</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>状态 3 = 3</td>
	</tr>
<tr>
		<td>4</td>
		<td>16</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>

<br>

### 仅限 CIFX PCI 主控

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 CIFX 状态 = 1000</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>状态 4 = 4</td>
	</tr>
	<tr>
		<td>4</td>
		<td>4</td>
		<td>从设备状态</td>
		<td colspan=8>0 = 未知, <br> 1 = 正常, <br> 2 = 失败</td>
	</tr>
	<tr>
		<td>8</td>
		<td>4</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>12</td>
		<td>4</td>
		<td>配置从设备的数量</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>16</td>
		<td>4</td>
		<td>活动从设备的数量</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
<td class='powderblued'>位 6</td>
<td class='powderblued'>位 5</td>
<td class='powderblued'>位 4</td>
<td class='powderblued'>位 3</td>
<td class='powderblued'>位 2</td>
<td class='powderblued'>位 1</td>
<td class='powderblued'>位 0</td>
</tr>
<tr>
<td>0</td>
<td>2</td>
<td>命令</td>
<td colspan=8>获取 CIFX 状态 = 1000</td>
</tr>
<tr>
<td>2</td>
<td>1</td>
<td>参数 1</td>
<td colspan=8>插槽编号 = 1 ~ 3</td>
</tr>
<tr>
<td>3</td>
<td>1</td>
<td>参数 2</td>
<td colspan=8>状态 5 = 5</td>
</tr>
<tr>
<td>4</td>
<td>4</td>
<td>诊断从设备数量</td>
<td colspan=8></td>
</tr>
<tr>
<td>8</td>
<td>12</td>
<td>保留</td>
<td colspan=8></td>
</tr>
</tbody>
</table>