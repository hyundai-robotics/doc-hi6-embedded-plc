# 5.1 명령어 일람


<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

### * Rung과 Branch
<br>

<table>
<thead>
  <tr>
    <th>니모닉</th>
    <th>이름</th>
    <th>심볼</th>
    <th>설명</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>RUNG</td>
    <td>Rung</td>
    <td>├─┤</td>
    <td>rung</td>
  </tr>
  <tr>
    <td>BST</td>
    <td>Branch Start</td>
    <td>┬─</td>
    <td>브렌치(branch)의 시작</td>
  </tr>
  <tr>
    <td>BND</td>
    <td>Branch End</td>
    <td>─┬</td>
    <td>브렌치(branch)의 끝</td>
  </tr>
  <tr>
    <td>NXB</td>
    <td>Nested Branch</td>
    <td>└,├</td>
    <td>브렌치(branch)의 내포</td>
  </tr>
</tbody>
</table>

<br><br>  

### * logic 검사 명령: 검사결과, 참이면 Rung 활성, 거짓이면 비활성
<br>

<table>
<thead>
	<tr>
		<th>니모닉</th>
		<th>이름</th>
		<th>심볼</th>
		<th>설명</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>XIC</td>
		<td>Examine if Closed</td>
		<td>-| |-</td>
		<td>접점이 닫혔는가를 검사(A접점)</td>
	</tr>
	<tr>
		<td>XIO</td>
		<td>Examine if Open</td>
		<td>-|/|-</td>
		<td>접점이 열렸는가를 검사(B접점)</td>
	</tr>
	<tr>
		<td>INV</td>
		<td>Inverting</td>
		<td>-//-</td>
		<td>Rung의 결과 반전(inverting)</td>
	</tr>
	<tr>
		<td>EQU</td>
		<td>Inverting</td>
		<td>-&#888;-</td>
		<td>같은지(=) 검사</td>
	</tr>
	<tr>
		<td>NEQ</td>
		<td>Inverting</td>
		<td>-&#888;-</td>
		<td>다른지(<>) 검사</td>
	</tr>
	<tr>
		<td>LES</td>
		<td>Less Than</td>
		<td>-&#888;-</td>
		<td>작은지(<) 검사</td>
	</tr>
	<tr>
		<td>GRT</td>
		<td>Greater Than</td>
		<td>-&#888;-</td>
		<td>큰지(>) 검사</td>
	</tr>
	<tr>
		<td>LEQ</td>
		<td>Less Than or Equal</td>
		<td>-&#888;-</td>
		<td>작거나 같은지(<=) 검사</td>
	</tr>
	<tr>
		<td>GEQ</td>
		<td>Greater Than or Equal</td>
		<td>-&#888;-</td>
		<td>크거나 같은지(>=) 검사</td>
	</tr>
</tbody>
</table>

<br><br>  

### * 출력명령

<br>

<table>
<thead>
	<tr>
		<th>니모닉</th>
		<th>이름</th>
		<th>심볼</th>
		<th>설명</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>OTE</td>
		<td>OuTput Energize</td>
		<td>-( )-</td>
		<td>Rung의 상태를 출력(활성:ON/비활성:OFF)</td>
	</tr>
	<tr>
		<td>OTL</td>
		<td>OuTput Latch</td>
		<td>-(L)-</td>
		<td>Rung이 활성이면, ON(high)으로 출력</td>
	</tr>
	<tr>
		<td>OTU</td>
		<td>OuTput Unlatch</td>
		<td>-(U)-</td>
		<td>Rung이 활성이면, OFF(low)로 출력</td>
	</tr>
	<tr>
		<td>OSR</td>
		<td>One Shot Rising</td>
		<td>-(OSR)-</td>
		<td>Rung이 활성이면, 한 scan동안만 ON출력</td>
	</tr>
	<tr>
		<td>RES</td>
		<td>RESet</td>
		<td>-(RES)-</td>
		<td>Rung이 활성이면, 타이머나 카운터를 리셋</td>
	</tr>
</tbody>
</table>



<br><br>  

### * 타이머 및 카운터 명령

<br>

<table>
<thead>
	<tr>
		<th>니모닉</th>
		<th>이름</th>
		<th>심볼</th>
		<th>설명</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TON</td>
		<td>Time ON delay</td>
		<td>-&#888;-</td>
		<td>Rung이 활성인 동안 타이머 동작</td>
	</tr>
	<tr>
		<td>CTD</td>
		<td>CounT Down</td>
		<td>-&#888;-</td>
		<td>Rung의 활성(비활성->활성)을 다운-카운트</td>
	</tr>
</tbody>
</table>


<br><br>  

### * 산술연산 명령

<br>

<table>
<thead>
	<tr>
		<th>니모닉</th>
		<th>이름</th>
		<th>심볼</th>
		<th>설명</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>ADD</td>
		<td>Add</td>
		<td>-&#888;-</td>
		<td>Rung이 활성이면, (+)연산</td>
	</tr>
	<tr>
		<td>SUB</td>
		<td>SUBtract</td>
		<td>-&#888;-</td>
		<td>Rung이 활성이면, (-)연산</td>
	</tr>
	<tr>
		<td>MUL</td>
		<td>MULtiply</td>
		<td>-&#888;-</td>
		<td>Rung이 활성이면, (x)연산</td>
	</tr>
	<tr>
		<td>DIV</td>
		<td>DIVide</td>
		<td>-&#888;-</td>
		<td>Rung이 활성이면, (/)연산</td>
	</tr>
	<tr>
		<td>POW</td>
		<td>POWer</td>
		<td>-&#888;-</td>
		<td>Rung이 활성이면, (^: 거듭제곱)연산</td>
	</tr>
</tbody>
</table>




<br><br>  

### 

<br>

<table>
<thead>
	<tr>
		<th>니모닉</th>
		<th>이름</th>
		<th>심볼</th>
		<th>설명</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TTT</td>
		<td>NNN</td>
		<td>-&#888;-</td>
		<td>DDD</td>
	</tr>
	<tr>
		<td>TTT</td>
		<td>NNN</td>
		<td>-&#888;-</td>
		<td>DDD</td>
	</tr>
</tbody>
</table>
