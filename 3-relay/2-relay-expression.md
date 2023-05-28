# 3.2 릴레이의 표기

Hi6 로봇제어기 내장PLC에서의 릴레이 표기는 아래와 같습니다.

`[FB{block-index}.]{relay-type}[{data-type}]{signal-index}`

예를 들어, 아래와 같이 표기됩니다.

Y1501
FB3.DIW21

* block-index  
입출력 릴레이(DI, DO, X, Y)는 객체명이 FB0 ~ FB9인 10개의 필드버스 블럭(fieldbus block)으로 그룹핑되어 있습니다. 물리적인 입출력의 경우 각 블럭은 각기 개별적인 필드버스 장치에 매핑됩니다.
하나의 FB의 크기는 입출력 각각 120 바이트(=960 bit)입니다.

  FB의 일부 영역을 FN0 ~ FN63의 객체명으로 매핑해 사용할 수도 있습니다. FN영역을 설정하는 방법은 아래 링크를 참조하십시오.

  [조작설명서: 7.3.2.12 fn 블럭 할당](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/7-setting/3-control-parameter/2-io-signal-setting/12-fn-block)

* relay-type  
아래와 같이 총 10가지 type이 있습니다.
각각의 type은 뒤에서 자세히 설명됩니다.

  1) DI (Digital Input) : HRScript나 각종 입력 할당에서 사용할 수 있는 논리적인 입력(Logical Input) 신호입니다.

  2) DO (Digital Output) : HRScript나 각종 출력 할당에서 사용할 수 있는 논리적인 출력(Logical Output) 신호입니다.

  3) SI (System Input) : 당사 시스템 보드와 인터페이스 되는 전용입력 신호입니다.

  4) SO (System Output) : 당사 시스템 보드와 인터페이스 되는 전용출력 신호입니다.

  5) X : 필드버스 장치를 통해 제어기 외부로부터 입력되는 물리적인 입력(Physical Input) 신호입니다.

  6) Y : 필드버스 장치를 통해 제어기 외부로 출력되는 물리적인 출력(Physical Output) 신호입니다. 

  7) M (Memory) : Data를 저장할 때 사용하며, HRScript에서도 access할 수 있습니다.

  8) S (System) : 제어기 내의 시스템 값을 읽거나 쓰는 용도입니다. [3.4 S 릴레이](./4-sw-relay/README.md)를 참조하세요.

  9) R (auxiliaRy) : Obsolete. 값을 임시로 보관하기 위한 보조 릴레이입니다. Hi5a 래더파일의 이식 편의를 위해 제공됩니다. 신규 래더 파일에서는 M 릴레이 사용을 권장합니다.

  10) K (Keep) : Obsolete. 값을 임시로 보관하기 위한 보조 릴레이이며 전원을 꺼도 값이 보관됩니다. Hi5a 래더파일의 이식 편의를 위해 제공됩니다. 신규 래더 파일에서는 M 릴레이 사용을 권장합니다.


    | ** 릴레이 명칭** | ** 점 수 ** | ** 릴레이(bit) ** |** 릴레이(byte) ** |
    | :--- | :--- | :--- | :--- |
    | DI | 9600 bit (1280 byte) | FB0.DI0 ~ FB9.DI959 | FB0.DIB0 ~ FB9.DIB127 |
    | DO | 9600 bit (1280 byte) | FB0.DO0 ~ FB9.DO959 | FB0.DOB0 ~ FB9.DOB127 |
    | SI | 960 bit (128 byte) | SI0 ~ SI959 | SIB0 ~ SIB127 |
    | SO | 960 bit (128 byte) | SO0 ~ SO959 | SOB0 ~ SOB127 |
    | X | 9600 bit (1280 byte) | FB0.X0 ~ FB9.X959 | FB0.XB0 ~ FB9.XB127 |
    | Y | 9600 bit (1280 byte) | FB0.Y0 ~ FB9.Y959 | FB0.YB0 ~ FB9.YB127 |
    | M | 160000 bit (20000 byte) | M0 ~ M159999 | MB0 ~ MB19999 |
    | S | 160000 bit (20000 byte) | S0 ~ S159999 | SB0 ~ SB19999 |
    | R | 960 bit (128 byte) | R0 ~ R959 | RB0 ~ RB127 |
    | K | 960 bit (128 byte) | K0 ~ K959 | KB0 ~ KB127 |

* data-type  
아래와 같이 5가지 type이 있습니다.

  * 표기없음 : 비트 (bit), 1bit
  * B : 부호있는 바이트 (signed-byte), 8bit
  * W : 부호있는 워드 (signed-word), 16bit
  * L : 부호있는 롱 (signed-long), 32bit
  * F : 부동소수점 실수 (floating-point real), 32bit

  <br>
  이들은 별개의 메모리 공간이 아니라 같은 960 bit의 공간을 서로 다른 데이터형으로 표현한 것입니다. 예를 들어 DO[0~15]와 DOB[0~1], DOW[0]은 모두 동일한 출력신호입니다.

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

* signal-index
relay-type 내에서의 0-based 인덱스입니다.  
인덱스는 DO는 bit단위, DOB, DOW, DOL, DOF는 byte단위로 매겨집니다.

<br>
<br>

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

