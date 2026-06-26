# 3.4.12 S realy - SYSTEM_VARIABLE

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>


### 获取和设置系统变量

{% hint style="info" %}
在版本低于 V70.00-00 的情况下，要设置系统变量，请检查命令是否已更改并操作。 <br>
换句话说，当命令值更改为 161 时，它将立即运行。  

{% endhint %}

#### 获取系统变量
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
		<td>GET_SYS_VAR (160)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>项（设置数据的）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4 ~ 18</td>
		<td>param n</td>
		<td>获取值</td>
		<td></td>
	</tr>
</tbody>
</table>
<br>

#### 设置系统变量
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
		<td>SET_SYS_VAR (161)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>项（设置数据的）</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4 ~ 18</td>
		<td>param n</td>
		<td>设置值</td>
		<td></td>
	</tr>
</tbody>
</table>
<br>
<br>

#### <mark style="color:green;">播放速度</mark>
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
		<td>2</td>
		<td>param 1</td>
		<td>42 = 播放速度</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 1</td>
		<td>值</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
信息） <br>
- 在版本低于 V70.00-00 的情况下不支持获取。 <br>
<br>

#### <mark style="color:green;">当前工具编号</mark>
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
		<td>2</td>
		<td>param 1</td>
		<td>40 = 工具编号</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 1</td>
		<td>值</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
信息） <br>
- 在版本低于 V70.00-00 的情况下不支持获取。 <br>
<br>

#### <mark style="color:green;">步进前进/后退最大速度</mark>
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
		<td>2</td>
		<td>param 1</td>
		<td>44 = 步进前进/后退最大速度</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 1</td>
		<td>值</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
信息） <br>
- 在版本低于 V70.00-00 的情况下不支持获取。 <br>
- 在版本低于 V60.32-07 的情况下不支持设置。 <br>
<br>

<div class="page-break"></div>