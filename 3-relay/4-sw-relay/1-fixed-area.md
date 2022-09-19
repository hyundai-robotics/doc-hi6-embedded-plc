# 3.4.1 S 릴레이 - 고정영역

항목이 고정 제공되는 SB0 ~ SB1999 영역은 아래 표를 참고하십시오.

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.bit { width: 10%; }
</style>

<table class="tg">
<thead>
	<tr>
		<th class='bit'>릴레이</th>
		<th class='bit'>bit7</th>
		<th class='bit'>bit6</th>
		<th class='bit'>bit5</th>
		<th class='bit'>bit4</th>
		<th class='bit'>bit3</th>
		<th class='bit'>bit2</th>
		<th class='bit'>bit1</th>
		<th class='bit'>bit0</th>		
		<th class='bit'>비고</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>SB0</td>
		<td>연산에 carry가 있으면 on</td>
		<td>BCD연산 불가시 on</td>
		<td>1초 clock</td>
		<td>0.2초 clock</td>
		<td>0.1초 clock</td>
		<td>한 scan만 on</td>
		<td>상시 off</td>
		<td>상시 on</td>		
		<td></td>
	</tr>
	<tr>
		<td>SB1</td>
		<td class='grayed'></td>
		<td>Label이 0이하, Jump할 Label이 없을때 on</td>
		<td>Label이 중복될때 on</td>
		<td>Label이 100개 이상일때 on</td>
		<td>Label이 상수가 아닐때 on</td>
		<td>On이면 Y릴레이 직접출력 허용</td>
		<td>4초 clock</td>
		<td>2초 clock</td>
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
		<td>Call로 호출되는 subladder가 없을때 on</td>
		<td>Scan time이 5초를 초과할때 on</td>
		<td></td>
	</tr>
</tbody>
</table>

<br>

<table class="tg">
<thead>
	<tr>
		<th>릴레이</th>
		<th>설명</th>
		<th>비고</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>SB4</th>
		<td>PLC실행모드<br>
		(0=stop, 1=R.stop, 2=R.run, 3= run, 4=off, 5=프로그램 없음)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB14</td>
		<td>소프트웨어 버전 : first<br>
		e.g. V60.05-08인 경우, SB14:60, SB15:5, SB16:8</td>
		<td></td>
	</tr>
	<tr>
		<td>SB15</td>
		<td>소프트웨어 버전 : second</td>
		<td></td>
	</tr>
	<tr>
		<td>SB16</td>
		<td>소프트웨어 버전 : small-fix</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW18</td>
		<td>Scan time</td>
		<td>ms</td>
	</tr>
	<tr>
		<td>SW20</td>
		<td>할당 시간</td>
		<td>us</td>
	</tr>
	<tr>
		<td>SW22</td>
		<td>최대 점유시간</td>
		<td>ms</td>
	</tr>
	<tr>
		<td>SW24</td>
		<td>평균 점유시간</td>
		<td>ms</td>
	</tr>
	<tr>
		<td>SW26</td>
		<td>Ladder의 총 스텝수</td>
		<td></td>
	</tr>
	<tr>
		<td>SW28</td>
		<td>점유비율</td>
		<td>%</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB40</td>
		<td>현재 툴번호</td>
		<td></td>
	</tr>
	<tr>
		<td>SB41</td>
		<td>로봇 상태 (0=stop, 1=run, 2=wait)</td>
		<td></td>
	</tr>
	<tr>
		<td>SB42</td>
		<td>재생속도</td>
		<td>%</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW44</td>
		<td>수동속도</td>
		<td>mm/s</td>
	</tr>
	<tr>
		<td>SW46</td>
		<td>툴 끝 이동속도</td>
		<td>mm/s</td>
	</tr>
	<tr>
		<td>SW48</td>
		<td>에러/경고 번호</td>
		<td></td>
	</tr>
	<tr>
		<td>SW50</td>
		<td>에러/경고 보조정보</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW60</td>
		<td>간접주소지정 1</td>
		<td></td>
	</tr>
	<tr>
		<td>SW62</td>
		<td>간접주소지정 2</td>
		<td></td>
	</tr>
	<tr>
		<td>SW64</td>
		<td>간접주소지정 3</td>
		<td></td>
	</tr>
	<tr>
		<td>SW66</td>
		<td>간접주소지정 4</td>
		<td></td>
	</tr>
	<tr>
		<td>SW68</td>
		<td>간접주소지정 5</td>
		<td></td>
	</tr>
	<tr>
		<td>SW70</td>
		<td>간접주소지정 6</td>
		<td></td>
	</tr>
	<tr>
		<td>SW72</td>
		<td>간접주소지정 7</td>
		<td></td>
	</tr>
	<tr>
		<td>SW74</td>
		<td>간접주소지정 8</td>
		<td></td>
	</tr>
	<tr>
		<td>SW76</td>
		<td>간접주소지정 9</td>
		<td></td>
	</tr>
	<tr>
		<td>SW78</td>
		<td>간접주소지정 10</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB720<br>~<br>SB839</td>
		<td>sib[0~119]<br>(system input)</td>
		<td></td>
	</tr>
	<tr>
		<td>SB840<br>~<br>SB959</td>
		<td>sob[0~119]<br>(system output)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
</tbody>
</table>