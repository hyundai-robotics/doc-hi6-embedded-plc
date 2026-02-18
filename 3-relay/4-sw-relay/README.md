# 3.4 S 继电器

在 ${cont_model} 控制器中，各种状态的值映射到 S 继电器。通过向某些 S 继电器写入值，也可以改变 ${cont_model} 的状态。

因此，外部设备，例如过程可编程逻辑控制器 (PLC) 或个人计算机 (PC)，可以通过读取 S 继电器的值，通过现场总线、Modbus 等远程监控 ${cont_model} 控制器的状态，并且可以通过向 S 继电器写入值远程控制 ${cont_model} 控制器。

S 继电器的区域可以大致分为以下两个部分。

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
	<tr>
		<th>地址</th>
		<th>内容</th>
	</tr>
	<tr>
		<td>SB00000-SB01999</td>
		<td>固定区域</td>
	</tr>
	<tr>
		<td>SB02000-SB19999</td>
		<td>可选项区域 (插槽)</td>
	</tr>
</table>

<br>

### 固定区域
经常使用的基本项分配到预定地址。无法通过设置更改或分配项目。固定区域的映射将在下一节中描述。

<br>

### 可选项区域
该区域由总共 900 个插槽组成，每个插槽 20 字节。每个插槽的配置将由放入首个字的命令值决定。每个命令的映射将在下一节中描述。

<table class="tg">
<thead>
	<tr>
		<th>插槽索引</th>
		<th>s 索引:偏移量</th>
		<th>字段</th>
	</tr>
</thead>
<tbody>
	<tr>
```html
<td rowspan=10>插槽 0</td>
<td>2000:0</td>
<td>命令（传统做法：获取偶数，设置奇数）</td>
</tr>
<tr>
	<td>:2</td>
	<td rowspan=2>参数</td>
</tr>
<tr>
	<td>:4</td>
</tr>
<tr>
	<td>:6</td>
	<td rowspan=5>结果</td>
</tr>
<tr><td>:8</td></tr>
<tr><td>:10</td></tr>
<tr><td>:12</td></tr>
<tr><td>:14</td></tr>
<tr><td>:16</td><td class='grayed'></td></tr>
<tr><td>:18</td><td class='grayed'></td></tr>
<tr>
	<td rowspan=10>插槽 1</td>
	<td>2020:0</td>
	<td>命令</td>
</tr>
<tr>
	<td>:2</td>
	<td>参数</td>
</tr>
<tr>
	<td>:4</td>
	<td rowspan=2>结果</td>
</tr>
<tr>
	<td>:6</td>
</tr>
<tr><td>:8</td><td class='grayed'></td></tr>
<tr><td>:10</td><td class='grayed'></td></tr>
<tr><td>:12</td><td class='grayed'></td></tr>
<tr><td>:14</td><td class='grayed'></td></tr>
<tr><td>:16</td><td class='grayed'></td></tr>
<tr><td>:18</td><td class='grayed'></td></tr>
<tr>
	<td rowspan=3>插槽 2</td>
	<td>2040:0</td>
	<td>命令</td>
</tr>
<tr>
	<td>:2</td>
```
<td>参数</td>
	</tr>
	<tr>
		<td>...</td>
		<td>...</td>
	</tr>
	<tr>
		<td>...</td>
		<td>...</td>
		<td>...</td>
	</tr>
	<tr>
		<td rowspan=3>槽 899</td>
		<td>19980:0</td>
		<td>命令</td>
	</tr>
	<tr>
		<td>:2</td>
		<td>参数</td>
	</tr>
	<tr>
		<td>...</td>
		<td>...</td>
	</tr>
</tbody>
</table>