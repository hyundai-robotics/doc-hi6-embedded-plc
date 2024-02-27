# 3.4.1 S 릴레이 - 고정영역

항목이 고정 제공되는 SB0 ~ SB1999 영역은 아래 표를 참고하십시오.

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
.bit { width: 10%; }
</style>

### 특수 플래그 (special flags) 영역

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
	<tr>
		<td>SB3</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td>T/P 부팅 완료시 on</td>
		<td></td>
	</tr>
</tbody>
</table>

<br>

### 기본 정보 (basic information) 영역

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
		<td>SW6</td>
		<td>날짜/시간 : 년</td>
	</tr>
	<tr>
		<td>SB8</td>
		<td>날짜/시간 : 월</td>
		<td></td>
	</tr>
	<tr>
		<td>SB9</td>
		<td>날짜/시간 : 일</td>
		<td></td>
	</tr>	
	<tr>
		<td>SB10</td>
		<td>날짜/시간 : 시</td>
		<td></td>
	</tr>	
	<tr>
		<td>SB11</td>
		<td>날짜/시간 : 분</td>
		<td></td>
	</tr>	
	<tr>
		<td>SB12</td>
		<td>날짜/시간 : 초</td>
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
		<td>SB30</td>
		<td>로봇 상태 정보 1
		</br>(b0 = 건 출력)</br>
		</td>
		<td></td>
	</tr>
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
		<td>SW62</td>
		<td>간접주소지정 (relay-2)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW64</td>
		<td>간접주소지정 (relay-4)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW66</td>
		<td>간접주소지정 (relay-6)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW68</td>
		<td>간접주소지정 (relay-8)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW70</td>
		<td>간접주소지정 (relay-10)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW72</td>
		<td>간접주소지정 (relay-12)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW74</td>
		<td>간접주소지정 (relay-14)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW76</td>
		<td>간접주소지정 (relay-16)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW78</td>
		<td>간접주소지정 (relay-18)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB88</br>
		...</br>
		SB99</td>
		<td>T/P키 입력상태</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB111</td>
		<td>가동시간 선택<br>
		(1=통산(초기화 후), 2=통산(전원투입 후), 3=마지막사이클, 4=현재사이클</td>
		<td></td>
	</tr>
	<tr>
		<td>SL112</td>
		<td>모터 on (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL116</td>
		<td>모터 on (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL120</td>
		<td>가동시간 (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL124</td>
		<td>가동시간 (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL128</td>
		<td>이동시간 (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL132</td>
		<td>이동시간 (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL136</td>
		<td>사이클 회수</td>
		<td></td>
	</tr>
	<tr>
		<td>SL140</td>
		<td>wait, di 대기시간 (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL144</td>
		<td>wait, di 대기시간 (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL148</td>
		<td>delay 대기시간 (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL152</td>
		<td>delay 대기시간 (ms)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB159</td>
		<td>축정보 선택<br>
		(1=현재위치(축각도), 2=현재위치(베이스좌표), 6=축속도, 7=모터속도<br>
		 10=부하율(I/Ir), 11=부하율(I/Ip), 13=부하율(연속), 15=엔코더온도<br>
		 18=축별누적거리</td>
		<td></td>
	</tr>
	<tr>
		<td>SF160</td>
		<td>1축 해당값</td>
		<td></td>
	</tr>
	<tr>
		<td>SF164</td>
		<td>2축 해당값</td>
		<td></td>
	</tr>
	<tr>
		<td>SF168</td>
		<td>3축 해당값</td>
		<td></td>
	</tr>
	<tr>
		<td>SF172</td>
		<td>4축 해당값</td>
		<td></td>
	</tr>
	<tr>
		<td>SF176</td>
		<td>5축 해당값</td>
		<td></td>
	</tr>
	<tr>
		<td>SF180</td>
		<td>6축 해당값</td>
		<td></td>
	</tr>
	<tr>
		<td>SF184</td>
		<td>7축 해당값</td>
		<td></td>
	</tr>
	<tr>
		<td>SF188</td>
		<td>8축 해당값</td>
		<td></td>
	</tr>
	<tr>
		<td>SF192</td>
		<td>9축 해당값</td>
		<td></td>
	</tr>
	<tr>
		<td>SF196</td>
		<td>10축 해당값</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SL200</td>
		<td>각 축별 제어상태 (0=off, 1=on)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW210</br>
		...</br>
		SW280</td>
		<td>프로그램 번호</br>
		(main task = sw210, subtask 1 = sw220, subtask 2 = sw230, subtask 3 = sw240,</br>
		subtask 4 = sw250, subtask 5 = sw260, subtask 6 = sw270, subtask 7 = sw280)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW212</br>
		...</br>
		SW282</td>
		<td>스텝 번호</br>
		(main task = sw212, subtask 1 = sw222, subtask 2 = sw232, subtask 3 = sw242,</br>
		subtask 4 = sw252, subtask 5 = sw262, subtask 6 = sw272, subtask 7 = sw282)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW214</br>
		...</br>
		SW284</td>
		<td>펑션 번호</br>
		(main task = sw214, subtask 1 = sw224, subtask 2 = sw234, subtask 3 = sw244,</br>
		subtask 4 = sw254, subtask 5 = sw264, subtask 6 = sw274, subtask 7 = sw284)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW216</br>
		...</br>
		SW286</td>
		<td>메인 프로그램 번호</br>
		(main task = sw216, subtask 1 = sw226, subtask 2 = sw236, subtask 3 = sw246,</br>
		subtask 4 = sw256, subtask 5 = sw266, subtask 6 = sw276, subtask 7 = sw286)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW500</td>
		<td>건번호 (0=현재 선택된 건번호, 1~16)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW502</td>
		<td>건서치 상태 (1=완료, 0=미완료)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW504</td>
		<td>이동전극 마모량 x 100</td>
		<td></td>
	</tr>
	<tr>
		<td>SW506</td>
		<td>고정전극 마모량 x 100</td>
		<td></td>
	</tr>
	<tr>
		<td>SW508</td>
		<td>가압력 지령값 x 10</td>
		<td></td>
	</tr>
	<tr>
		<td>SW510</td>
		<td>가압력 현재값 x 10</td>
		<td></td>
	</tr>
</tbody>
</table>


<br>

### 산업용 통신 상태 (CIFX PCI Status) 영역

##### Slot 1 : SB 1000 ~ SB 1199
##### Slot 2 : SB 1200 ~ SB 1399
##### Slot 3 : SB 1400 ~ SB 1599


<table class="tg">
<thead>
	<tr>
		<td colspan=2>SB</td>
		<th>이름</th>
		<th colspan=8>설명 or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<th>시작</th>
		<th>크기</th>
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
		<td>4</td>
		<td>채널 상태</td>
		<td class='grayed'></td>
		<td>Restart 가능</td>
		<td>Restart 필요</td>
		<td>Config New</td>
		<td>Config Lock</td>
		<td>Bus On</td>
		<td>Run</td>
		<td>Ready</td>
	</tr>
	<tr>
		<td>4</td>
		<td>4</td>
		<td>채널 상태</td>
		<td colspan=8>0 = Unknown, <br> 1 =  Not Configured, <br> 2 = Stop, <br> 3 = Idle, <br> 4 = Operate</td>
	</tr>
	<tr>
		<td>8</td>
		<td>4</td>
		<td>통신 에러 코드</td>
		<td colspan=8>0 = 정상, <br> 그외 =  Error Code (32Bit Hexa)</td>
	</tr>
	<tr>
		<td>12</td>
		<td>2</td>
		<td>상태 진단 버전</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>14</td>
		<td>2</td>
		<td>Watchdog Timeout (ms)</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>16</td>
		<td>1</td>
		<td>Input Data Handshake Mode</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>17</td>
		<td>-</td>
		<td></td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>18</td>
		<td>1</td>
		<td>Output Data Handshake Mode</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>19</td>
		<td>-</td>
		<td></td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>20</td>
		<td>4</td>
		<td>Host System Watchdog</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>24</td>
		<td>4</td>
		<td>통신에러 누적 횟수</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>28</td>
		<td>-</td>
		<td></td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>29</td>
		<td>1</td>
		<td>Input Data Handshake Error</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>30</td>
		<td>1</td>
		<td>Output Data Handshake Error</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td colspan=11>Status (Master Only)</td>
	</tr>
	<tr>
		<td>40</td>
		<td>4</td>
		<td>슬레이브 통신 상태</td>
		<td colspan=8>0 = Unknown, <br> 1 = OK, <br> 2 = FAILED</td>
	</tr>
	<tr>
		<td>48</td>
		<td>4</td>
		<td>연결된 슬레이브 수</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>52</td>
		<td>4</td>
		<td>정상동작 슬레이브 수</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>56</td>
		<td>4</td>
		<td>진단 슬레이브 수</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>64</td>
		<td>1</td>
		<td>Global Bits <br> (DeviceNet Master)</td>
		<td>중복 MAC ID 확인중</td>
		<td>중복된 MAC ID</td>
		<td>Host 준비 안됨</td>
		<td>Bus Event Error</td>
		<td rowspan=2>Fatal Error</td>
		<td rowspan=2>Not Exchange Error</td>
		<td rowspan=2>Auto Clear Error</td>
		<td rowspan=2>Control Error</td>
	</tr>
	<tr>
		<td>64</td>
		<td>1</td>
		<td>Global Bits <br> (Profibus Master)</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td>TimeOut</td>
		<td>Host 준비 안됨</td>
	</tr>
	<tr>
		<td>64</td>
		<td>4</td>
		<td>알람 횟수</td>
		<td colspan=8>EtherNet/IP Master Only</td>
	</tr>
	<tr>
		<td>65</td>
		<td>1</td>
		<td>마스터 상태</td>
		<td colspan=8>DeviceNet <br> 0x00 = Offline, <br> 0x40 = Stop, <br> 0x80 = Idle, <br> 0xC0 = Run <br> Profibus <br> 0x00 = Offline, <br> 0x40 = Stop, <br> 0x80 = Clear, <br> 0xC0 = Operate</td>
	</tr>
	<tr>
		<td>66</td>
		<td>1</td>
		<td>에러 스테이션 번호</td>
		<td colspan=8>DeviceNet Master Only</td>
	</tr>
	<tr>
		<td>67</td>
		<td>1</td>
		<td>에러 코드</td>
		<td colspan=8>DeviceNet Master Only <br> 52 = Unknown process data handshake mode, <br> 53 = Baudrate 에러, <br> 54 = MAC ID 에러, <br> 57 = 중복된 MAC ID, <br> 58 = 디바이스 없음, <br> 210 = 통신 설정 없음, <br> 212 = 통신 설정 읽기 실패, <br> 220 = User Watchdog Fail, <br> 221 = User Data 응답 없음, <br> 223 = 마스터 Stop (CAN Bus Off), <br> 226 = 해당 장치가 마스터 장치가 아님</td>
	</tr>
	<tr>
		<td>68</td>
		<td>2</td>
		<td>Bus Data 송수신 이상 횟수</td>
		<td colspan=8>DeviceNet Master Only</td>
	</tr>
	<tr>
		<td>68</td>
		<td>4</td>
		<td>경고 횟수</td>
		<td colspan=8>EtherNet/IP Master Only</td>
	</tr>
	<tr>
		<td>70</td>
		<td>2</td>
		<td>Bus Off 에러 횟수</td>
		<td colspan=8>DeviceNet Master Only</td>
	</tr>
	<tr>
		<td>72</td>
		<td>4</td>
		<td>Bus 에러 코드</td>
		<td colspan=8>DeviceNet Master Only</td>
	</tr>
	<tr>
		<td>72</td>
		<td>4</td>
		<td>에러 횟수</td>
		<td colspan=8>EtherNet/IP Master Only</td>
	</tr>
	<tr>
		<td>76</td>
		<td>4</td>
		<td>에러 레벨</td>
		<td colspan=8>EtherNet/IP Master Only <br> 알람, 경고, 에러</td>
	</tr>
	<tr>
		<td>80</td>
		<td>4</td>
		<td>에러 코드</td>
		<td colspan=8>EtherNet/IP Master Only </td>
	</tr>
	<tr>
		<td>84</td>
		<td>4</td>
		<td>에러 코드 파라미터</td>
		<td colspan=8>EtherNet/IP Master Only </td>
	</tr>
	<tr>
		<td>88</td>
		<td>4</td>
		<td>에러 발생 Source Line</td>
		<td colspan=8>EtherNet/IP Master Only </td>
	</tr>
	<tr>
		<td>92</td>
		<td>12</td>
		<td>에러 발생 Source Identifier</td>
		<td colspan=8>EtherNet/IP Master Only </td>
	</tr>
	<tr>
		<td colspan=11>Slave Node Status (Master Only)</td>
	</tr>
	<tr>
		<td>80</td>
		<td>8</td>
		<td>슬레이브 리스트 1</td>
		<td colspan=8>(DeviceNet Master) 활성 슬레이브  (0 ~ 63) <br>  <br>(Profibus Master) 연결된 슬레이브 (0 ~ 63) </td>
	</tr>
	<tr>
		<td>88</td>
		<td>8</td>
		<td>슬레이브 리스트 2</td>
		<td colspan=8>(DeviceNet Master) 비활성된 슬레이브  (0 ~ 63) <br>  <br>(Profibus Master) 연결된 슬레이브 (64 ~ 127) </td>
	</tr>
	<tr>
		<td>96</td>
		<td>8</td>
		<td>슬레이브 리스트 3</td>
		<td colspan=8>(DeviceNet Master) Explicit Message 가능한 슬레이브  (0 ~ 63) <br>  <br>(Profibus Master) IO 교환 중인 슬레이브 (0 ~ 63) </td>
	</tr>
	<tr>
		<td>104</td>
		<td>8</td>
		<td>슬레이브 리스트 4</td>
		<td colspan=8>(DeviceNet Master) IO 교환 중인 슬레이브  (0 ~ 63) <br>  <br>(Profibus Master) IO 교환 중인 슬레이브 (64 ~ 127) </td>
	</tr>
	<tr>
		<td>112</td>
		<td>8</td>
		<td>슬레이브 리스트 5</td>
		<td colspan=8>(DeviceNet Master) 진단 중인 슬레이브  (0 ~ 63) <br>  <br>(Profibus Master) 진단 중인 슬레이브 (0 ~ 63) </td>
	</tr>
	<tr>
		<td>120</td>
		<td>8</td>
		<td>슬레이브 리스트 6</td>
		<td colspan=8>(Profibus Master) 진단 중인 슬레이브 (64 ~ 127) </td>
	</tr>
	<tr>
		<td colspan=11>Slave Node Status (Extended Status Field) (Master Only)</td>
	</tr>
	<tr>
		<td>128</td>
		<td>16</td>
		<td>슬레이브 리스트 7</td>
		<td colspan=8>(DeviceNet Master) 연결된 슬레이브  (0 ~ 63) <br>  <br>(Profibus / EtherNet IP / Profinet IO / EtherCAT Master) <br> 연결된 슬레이브 (0 ~ 127) </td>
	</tr>
	<tr>
		<td>144</td>
		<td>16</td>
		<td>슬레이브 리스트 8</td>
		<td colspan=8>(DeviceNet Master) 활성 슬레이브  (0 ~ 63) <br>  <br> (Profibus / EtherNet IP / Profinet IO / EtherCAT Master) <br> IO 교환 중인 슬레이브 (0 ~ 127) </td>
	</tr>
	<tr>
		<td>160</td>
		<td>16</td>
		<td>슬레이브 리스트 9</td>
		<td colspan=8>(DeviceNet Master) 진단 중인 슬레이브  (0 ~ 63) <br>  <br> (Profibus / EtherNet IP / Profinet IO / EtherCAT Master) <br> 진단 중인 슬레이브 (0 ~ 127) </td>
	</tr>
	<tr>
		<td>176</td>
		<td>16</td>
		<td>슬레이브 리스트 10</td>
		<td colspan=8>(Profibus Master) Slave 최신 Input Data Update (0 ~ 127) </td>
	</tr>
</tbody>
</table>
