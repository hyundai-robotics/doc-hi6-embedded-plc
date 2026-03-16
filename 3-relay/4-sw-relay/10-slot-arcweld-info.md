# 3.4.10 S 릴레이 - ARCWELD_INFO

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

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
		<td>GET_ARCTWELD_INFO (3000) - 입력</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>트윈용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>용접 전류</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>용접 전압</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>용접기 에러</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>와이어 피딩속도</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
  
<div class="page-break"></div>

하기의 서비스는 V60.32-00 이후부터 지원합니다.
<br>
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
		<td>GET_ARCTWELD_INFO (3001) - 입력</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>트윈용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>피드 모터 전류</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>심트레킹 데이터</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>용접 프로세서</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td></td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
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
		<td>GET_ARCTWELD_INFO (3002) - 입력</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>트윈용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>용접기 전체 동작시간(s)</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>용접기 버전 - 하위(Vx.x.255)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>용접기 버전 - 중간(Vx.255.x)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>용접기 버전 - 상위(V255.x.x)</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
  
<div class="page-break"></div>

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
		<td>GET_ARCTWELD_INFO (3004) - 입력</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>트윈용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>
			0x01 = WCR(와이어 접축상태) <br>
			0x02 = 토치 충돌 <br>
			0x04 = 용접전원 OK <br>
			0x08 = 와이어 스틱상태 <br>
			0x10 = 용접기 에러 <br>
			0x20 = 프로세스 활성 <br>
			0x40 = 통신 상태 <br>
			0x80 = 와이어 사용가능 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 토치 상태 <br>
			0x02 = 인칭 상태 <br>
			0x04 = 역인칭 상태 <br>
			0x08 = 가스체크 <br>
			0x10 = 시너직 사용가능 <br>
			0x20 = 리밋 상태 <br>
			0x40 = 설정범위 초과 <br>
		</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>
  
<div class="page-break"></div>

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
		<td>GET_ARCTWELD_INFO (3005) - 출력</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>트윈용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>용접 전류</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>용접 전압</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>Job/Prog 번호</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>동작 모드</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>16</td>
		<td>시너직 코드</td>
		<td>s2</td>
	</tr>
</tbody>
</table>

<br>
  
<div class="page-break"></div>

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
		<td>GET_ARCTWELD_INFO (3006) - 출력</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>트윈용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>펄스 다이나믹 보정</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>와이어 번백</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>프로세스 제어</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>아크 특성</td>
		<td>f4</td>
	</tr>
</tbody>
</table>

<br>
  
<div class="page-break"></div>

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
		<td>GET_ARCTWELD_INFO (3007) - 출력</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>트윈용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>와이어 재질</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>와이어 직경</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>가스 타입</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>7</td>
		<td>용접 모드</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>트윈 동작 모드</td>
		<td>s1</td>
	</tr>
</tbody>
</table>

<br>

<div class="page-break"></div>

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
		<td>GET_ARCTWELD_INFO (3009) - 출력</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>트윈용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>
			0x01 = 아크 on <br>
			0x02 = 로봇 준비 <br>
			0x04 = 마스터 토치 선택 <br>
			0x08 = 가스 on <br>
			0x10 = 와이어 인칭 <br>
			0x20 = 와이어 역인칭 <br>
			0x40 = 용접기 에러 리셋 <br>
			0x80 = 와이어 스틱체크 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>
			0x01 = 용접 시뮬레이션 <br>
			0x02 = 필럿 아크 <br>
			0x04 = 리프트 아크 사용 <br>
			0x08 = 수퍼 펄스 사용 <br>
			0x10 = 온라인 상태 <br>
			0x20 = Job 모드 활성 <br>
			0x40 = 전압 설정 모드 <br>
			0x80 = 전류 설정 모드 <br>
		</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>
			0x01 = 로봇 토치 충돌 <br>
			0x02 = 로봇 에러 상태 <br>
		</td>
		<td>s1</td>
	</tr>	
</tbody>
</table>

<br>
  
<div class="page-break"></div>

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
		<td>GET_ARCTWELD_INFO (3010) - 상태</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>3</td>
		<td>param 2</td>
		<td>트윈용접기 번호 (0~1)</td>
		<td>s1</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>현재 아크on 조건 번호</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>현재 터치센싱 조건 번호</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>현재 위빙 조건 번호</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>현재 LVS 조건 번호</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>현재 arccond 조건 번호</td>
		<td>s2</td>
	</tr>
</tbody>
</table>
  
<div class="page-break"></div>
