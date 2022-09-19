# 3.4 S 릴레이

Hi6 제어기 내의 다양한 상태값이 S릴레이에 매핑되어 있습니다. 또한 일부 S릴레이에 값을 써서 Hi6의 상태를 바꿀 수 있습니다.

따라서, 공정 PLC나 PC 같은 외부 장치는 필드버스, MODBUS 등을 통해 S 릴레이 값을 읽어 Hi6 제어기의 상태를 원격 모니터링할 수 있으며, S 릴레이에 값을 써서 Hi6 제어기를 원격 제어할 수 있습니다. 

S릴레이 영역은 아래와 같이 크게 2부분으로 나뉩니다.


<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
	<tr>
		<th>주소</th>
		<th>내용</th>
	</tr>
	<tr>
		<th>SB00000 ~ SB01999</th>
		<th>고정 항목 영역</th>
	</tr>
	<tr>
		<th>SB02000 ~ SB19999</th>
		<th>선택 항목 영역 (slots)</th>
	</tr>
</table>

<br>

### 고정 영역
자주 사용되는 기본적인 항목들이 미리 정해진 주소로 배치되어 있습니다. 설정을 통한 항목 변경과 배치가 불가능합니다. 다음 절에서 고정영역의 맵이 설명됩니다.

<br>

### 선택 항목 영역
20byte 크기의 slot들 900개로 구성되어 있습니다. 각 slot은 선두 word에 어떤 command 값을 넣느냐에 따라 구성이 결정됩니다. 각 command별 맵이 이어지는 절에서 설명됩니다.

<table class="tg">
<thead>
	<tr>
		<th>slot index</th>
		<th>s index:offset</th>
		<th>field</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td rowspan=10>slot 0</td>
		<td>2000:0</td>
		<td>command (관례: 짝수는 get, 홀수는 set)</td>
	</tr>
	<tr>
		<td>:2</td>
		<td rowspan=2>params</td>
	</tr>
	<tr>
		<td>:4</td>
	</tr>
	<tr>
		<td>:6</td>
		<td rowspan=5>results</td>
	</tr>
	<tr><td>:8</td></tr>
	<tr><td>:10</td></tr>
	<tr><td>:12</td></tr>
	<tr><td>:14</td></tr>
	<tr><td>:16</td><td class='grayed'></td></tr>
	<tr><td>:18</td><td class='grayed'></td></tr>
	<tr>
		<td rowspan=10>slot 1</td>
		<td>2020:0</td>
		<td>command</td>
	</tr>
	<tr>
		<td>:2</td>
		<td>params</td>
	</tr>
	<tr>
		<td>:4</td>
		<td rowspan=2>results</td>
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
		<td rowspan=3>slot 2</td>
		<td>2040:0</td>
		<td>command</td>
	</tr>
	<tr>
		<td>:2</td>
		<td>params</td>
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
		<td rowspan=3>slot 899</td>
		<td>19980:0</td>
		<td>command</td>
	</tr>
	<tr>
		<td>:2</td>
		<td>params</td>
	</tr>
	<tr>
		<td>...</td>
		<td>...</td>
	</tr>
</tbody>
</table>