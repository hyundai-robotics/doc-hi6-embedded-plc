# 3.4.12 S 릴레이 - SYSTEM_VARIABLE

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>


### 시스템 변수 (system variable) 얻기 및 설정

{% hint style="info" %}
V70.00-00 미만의 버전에서는
시스템 변수 설정을 위해서 command 가 변경된 것을 확인하고 동작합니다. <br>
즉, command 값이 161로 변경된 순간에 1회 동작합니다.  

{% endhint %}

#### 시스템 변수 얻기 
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

#### 시스템 변수 설정 
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

#### <mark style="color:green;">재생속도</mark>
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
		<td>42 = 재생속도</td>
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
참고) <br>
- V70.00-00 미만의 버전에서 얻기는 지원하지 않습니다. <br>
<br>

#### <mark style="color:green;">현재 툴번호</mark>
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
		<td>40 = 툴번호</td>
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
참고) <br>
- V70.00-00 미만의 버전에서 얻기는 지원하지 않습니다. <br>
<br>

#### <mark style="color:green;">스텝 전/후진시 최고속</mark>
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
		<td>44 = 스텝 전/후진시 최고속</td>
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
참고) <br>
- V70.00-00 미만의 버전에서 얻기는 지원하지 않습니다. <br>
- V60.32-07 미만의 버전에서 설정을 지원하지 않습니다. <br>
<br>

<div class="page-break"></div>
