# 3.2 릴레이의 표기

${cont_model} 로봇제어기 내장PLC에서의 릴레이 표기는 아래와 같습니다.

`[FB{block-index}.]{relay-type}[{data-type}]{signal-index}`

예를 들어, 아래와 같이 표기됩니다.

Y1501
FB3.DIW21

### block-index  
입출력 릴레이(DI, DO, X, Y)는 객체명이 FB0 ~ FB9인 10개의 필드버스 블럭(fieldbus block)으로 그룹핑되어 있습니다. 물리적인 입출력의 경우 각 블럭은 각기 개별적인 필드버스 장치에 매핑됩니다.
하나의 FB의 크기는 입출력 각각 120 바이트(=960 bit)입니다.

  FB의 일부 영역을 FN0 ~ FN63의 객체명으로 매핑해 사용할 수도 있습니다. FN영역을 설정하는 방법은 아래 링크를 참조하십시오.

  [조작설명서: 7.3.2.12 fn 블럭 할당](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/ko-tp630/7-system/3-control-parameter/2-io-signal-setting/12-fn-block?cont_model=${cont_model})

### relay-type  
아래와 같이 총 10가지 type이 있습니다.
각각의 type은 뒤에서 자세히 설명됩니다.

-  DI (Digital Input) : HRScript나 각종 입력 할당에서 사용할 수 있는 논리적인 입력(Logical Input) 신호입니다.
-  DO (Digital Output) : HRScript나 각종 출력 할당에서 사용할 수 있는 논리적인 출력(Logical Output) 신호입니다.
-  SI (System Input) : 당사 시스템 보드와 인터페이스 되는 전용입력 신호입니다.
-  SO (System Output) : 당사 시스템 보드와 인터페이스 되는 전용출력 신호입니다.
-  X : 필드버스 장치를 통해 제어기 외부로부터 입력되는 물리적인 입력(Physical Input) 신호입니다.
- Y : 필드버스 장치를 통해 제어기 외부로 출력되는 물리적인 출력(Physical Output) 신호입니다. 
- M (Memory) : Data를 저장할 때 사용하며, HRScript에서도 access할 수 있습니다.
- S (System) : 제어기 내의 시스템 값을 읽거나 쓰는 용도입니다. [3.4 S 릴레이](./4-sw-relay/README.md)를 참조하세요.
- R (auxiliaRy) : 값을 임시로 보관하기 위한 보조 릴레이입니다. 
- K (Keep) : 값을 임시로 보관하기 위한 보조 릴레이이며 전원을 꺼도 값이 보관됩니다. 
- T (Timer) : 타이머 동작을 위한 릴레이며, 값이 0일 때 접점이 On됩니다. 
- C (Counter) : 카운터 동작을 위한 릴레이며, 값이 0일 때 접점이 On 됩니다.  
  
<style type="text/css">
  .relay-table {
    border-collapse: collapse;
    /* width를 지정하지 않거나 auto로 두면 내용물에 폭이 딱 맞춰집니다 */
    width: auto; 
    font-family: sans-serif;
    font-size: 12px;
  }
  
  .relay-table th, 
  .relay-table td {
    border: 1px solid #a0a0a0;
    /* 상하 패딩 6px, 좌우 패딩 2px (완전 0보다 가독성을 위해 2px 추천) */
    padding: 6px 2px;
    text-align: center;
    /* 내용이 길어도 줄바꿈되지 않고 한 줄로 나오게 하여 폭을 압축 */
    white-space: nowrap; 
    font-size: 12px;
  }

  .relay-table th {
    background-color: #efefef;
    color: black;
    font-weight: bold;
  }

  /* 홀수 줄 배경색 (선택사항: 가독성 향상) */
  .relay-table tbody tr:nth-child(odd) {
    background-color: #ffffff;
  }
  .relay-table tbody tr:nth-child(even) {
    background-color: #f9f9f9;
  }
</style>

<table class="relay-table">
  <thead>
    <tr>
      <th>릴레이 <br>명칭</th>      <th>점 수</th>      <th>릴레이 <br>(bit)</th>      <th>릴레이 <br>(byte)</th>      <th>릴레이 <br>(word)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>DI</td>      <td>9600 bits (1200 bytes)</td>      <td>FB0.DI0-FB9.DI959</td>      <td>FB0.DIB0 ~ FB9.DIB119</td>      <td>FB0.DIW0 ~ FB9.DIW118</td> 
    </tr>
    <tr>
      <td>DO</td>      <td>9600 bits (1200 bytes)</td>      <td>FB0.DO0-FB9.DO959</td>      <td>FB0.DOB0 ~ FB9.DOB119</td>      <td>FB0.DOW0 ~ FB9.DOW118</td>
    </tr>
    <tr>
      <td>SI</td>      <td>960 bits (120 bytes)</td>      <td>SI0-SI959</td>      <td>SIB0 ~ SIB119</td>      <td>SIW0 ~ SIW118</td>
    </tr>
    <tr>
      <td>SO</td>      <td>960 bits (120 bytes)</td>      <td>SO0-SO959</td>      <td>SOB0 ~ SOB119</td>      <td>SOW0 ~ SOW118</td>
    </tr>
    <tr>
      <td>X</td>      <td>9600 bits (1200 bytes)</td>      <td>FB0.X0-FB9.X959</td>      <td>FB0.XB0 ~ FB9.XB119</td>      <td>FB0.XW0 ~ FB9.XW118</td>
      </tr>      
    <tr>
      <td>Y</td>      <td>9600 bits (1200 bytes)</td>      <td>FB0.Y0-FB9.Y959</td>      <td>FB0.YB0 ~ FB9.YB119</td>      <td>FB0.YW0 ~ FB9.YW118</td>
    </tr>
    <tr>
      <td>M</td>      <td>160000 bits (20000 bytes)</td>      <td>M0-M159999</td>      <td>MB0-MB19999</td>      <td>MW0 ~ MW19998</td>
    </tr>
    <tr>
      <td>S</td>      <td>160000 bits (20000 bytes)</td>      <td>S0-S159999</td>      <td>SB0-SB19999</td>      <td>SW0 ~ SW19998</td>
    </tr>
    <tr>
      <td>R</td>      <td>960 bits (128 bytes)</td>      <td>R0-R959</td>      <td>RB0 ~ RB127</td>      <td>RW0 ~ RW126</td>
    </tr>
    <tr>
      <td>K</td>      <td>960 bits (128 bytes)</td>      <td>K0-K959</td>      <td>KB0 ~ KB127</td>      <td>KW0 ~ KW126</td>
    </tr>
    <tr>
      <td>T</td>      <td>256 DWORD (1024 bytes)</td>      <td>T0-T255</td>      <td>-</td>      <td>-</td>
    </tr>
    <tr>
      <td>C</td>      <td>256 DWORD (1024 bytes)</td>      <td>C0-C255</td>      <td>-</td>      <td>-</td>
    </tr>
  </tbody>
</table>

<div class="page-break"></div>

### data-type  
아래와 같이 5가지 type이 있습니다.

  * 표기없음 : 비트 (bit), 1bit
  * B : 부호있는 바이트 (signed-byte), 8bit
  * W : 부호있는 워드 (signed-word), 16bit
  * L : 부호있는 롱 (signed-long), 32bit
  * F : 부동소수점 실수 (floating-point real), 32bit

  이들은 별개의 메모리 공간이 아니라 같은 960 bit의 공간을 서로 다른 데이터형으로 표현한 것입니다. 예를 들어 DO[0~15]와 DOB[0~1], DOW[0]은 모두 동일한 출력신호입니다.

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

### signal-index
relay-type 내에서의 0-based 인덱스입니다.  
인덱스는 DO는 bit단위, DOB, DOW, DOL, DOF는 byte단위로 매겨집니다.

FB 객체명은 아래와 같이 생략할 수도 있습니다. 예를 들어 DO961은 FB1.DO1과 동일한 표기입니다.

| **객체명** | **DO 표기** | **FB.DO 표기** |
| :--- | :--- | :--- |
| FB0 | DO0 ~ DO959 | FB0.DO0 ~ FB0.DO959 |
| FB1 | DO960 ~ DO1919 | FB1.DO0 ~ FB1.DO959 |
| FB2 | DO1920 ~ DO2879 | FB2.DO0 ~ FB2.DO959 |
| FB3 | DO2880 ~ DO3839 | FB3.DO0 ~ FB3.DO959 |
| FB4 | DO3840 ~ DO4799 | FB4.DO0 ~ FB4.DO959 |
| FB5 | DO4800 ~ DO5759 | FB5.DO0 ~ FB5.DO959 |
| FB6 | DO5760 ~ DO6719 | FB6.DO0 ~ FB6.DO959 |
| FB7 | DO6720 ~ DO7679 | FB7.DO0 ~ FB7.DO959 |
| FB8 | DO7680 ~ DO8639 | FB8.DO0 ~ FB8.DO959 |
| FB9 | DO8640 ~ DO9599 | FB9.DO0 ~ FB9.DO959 |

DI, DO는 각기 논리적인 입력과 출력으로서 로봇언어와 입출력 할당에서 접근할 수 있습니다.

