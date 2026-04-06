# 3.4.12 S realy - SYSTEM_VARIABLE

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>


### Getting and Setting system variables

{% hint style="info" %}
In versions lower than V70.00-00 to set system variables, check that the command has changed and operate. <br>
In other words, it operates once at the moment the command value changes to 161.  

{% endhint %}

#### Get system variables
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
		<td>item (of set data)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4 ~ 18</td>
		<td>param n</td>
		<td>get value</td>
		<td></td>
	</tr>
</tbody>
</table>
<br>

#### Set system variables
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
		<td>item (of set data)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4 ~ 18</td>
		<td>param n</td>
		<td>set value</td>
		<td></td>
	</tr>
</tbody>
</table>
<br>
<br>

#### <mark style="color:green;">Playback speed</mark>
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
		<td>42 = Playback speed</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 1</td>
		<td>value</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
Info) <br>
- Getting it on versions lower than V70.00-00 is not supported. <br>
<br>

#### <mark style="color:green;">Current tool number</mark>
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
		<td>40 = Tool number</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 1</td>
		<td>value</td>
		<td>s1</td>
	</tr>
</tbody>
</table>
Info) <br>
- Getting it on versions lower than V70.00-00 is not supported. <br>
<br>

#### <mark style="color:green;">Step go/back max speed</mark>
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
		<td>44 = Step go/back max speed</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 1</td>
		<td>value</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
Info) <br>
- Getting it on versions lower than V70.00-00 is not supported. <br>
- Settings are not supported on versions lower than V60.32-07. <br>
<br>

<div class="page-break"></div>
