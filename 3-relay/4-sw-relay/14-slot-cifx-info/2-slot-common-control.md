# 3.4.14.2 S 릴레이 - CIFX 산업용 통신 제어 릴레이 (공통)

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>


<br>

#### 60.30-07 버전 부터 지원

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>이름</th>
		<th colspan=8>설명 or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>시작</td>
		<td class='powderblued'>크기</td>
		<td class='powderblued'>릴레이</td>
		<td class='powderblued'>Bit 7</td>
		<td class='powderblued'>Bit 6</td>
		<td class='powderblued'>Bit 5</td>
		<td class='powderblued'>Bit 4</td>
		<td class='powderblued'>Bit 3</td>
		<td class='powderblued'>Bit 2</td>
		<td class='powderblued'>Bit 1</td>
		<td class='powderblued'>Bit 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>Set CIFX Control = 1001</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>Slot 번호 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>제어 그룹 = 1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>1</td>
		<td>통신 재시작</td>
		<td colspan=8>0 -> 1 값 변경시 재시작 요청</td>
	</tr>
	<tr>
		<td>5</td>
		<td>1</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>6</td>
		<td>1</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>7</td>
		<td>1</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>8</td>
		<td>2</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>10</td>
		<td>2</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>12</td>
		<td>8</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>