# 5. Hi5a와 Hi6의 내장PLC 차이점

Hi6의 내장PLC 기능은 Hi5a의 내장PLC 기능과 유사하며, 동일한 래더 편집기 HRLadder를 사용합니다.
따라서 이미 Hi5a의 내장PLC 기능에 익숙한 사용자는, Hi6제어기에서 달라진 부분만을 확인하는 방식으로 이 설명서를 빠르게 학습할 수 있습니다.

아래는 달라진 부분의 리스트입니다.

<br>

## HRLadder online 연결

HRLadder v2.80부터 Hi6제어기를 지원합니다.  
HRLadder v2.80 미만 버전에서는 online 버튼을 누르면 제어기 종류(Hi4~Hi5a)를 자동 인식하여 원격 연결이 수행합니다.  
반면 HRLadder v2.80 이상 버전에서는 먼저 프로젝트의 속성에서 제어기 종류를 선택한 후 online 버튼을 누르십시오.

![](_assets/hrladder-prj-prop.png)

![](_assets/hrladder-prj-prop2.png)

<br>

## 릴레이 종류

### Hi5a

보조릴레이 R, 보존릴레이 K, 특수릴레이 SP가 존재합니다.
M릴레이는 MW1~1000을 지원합니다.

### Hi6

보조릴레이 R, 보존릴레이 K가 폐기되었습니다.
M릴레이가 MW0~MW19998 로 대폭 확대되었으므로, M릴레이로 대체하여 사용하십시오.
SP릴레이는 [S 릴레이 - 고정영역](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/korean/3-relay/4-sw-relay/1-fixed-area)의 특수 플래그 영역로서 통합되었습니다.  

<br>


## 인덱스(index)

### Hi5a
index가 1부터 시작합니다.
word, long, float 의 index가 1씩 증가합니다. 
예를 들어 DOW1 따라서, DO16~DO23은 DOW1과 같습니다.


<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table class="tg">
<tbody>
  <tr>
    <td class="tg-kftd">bit</td>
    <td>DO1~DO8</td>
    <td>DO9~DO16</td>
    <td>DO17~DO24</td>
    <td>DO25~DO32</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">byte</td>
    <td>DOB1</td>
    <td>DOB2</td>
    <td>DOB3</td>
    <td>DOB4</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">word</td>
    <td colspan="2">DOW1</td>
    <td colspan="2">DOW2</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">long</td>
    <td colspan="4">DOL1</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">float</td>
    <td colspan="4">DOF1</td>
    <td>...</td>
  </tr>
</tbody>
</table>

<br>

### Hi6
index가 0부터 시작합니다.
word, long, float 의 index가 byte 위치에 맞추어 증가합니다.
가령 DOW는 DOW0, DOW2, DOW4, DOW6...의 식으로 증가하고, DOL은 DOL0, DOL4, DOL8...의 식의 증가합니다.
아래 그림에서, 볼 수 있듯이 DO16~DO23은 DOW2와 같습니다.

[3.2 릴레이의 표기](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/korean/3-relay/2-relay-expression)를 참조하십시오.

<br>

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table class="tg">
<tbody>
  <tr>
    <td class="tg-kftd">bit</td>
    <td>DO0~DO7</td>
    <td>DO8~DO15</td>
    <td>DO16~DO23</td>
    <td>DO24~DO31</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">byte</td>
    <td>DOB0</td>
    <td>DOB1</td>
    <td>DOB2</td>
    <td>DOB3</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">word</td>
    <td colspan="2">DOW0</td>
    <td colspan="2">DOW2</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">long</td>
    <td colspan="4">DOL0</td>
    <td>...</td>
  </tr>
  <tr>
    <td class="tg-kftd">float</td>
    <td colspan="4">DOF0</td>
    <td>...</td>
  </tr>
</tbody>
</table>

<br>


## 시스템 릴레이 (SW relay)

### Hi5a

거의 모니터링 항목에 각기 정해진 SW릴레이 인덱스 주소가 있습니다.  
단, 인덱스 주소 중 SW220~249는 10개의 다용도 슬롯(slot)이며, 시스템변수, 메인보드 저장공간, 아날로그 입출력, 날짜/시간, GE변수 중 원하는 코드를 원하는 슬롯에 넣어 모니터링합니다.

<br>

### Hi6

SB0~SB1999 영역은 Hi5a와 같이 항목마다 정해진 인덱스 주소를 갖는 [S 릴레이 고정 영역](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/korean/3-relay/4-sw-relay/1-fixed-area)입니다.

반면 SB2000~ 영역은 900개의 다용도 슬롯(slot)으로 구성되어 있어서 원하는 항목의 command를 널어 사용할 수 있는 [선택 항목 영역](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/korean/3-relay/4-sw-relay/README)입니다.

