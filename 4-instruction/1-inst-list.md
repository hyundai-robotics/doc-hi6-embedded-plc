# 4.1 명령어 일람


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
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>같은지(=) 검사</td>
	</tr>
	<tr>
		<td>NEQ</td>
		<td>Inverting</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>다른지(<>) 검사</td>
	</tr>
	<tr>
		<td>LES</td>
		<td>Less Than</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>작은지(<) 검사</td>
	</tr>
	<tr>
		<td>GRT</td>
		<td>Greater Than</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>큰지(>) 검사</td>
	</tr>
	<tr>
		<td>LEQ</td>
		<td>Less Than or Equal</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>작거나 같은지(<=) 검사</td>
	</tr>
	<tr>
		<td>GEQ</td>
		<td>Greater Than or Equal</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
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
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성인 동안 타이머 동작</td>
	</tr>
	<tr>
		<td>CTD</td>
		<td>CounT Down</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
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
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, (+)연산</td>
	</tr>
	<tr>
		<td>SUB</td>
		<td>SUBtract</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, (-)연산</td>
	</tr>
	<tr>
		<td>MUL</td>
		<td>MULtiply</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, (x)연산</td>
	</tr>
	<tr>
		<td>DIV</td>
		<td>DIVide</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, (/)연산</td>
	</tr>
	<tr>
		<td>POW</td>
		<td>POWer</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, (^: 거듭제곱)연산</td>
	</tr>
</tbody>
</table>




<br><br>  

### * 데이터 변환 명령

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
		<td>TOD</td>
		<td>convert integer TO BCD</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, integer를 BCD로 변환</td>
	</tr>
	<tr>
		<td>FRD</td>
		<td>convert FRom BCD to inetger</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, BCD를 integer로 변환.</td>
	</tr>
	<tr>
		<td>SEG</td>
		<td>7'SEGment</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, 7'세그먼트 값으로 변환.</td>
	</tr>
</tbody>
</table>


<br><br>  

### * 이동 및 복사 명령

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
		<td>MOV</td>
		<td>MOVe</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, 데이터 한 개를 복사</td>
	</tr>
	<tr>
		<td>COP</td>
		<td>COPy data</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, 데이터 여러 개를 복사.</td>
	</tr>
	<tr>
		<td>CCOP</td>
		<td>Conditional COPy data</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung 상태에 따라, 데이터 여러 개를 복사.</td>
	</tr>
	<tr>
		<td>ROT</td>
		<td>ROTating output</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, 순차적으로 출력.</td>
	</tr>
</tbody>
</table>

<br><br>  


### * 블록 제어 명령

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
		<td>FOR</td>
		<td>FOR loop</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, NEXT까지 반복 실행</td>
	</tr>
	<tr>
		<td>NEXT</td>
		<td>NEXT loop</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>반복횟수 이내이면, FOR문으로 분기(jump).</td>
	</tr>
	<tr>
		<td>LBL</td>
		<td>LaBeL</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>JMP 명령으로 분기(jump)할 위치 지정.</td>
	</tr>
	<tr>
		<td>JMP</td>
		<td>JuMP</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, LBL 위치로 분기.<br>
		(Label&lt;0이면, -n개의 NEXT까지 건너뜀.)</td>
	</tr>
	<tr>
		<td>CALL</td>
		<td>CALL</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, sub-ladder 호출.</td>
	</tr>
	<tr>
		<td>END</td>
		<td>END</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>Rung이 활성이면, sub-ladder end.</td>
	</tr>
</tbody>
</table>