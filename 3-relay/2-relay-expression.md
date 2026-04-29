# 3.2 Designating a relay

The following shows how the relays are designated in the embedded programmable logic controller (PLC) of the ${cont_model} robot controller.

`[FB{block-index}.]{relay-type}[{data-type}]{signal-index}`

For example, relays can be designated as below.

Y1501
FB3.DIW21

### block-index  
Input and output relays (DI, DO, X, Y) are grouped into 10 fieldbus blocks with their object names ranging from FB0 to FB9. For physical inputs and outputs, each block will be mapped to each fieldbus device.
The size of one fieldbus block is 120 bytes (=960 bits) for the input and output, respectively.

  You can also map some areas of FB to object names from FN0 to FN63.
  See the link below for instructions on how to set up the FN region.

  [Operation manual: 7.3.2.12 fn block allocation](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/en-tp630/7-system/3-control-parameter/2-io-signal-setting/12-fn-block?cont_model=${cont_model})


### relay-type  
There are 12 different types, as shown below.
Each will be explained in detail later.

- Digital Input (DI): This is a logical input signal that can be used in HRScript or for assigning various inputs.
- Digital Output (DO): This is a logical output signal that can be used in HRScript or for assigning various outputs.
- System Input (SI): This is a dedicated input signal that interfaces with the company"s system board.
- System Output (SO): This is a dedicated output signal that interfaces with the company"s system board.
- X: This is a physical input signal that is inputted from the outside of the controller via a fieldbus device.
- Y: This is a physical output signal that is outputted to the outside of the controller via a fieldbus device. 
- Memory (M): This can be used for storing data and can be accessed from HRScript.
- System (S): This is used to read or write system values in the controller. Refer to [3.4 S relay](./4-sw-relay/README.md).
- AuxiliaRy (R): This is an auxiliary relay for temporarily storing.
- Keep (K): This is an auxiliary relay for temporarily storing. The value will be stored even when the power is turned off. 
- Timer (T): Relays for timer operation, the contact is On when the value is 0. 
- Counter (C): Relays for counter operation, the contact is On when the value is 0. 

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
      <th>Relay<br>name</th>      <th>Number of points</th>      <th>Relay <br>(bit)</th>      <th>Relay <br>(byte)</th>      <th>Relay <br>(word)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>DI</td>      <td>9600 bits (1280 bytes)</td>      <td>FB0.DI0-FB9.DI959</td>      <td>FB0.DIB0 ~ FB9.DIB119</td>      <td>FB0.DIW0 ~ FB9.DIW118</td> 
    </tr>
    <tr>
      <td>DO</td>      <td>9600 bits (1280 bytes)</td>      <td>FB0.DO0-FB9.DO959</td>      <td>FB0.DOB0 ~ FB9.DOB119</td>      <td>FB0.DOW0 ~ FB9.DOW118</td>
    </tr>
    <tr>
      <td>SI</td>      <td>960 bits (128 bytes)</td>      <td>SI0-SI959</td>      <td>SIB0 ~ SIB119</td>      <td>SIW0 ~ SIW118</td>
    </tr>
    <tr>
      <td>SO</td>      <td>960 bits (128 bytes)</td>      <td>SO0-SO959</td>      <td>SOB0 ~ SOB119</td>      <td>SOW0 ~ SOW118</td>
    </tr>
    <tr>
      <td>X</td>      <td>9600 bits (1280 bytes)</td>      <td>FB0.X0-FB9.X959</td>      <td>FB0.XB0 ~ FB9.XB119</td>      <td>FB0.XW0 ~ FB9.XW118</td>
      </tr>      
    <tr>
      <td>Y</td>      <td>9600 bits (1280 bytes)</td>      <td>FB0.Y0-FB9.Y959</td>      <td>FB0.YB0 ~ FB9.YB119</td>      <td>FB0.YW0 ~ FB9.YW118</td>
    </tr>
    <tr>
      <td>M</td>      <td>160000 bits (20000 bytes)</td>      <td>M0-M159999</td>      <td>MB0-MB19999</td>      <td>MW0 ~ MW19998</td>
    </tr>
    <tr>
      <td>S</td>      <td>160000 bits (20000 bytes)</td>      <td>S0-S159999</td>      <td>SB0-SB19999</td>      <td>SW0 ~ SW19998</td>
    </tr>
    <tr>
      <td>R</td>      <td>960 bits (128 bytes)</td>      <td>R0-R959</td>      <td>RB0 ~ RB119</td>      <td>RW0 ~ RW118</td>
    </tr>
    <tr>
      <td>K</td>      <td>960 bits (128 bytes)</td>      <td>K0-K959</td>      <td>KB0 ~ KB119</td>      <td>KW0 ~ KW118</td>
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
There are five different types, as shown below.

  * No designation: bit, 1 bit
  * B: signed-byte, 8 bits
  * W: signed-word, 16 bits
  * L: signed-long, 32 bits
  * F: floating-point real, 32 bits

  <br>
  They are just different data types representing the same memory space of 960 bit rather than separate memory spaces. For example, DO[0-15], DOB[0-1], and DOW[0] are all the same output signals.

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
    <td>DO0-DO7</td>
    <td>DO8-DO15</td>
    <td>DO16-DO23</td>
    <td>DO24-DO31</td>
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

<div class="page-break"></div>

### signal-index

 This is a 0-based index within the relay type. The index will be given in bit units for DO and in byte units for DOB, DOW, DOL, and DOF.

<br>
<br>

The fieldbus object name can be partially skipped, as shown below. For example, DO961 is the same designation as FB1.DO1.

| **Object name** | **DO designation** | **FB.DO designation** |
| :--- | :--- | :--- |
| FB0 | DO0-DO959 | FB0.DO0-FB0.DO959 |
| FB1 | DO960-DO1919 | FB1.DO0-FB1.DO959 |
| FB2 | DO1920-DO2879 | FB2.DO0-FB2.DO959 |
| FB3 | DO2880-DO3839 | FB3.DO0-FB3.DO959 |
| FB4 | DO3840-DO4799 | FB4.DO0-FB4.DO959 |
| FB5 | DO4800-DO5759 | FB5.DO0-FB5.DO959 |
| FB6 | DO5760-DO6719 | FB6.DO0-FB6.DO959 |
| FB7 | DO6720-DO7679 | FB7.DO0-FB7.DO959 |
| FB8 | DO7680-DO8639 | FB8.DO0-FB8.DO959 |
| FB9 | DO8640-DO9599 | FB9.DO0-FB9.DO959 |


DI and DO are logical inputs and outputs, respectively, and can be accessed through the robot language and I/O assignment.