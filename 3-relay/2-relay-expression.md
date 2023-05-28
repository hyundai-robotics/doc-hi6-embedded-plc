# 3.2 Designating a relay

The following shows how the relays are designated in the embedded programmable logic controller (PLC) of the Hi6 robot controller.

`[FB{block-index}.]{relay-type}[{data-type}]{signal-index}`

For example, relays can be designated as below.

Y1501
FB3.DIW21

* block-index  
Input and output relays (DI, DO, X, Y) are grouped into 10 fieldbus blocks with their object names ranging from FB0 to FB9. For physical inputs and outputs, each block will be mapped to each fieldbus device.
The size of one fieldbus block is 120 bytes (=960 bits) for the input and output, respectively.

  You can also map some areas of FB to object names from FN0 to FN63.
  See the link below for instructions on how to set up the FN region.

  [Operation manual: 7.3.2.12 fn block allocation](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/english-tp630/7-setting/3-control-parameter/2-io-signal-setting/12-fn-block)


* relay-type  
There are 10 different types, as shown below.
Each will be explained in detail later.

  1) Digital Input (DI): This is a logical input signal that can be used in HRScript or for assigning various inputs.

  2) Digital Output (DO): This is a logical output signal that can be used in HRScript or for assigning various outputs.

  3) System Input (SI): This is a dedicated input signal that interfaces with the company’s system board.

  4) System Output (SO): This is a dedicated output signal that interfaces with the company’s system board.

  5) X: This is a physical input signal that is inputted from the outside of the controller via a fieldbus device.

  6) Y: This is a physical output signal that is outputted to the outside of the controller via a fieldbus device. 

  7) Memory (M): This can be used for storing data and can be accessed from HRScript.

  8) System (S): This is used to read or write system values in the controller. Refer to [3.4 S relay](./4-sw-relay/README.md).

  9) AuxiliaRy (R): This is an auxiliary relay for temporarily storing the Obsolete. value and is provided for the convenience of porting the Hi5a ladder file. It is recommended to use the M relay in new ladder files.

  10) Keep (K): This is an auxiliary relay for temporarily storing the Obsolete. value. The value will be stored even when the power is turned off. This is provided for the convenience of porting the Hi5a ladder file. It is recommended to use the M relay in new ladder files.


    | ** Relay name** | ** Number of points ** | ** Relay (bit) ** |** Relay (byte) ** |
    | :--- | :--- | :--- | :--- |
    | DI | 9600 bits (1280 bytes) | FB0.DI0–FB9.DI959 | FB0.DIB0–FB9.DIB127 |
    | DO | 9600 bits (1280 bytes) | FB0.DO0–FB9.DO959 | FB0.DOB0–FB9.DOB127 |
    | SI | 960 bits (128 bytes) | SI0–SI959 | SIB0–SIB127 |
    | SO | 960 bits (128 bytes) | SO0–SO959 | SOB0–SOB127 |
    | X | 9600 bits (1280 bytes) | FB0.X0–FB9.X959 | FB0.XB0–FB9.XB127 |
    | Y | 9600 bits (1280 bytes) | FB0.Y0–FB9.Y959 | FB0.YB0–FB9.YB127 |
    | M | 160000 bits (20000 bytes) | M0–M159999 | MB0–MB19999 |
    | S | 160000 bits (20000 bytes) | S0–S159999 | SB0–SB19999 |
    | R | 960 bits (128 bytes) | R0–R959 | RB0–RB127 |
    | K | 960 bits (128 bytes) | K0–K959 | KB0–KB127 |

* data-type  
There are five different types, as shown below.

  * No designation: bit, 1 bit
  * B: signed-byte, 8 bits
  * W: signed-word, 16 bits
  * L: signed-long, 32 bits
  * F: floating-point real, 32 bits

  <br>
  They are just different data types representing the same memory space of 960 bit rather than separate memory spaces. For example, DO[0–15], DOB[0–1], and DOW[0] are all the same output signals.

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
    <td>DO0–DO7</td>
    <td>DO8–DO15</td>
    <td>DO16–DO23</td>
    <td>DO24–DO31</td>
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

 This is a 0-based index within the relay type. The index will be given in bit units for DO and in byte units for DOB, DOW, DOL, and DOF.

<br>
<br>

The fieldbus object name can be partially skipped, as shown below. For example, DO961 is the same designation as FB1.DO1.

| **Object name** | **DO designation** | **FB.DO designation** |
| :--- | :--- | :--- |
| FB0 | DO0–DO959 | FB0.DO0–FB0.DO959 |
| FB1 | DO960–DO1919 | FB1.DO0–FB1.DO959 |
| FB2 | DO1920–DO2879 | FB2.DO0–FB2.DO959 |
| FB3 | DO2880–DO3839 | FB3.DO0–FB3.DO959 |
| FB4 | DO3840–DO4799 | FB4.DO0–FB4.DO959 |
| FB5 | DO4800–DO5759 | FB5.DO0–FB5.DO959 |
| FB6 | DO5760–DO6719 | FB6.DO0–FB6.DO959 |
| FB7 | DO6720–DO7679 | FB7.DO0–FB7.DO959 |
| FB8 | DO7680–DO8639 | FB8.DO0–FB8.DO959 |
| FB9 | DO8640–DO9599 | FB9.DO0–FB9.DO959 |


DI and DO are logical inputs and outputs, respectively, and can be accessed through the robot language and I/O assignment.