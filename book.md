# Hi6 Robot Controller Function Manual - Embedded Progammable Logic Controller (PLC)

{% hint style="warning" %}
The information provided in this product manual is the property of Hyundai Robotics.

It cannot be reproduced or redistributed in part or whole without written consent from Hyundai Robotics, and it cannot be provided to third parties or used for other purposes.



The manual is subject to change without prior notification.



**Copyright ⓒ 2022 by Hyundai Robotics**
{% endhint %}
# 1. Overview

The embedded programmable logic controller (PLC) of the Hi6 controller refers to the functions of the PLC that are installed into the controller in a software-like manner. The user can write and operate ladder programs that are commonly used in PLCs.


Ladder programs can be written or edited using the HRLadder, a ladder editing PC software dedicated to the robots of Hyundai Robotics, and downloaded to the Hi6 controller connected via Ethernet. Conversely, the ladder program running on the Hi6 controller can be uploaded to the HRLadder on the PC, and the status, such as the mode of the PLC running on the controller or the values of relays, can be remotely monitored from the HRLadder. 

* You can download the HRLadder from the Hyundai Robotics website (https://www.hyundai-robotics.com) - Customer Support - Application Software screen.
* For the information on how to use the HRLadder, refer to the function manual linked to the Help menu of the HRLadder.
* HRLadder can be used for old controller models ranging from Hi4 to Hi5a. Please note that as the ladder program of the Hi6 controller is different from that of the old model controllers, there is no compatibility between them.


The Hi6 controller’s I/O can be connected to the upper-process PLCs with fieldbus masters or to the devices of lower-level fieldbus slaves, both through a fieldbus or remote I/O device. The functions of the embedded PLC are designed to control the signals of the thus connected I/O using ladder logic.


The functions of the Hi6 controller’s embedded PLC are similar to those of the Hi5a controller’s embedded PLC, and the same HRLadder, in other words, the same ladder editor, is used. Therefore, users who are already familiar with the functions of the Hi5a controller’s embedded PLC can quickly learn from this manual by checking only the different parts of the Hi6 controller.


{% hint style="info" %}
Therefore, users already familiar with the functions of the Hi5a controller’s embedded PLC can quickly learn from this manual by checking only the different parts of the Hi6 controller. You are kindly required to check the link shown below.
[5. Difference in the embedded PLC between Hi5a and Hi6 controllers](../5-diff-hi5a-hi6.md)

{% endhint %}

# 1.1 Ladder logic

Ladder Logic, or Ladder Diagram (LD), is the main programming method for embedded PLCs. [Besides LD, there are other methods such as Structured Text (ST), Function Block Diagram (FBD), and Sequential Function Chart (SFC), but embedded PLCs do not support them and will not be further discussed.]

The reason the ladder program is so named is that the architecture of the program resembles a ladder. The horizontal connection line through which signals flow in a ladder-like structure is called a rung, which includes multiple instructions.

![](../_assets/ladder-sample2.png)


A robot teaching project can include one or multiple ladder diagrams, and each diagram may consist of tens to hundreds of rungs.
When the programmable logic controller (PLC) is switched to RUN mode, LD will be executed repeatedly. The time taken to complete one cycle is called scan time and usually ranges from a few milliseconds to several tens of milliseconds.


<br>

An instruction consists of a mnemonic, which is the name of the instruction, and an operand, which is the argument to be transferred to the instruction.

  For example, the ADD (+) instruction in the figure below is configured as follows.

![](../_assets/ladder-add.png)

* Mnemonic: ADD
* Operand1: MW5
* Operand2: DOW2
* Operand3: MW6

<br>

Instructions of an embedded PLC can be classified into multiple instruction groups, as described below. As every instruction will be explained in Section 4, the instructions in this section will be explained as examples for understanding the concept of ladder logic.

---

<br>

## Contact instruction

Classified as a contact instruction, eXamine If Closed (XIC) is a simple instruction with only one operand. This instruction will be indicated on the rung with an operand marked on the -| |- symbol.

![](../_assets/ladder-xic.png)

A contact is a switch determining whether to transfer the signal (1) applied to the left along the rung to the right. If the relay DO3’s value is 0 (inactive), the contact will be open, keeping the signal from being transferred. If the DO3’s value is 1 (active), the contact will be closed, allowing the signal to be transferred.

![](../_assets/ladder-contact.png)

<br>

When several XIC contacts are connected in series or parallel in the form of a branch, logical operational expressions such as AND, OR, and NOT can be created.
(![](../_assets/ladder-not.png) shows an Inverting (INV) instruction that is designed to transfer the opposite value of the logical value on the left to the right and has no operand.)

```
X1 AND (X2 OR (NOT X3))
```

![](../_assets/ladder-and-or-not.png)

<br>


## Output-coil instruction

OuTput Energize (OTE) is classified as an output coil instruction. It is always placed at the rightmost end of the rung and indicated by the -( )- symbol. This instruction allows the value transferred from the left to be outputted to the operand relay.

If the result of the logical operation expression described above is outputted to the Y8 relay, it will be in the form shown below.

```
Y8 = X1 AND (X2 OR (NOT X3))
```

![](../_assets/ladder-ote.png)


<br>

## Function instruction

When the left side becomes active, a specific operation for the given operand will be executed. For example, in the diagram below, when DO3 becomes active, the arithmetic operation ADD (+) of adding the values of MW5 and DOW2 relays and then substituting the thus acquired sum into the MW6 relay will be executed.

```
IF DO3:
   MW6 = MW5 + DOW2
```

![](../_assets/ladder-add2.png)

The compare instruction also transfers the operation result to the right side. For example, in the diagram below, if DO6 becomes active and MW8 exceeds 120, Y20 will be activated.

```
Y20 = DO6 AND (MW8 > 120)
```


![](../_assets/ladder-grt.png)
# 2. Setting up the controller

# 2.1. Setting the embedded PLC’s mode

In “[F7: Condition setting] – PLC’s operation mode”, you can select one of the Off, Stop, R-Stop, R-Run, or Run modes as the operation mode of the embedded progammable logic controller (PLC.) 
R-Stop and R-Run refer to Remote-Stop and Remote-Run, respectively, and each represents a state in which the mode can be changed remotely from the HRLadder of the PC connected via Ethernet.

![Figure 2.1 Setting the embedded PLC’s mode](../_assets/plc_run_mode.png)

<br>
<br>
According to the selected mode, the state will be indicated with an icon at the top right of the teach pendant’s screen. That is, in the case of PLC=R-Run or PLC=Run, the PLC icon will be displayed, as shown in the figure above; in the case of PLC=Off, the PLC icon will disappear, as shown in the figure below; and in the case of PLC=Stop, a prohibition mark in red will be indicated on the PLC icon.

![Figure 2.2 Embedded PLC in Off State](../_assets/plc_mode_off.png)

 
![Figure 2.3 Embedded PLC in Stop State](../_assets/plc_mode_stop.png)


* Off  
The functions of the embedded PLC will be turned off. When this occurs, the logical outputs of the robot controller, FB0.DO0–FB9.DO959, will be automatically outputted as the physical outputs (means bypassing), FB0.Y0–FB9.Y959, and the physical inputs, FB0.X0–FB9.X959, will be automatically inputted as logical inputs, FB0.DI0–FB9.DI595.

* R-Stop/Stop  
The operation of the embedded PLC will be stopped. R-Stop represents a remote state in which a change can be made from the HRLadder. If the Stop mode is set, it will be impossible to change the operation mode from the HRLadder. 
When the embedded PLC is stopped, the DI and Y relays, which are PLC output signals, will become 0 automatically. *(DI is an input from the perspective of robot language or assignment, but it is an output from the perspective of the embedded PLC.)*  

* R-Run/Run  
The embedded PLC will be executed. R-Run represents a remote state in which changes can be made from the HRLadder. If the Run mode is set, it will be impossible to change the operation mode from the HRLadder. 
# 2.2. Monitoring the relay state from the teach pendant of the controller

The relay state can be monitored by entering “[R2: Window adjustment] - [F1: Selection]”.

For more details, refer to [Hi6 Operation Manual - 6. Monitoring](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/6-monitoring/README).# 2.3. Scan time

The time taken for the one-cycle execution of the ladder file in the embedded PLC will be indicated as “scan time” on the status bar at the bottom of the HRLadder. As the number of steps in the ladder program increases, the time for execution increases, slowing down the I/O responsiveness accordingly.# 3. Relays

# 3.1 The meaning of a relay

A device in a state equivalent to an on/off contact that determines whether to transfer an electrical signal is called a switch. Meanwhile, a relay is a switch that can operate automatically by using electricity rather than manually.  

Originally, a relay was a physical device that controls contacts using the magnetic force of a coil. However, a relay in a computerized programmable logic controller (PLC) is a logical concept that is controlled by software. In terms of the meaning, a relay has been used as a variable that can store not only an on/off state consisting of 1 bit but also a byte, word, double word, or real value consisting of several bits.# 3.2 Designating a relay

The following shows how the relays are designated in the embedded programmable logic controller (PLC) of the Hi6 robot controller.

[FB{block-index}.]{relay-type}[{data-type}]{signal-index}

For example, relays can be designated as below.

Y1501
FB3.DIW21

* block-index  
Input and output relays are grouped into 10 fieldbus blocks with their object names ranging from FB0 to FB9. For physical inputs and outputs, each block will be mapped to each fieldbus device.
The size of one fieldbus block is 120 bytes (=960 bits) for the input and output, respectively.

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


DI and DO are logical inputs and outputs, respectively, and can be accessed through the robot language and I/O assignment.# 3.3 Input/output diagram

The I/O diagram of the Hi6 robot controller is as shown below.


![](../_assets/io-diagram.png)

Figure 3.1 I/O diagram

<br><br>

The light green boxes on the right side of the figure are hardware modules inside the Hi6 controller. On the left, there is the main module (COM module) where the main software runs. Meanwhile, on the right, there are Hilscher communication interface (CIF) cards, which are peripheral component interconnect (PCI) cards for the connection to the fieldbus, and serial or Ethernet devices for the connection to the Modbus.

In the main software, there are various relays drawn in the form of small boxes. In the Hi6 controller, there are software elements that access these relays, and they are HRScript (robot language), I/O assignment, and the embedded programmable logic controller (PLC). 

<br>

## HRScript (robot language)
The robot language can access User I/O (FB.DI/DO) relays and Memory (M) relays through I/O variables. However, lowercase letters are to be used instead of uppercase letters (e.g., fb3.dow14, mw501.). For details on input/output variables, refer to the [Hi6 Function Manual - Robot Language - I/O Variables](https://hrbook-hrc.web.app/#/view/doc-hrscript/korean/6-external-comm/1-fb-io/1-io-val) section.


<br>

## I/O assignment, I/O attributes
I/O assignment can access FB.DI/DO relays. In addition, negative logic, pulse, etc. can be set in FB.DI/DO by setting the I/O attributes. For example, for the “external stop,” which is an input assignment, if negative logic is set in DI24, the robot will stop when the DI24 signal is 0 (active).
For more details, refer to the [Hi6 Operation Manual - Input/Output Signal Setting](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/7-setting/3-control-parameter/2-io-signal-setting/README) section. 


<br>

## Embedded PLC
Ladder Logic is drawn in a dotted line inside the embedded PLC box, and this part is connected to the relays on both sides with arrows. Ladder Logic receives inputs from relays, executes arithmetic/logical operations intended by the author, and then transfers the result values ​​to other relays.  

As Ladder Logic is connected to Memory, System, Timer, and Counter relays in both directions, it can read values from the relays and write values to them. On the other hand, it is possible only to write values to FB.Y, a physical output, and only to read values from FB.X, a physical input. 

FB.DI is an input from the point of view of the robot language, but this input is a logical input coming inside the controller through the embedded PLC. In other words, from the point of view of the embedded PLC, it is an output. Therefore, Ladder Logic can only write to it. Likewise, as FB.DO is an input from the point of view of the embedded PLC, Ladder Logic can only read from it.

<br>

## Connection to external communication
Hilscher CIF cards are to be connected to physical inputs and outputs. For how to map one or multiple fieldbus objects to a specific CIF card, refer to [Hi6 Operation Manual - I/O Signal Setting - DIO Block Assignment](https://hrbook-hrc.web.app/#/view/doc-hi6-operation/korean-tp630/7-setting/3-control-parameter/2-io-signal-setting/9-dio-block-assign).  

All relays are mapped to the address space of the Modbus slave function. For more details, refer to [Hi6 Function Manual - Modbus](https://hrbook-hrc.web.app/#/view/doc-modbus/korean/README).
# 3.4 S relays

The values ​​for various states in the Hi6 controller are mapped to the S relays. It is also possible to change the state of Hi6 by writing values ​​to some of the S relays.

Therefore, an external device, such as a process programmable logic controller (PLC) or personal computer (PC), can remotely monitor the states of the Hi6 controller by reading the values of the S relays through fieldbus, Modbus, etc. and can remotely control the Hi6 controller by writing values to the S relays.  

The area of the S relays can be largely divided into two parts as follows.


<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
	<tr>
		<th>address</th>
		<th>content</th>
	</tr>
	<tr>
		<td>SB00000–SB01999</td>
		<td>fixed area</td>
	</tr>
	<tr>
		<td>SB02000–SB19999</td>
		<td>optional items area (slots)</td>
	</tr>
</table>

<br>

### Fixed area
Basic items that are frequently used are allocated to predetermined addresses. It is not possible to change or allocate items through settings. The map of the fixed area will be described in the next section.

<br>

### Optional items area
This area consists of a total of 900 slots, with each slot of 20 bytes. The configuration of each slot will be determined by what command value is to be put into the leading word. The map for each command is described in the following section.

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
		<td>command (conventional practice: get is for even numbers, set is for odd numbers)</td>
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
</table># 3.4.1 S relay - Fixed area

Please refer to the table shown below for the SB0–SB1999 areas for which fixed items are provided.

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.bit { width: 10%; }
</style>

### Area for special flags

<table class="tg">
<thead>
	<tr>
		<th class='bit'>Relay</th>
		<th class='bit'>bit7</th>
		<th class='bit'>bit6</th>
		<th class='bit'>bit5</th>
		<th class='bit'>bit4</th>
		<th class='bit'>bit3</th>
		<th class='bit'>bit2</th>
		<th class='bit'>bit1</th>
		<th class='bit'>bit0</th>		
		<th class='bit'>Remark</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>SB0</td>
		<td>On if carry occurs in the operation</td>
		<td>On if BCD operation is impossible</td>
		<td>1-sec clock</td>
		<td>0.2-sec clock</td>
		<td>0.1-sec clock</td>
		<td>On only for one scan</td>
		<td>Always off</td>
		<td>Always on</td>		
		<td></td>
	</tr>
	<tr>
		<td>SB1</td>
		<td class='grayed'></td>
		<td>On when the label is 0 or below or when there is no label to jump to</td>
		<td>On if the label is duplicated</td>
		<td>On if there are more than 100 labels</td>
		<td>On if the label is not a constant</td>
		<td>Y relay direct output allowable if on</td>
		<td>4-sec clock</td>
		<td>2-sec clock</td>
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
		<td>On if there is no subladder to be called by Call</td>
		<td>On when the scan time exceeds 5 seconds</td>
		<td></td>
	</tr>
</tbody>
</table>

<br>

### Area for basic information

<table class="tg">
<thead>
	<tr>
		<th>Relay</th>
		<th>Description</th>
		<th>Remark</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td>SB4</th>
		<td>PLC execution mode<br>
		(0=stop, 1=R.stop, 2=R.run, 3= run, 4=off, 5=no program)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW6</td>
		<td>Date/Time: Year</td>
	</tr>
	<tr>
		<td>SB8</td>
		<td>Date/Time: Month</td>
		<td></td>
	</tr>
	<tr>
		<td>SB9</td>
		<td>Date/Time: Date</td>
		<td></td>
	</tr>	
	<tr>
		<td>SB10</td>
		<td>Date/Time: Hour</td>
		<td></td>
	</tr>	
	<tr>
		<td>SB11</td>
		<td>Date/Time: Minute</td>
		<td></td>
	</tr>	
	<tr>
		<td>SB12</td>
		<td>Date/Time: Second</td>
		<td></td>
	</tr>	
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB14</td>
		<td>Software version: First<br>
		e.g., In the case of V60.05-08, SB14:60, SB15:5, SB16:8</td>
		<td></td>
	</tr>
	<tr>
		<td>SB15</td>
		<td>Software version: Second</td>
		<td></td>
	</tr>
	<tr>
		<td>SB16</td>
		<td>Software version: Small-fix</td>
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
		<td>Assignment time</td>
		<td>us</td>
	</tr>
	<tr>
		<td>SW22</td>
		<td>Maximum occupancy time</td>
		<td>ms</td>
	</tr>
	<tr>
		<td>SW24</td>
		<td>Average occupancy time</td>
		<td>ms</td>
	</tr>
	<tr>
		<td>SW26</td>
		<td>Total number of the steps in the Ladder</td>
		<td></td>
	</tr>
	<tr>
		<td>SW28</td>
		<td>Occupancy ratio</td>
		<td>%</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB40</td>
		<td>Current tool number</td>
		<td></td>
	</tr>
	<tr>
		<td>SB41</td>
		<td>Robot state (0=stop, 1=run, 2=wait)</td>
		<td></td>
	</tr>
	<tr>
		<td>SB42</td>
		<td>Playback speed</td>
		<td>%</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW44</td>
		<td>Manual speed</td>
		<td>mm/s</td>
	</tr>
	<tr>
		<td>SW46</td>
		<td>Tool tip movement speed</td>
		<td>mm/s</td>
	</tr>
	<tr>
		<td>SW48</td>
		<td>Error/warning number</td>
		<td></td>
	</tr>
	<tr>
		<td>SW50</td>
		<td>Error/warning auxiliary information</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW60</td>
		<td>Indirect address designation 1</td>
		<td></td>
	</tr>
	<tr>
		<td>SW62</td>
		<td>Indirect address designation 2</td>
		<td></td>
	</tr>
	<tr>
		<td>SW64</td>
		<td>Indirect address designation 3</td>
		<td></td>
	</tr>
	<tr>
		<td>SW66</td>
		<td>Indirect address designation 4</td>
		<td></td>
	</tr>
	<tr>
		<td>SW68</td>
		<td>Indirect address designation 5</td>
		<td></td>
	</tr>
	<tr>
		<td>SW70</td>
		<td>Indirect address designation 6</td>
		<td></td>
	</tr>
	<tr>
		<td>SW72</td>
		<td>Indirect address designation 7</td>
		<td></td>
	</tr>
	<tr>
		<td>SW74</td>
		<td>Indirect address designation 8</td>
		<td></td>
	</tr>
	<tr>
		<td>SW76</td>
		<td>Indirect address designation 9</td>
		<td></td>
	</tr>
	<tr>
		<td>SW78</td>
		<td>Indirect address designation 10</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB88</br>
		...</br>
		SB99</td>
		<td>Teach pendant key input state</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW100</td>
		<td>Main program number</td>
		<td>Main task</td>
	</tr>
	<tr>
		<td>SW102</td>
		<td>Step number</td>
		<td>Main task</td>
	</tr>
	<tr>
		<td>SW104</td>
		<td>Function number</td>
		<td>Main task</td>
	</tr>
	<tr>
		<td>SW106</td>
		<td>Main program number</td>
		<td>Main task</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB109</td>
		<td>Run time selection<br>
		(1=Total (after initialization), 2=Total (after power input), 3=Last cycle, 4=Current cycle)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL110</td>
		<td>Motor on (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL114</td>
		<td>Motor on (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL118</td>
		<td>Run time (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL122</td>
		<td>Run time (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL126</td>
		<td>Movement time (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL130</td>
		<td>Movement time (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL134</td>
		<td>Cycle count</td>
		<td></td>
	</tr>
	<tr>
		<td>SL138</td>
		<td>wait, di wait time (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL142</td>
		<td>wait, di wait time (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL146</td>
		<td>delay wait time (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL150</td>
		<td>delay wait time (ms)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB159</td>
		<td>Axis information selection<br>
		(1=Current position (axis angle), 2=Current position (base coordinate), 6=Axis speed, 7=Motor speed<br>
		 10=Load factor(I/Ir), 11=Load factor(I/Ip), 13=Load factor(continuous), 15=Encoder temperature<br>
		 18=Accumulated distance for each axis)</td>
		<td></td>
	</tr>
	<tr>
		<td>SF160</td>
		<td>Relevant value for Axis 1</td>
		<td></td>
	</tr>
	<tr>
		<td>SF164</td>
		<td>Relevant value for Axis 2</td>
		<td></td>
	</tr>
	<tr>
		<td>SF168</td>
		<td>Relevant value for Axis 3</td>
		<td></td>
	</tr>
	<tr>
		<td>SF172</td>
		<td>Relevant value for Axis 4</td>
		<td></td>
	</tr>
	<tr>
		<td>SF176</td>
		<td>Relevant value for Axis 5</td>
		<td></td>
	</tr>
	<tr>
		<td>SF180</td>
		<td>Relevant value for Axis 6</td>
		<td></td>
	</tr>
	<tr>
		<td>SF184</td>
		<td>Relevant value for Axis 7</td>
		<td></td>
	</tr>
	<tr>
		<td>SF188</td>
		<td>Relevant value for Axis 8</td>
		<td></td>
	</tr>
	<tr>
		<td>SF192</td>
		<td>Relevant value for Axis 9</td>
		<td></td>
	</tr>
	<tr>
		<td>SF196</td>
		<td>Relevant value for Axis 10</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
</tbody>
</table># 3.4.2 S relay - TASK_INFO

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
		<td>GET_TASK_INFO (100)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>task_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=5>result</td>
		<td>task in activated state</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>task program number</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>task step number</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>task function number</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>task main program number</td>
		<td>s2</td>
	</tr>	
</tbody>
</table># 3.4.3 S relay - OP_TIME

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
		<td>GET_OP_TIME (110)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>task_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
		<td>time_base<br>1=since_init, 2=since power ON, 3=since last cycle, 4=current cycle</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>param. 3</td>
		<td>item<br>1=motor ON, 2=run_time, 3=moving time, 4=wait time, 5=delay time, 11=spotweld time (welder 1), 12=(welder 2), 13=(welder 3), 14=(welder 4)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>result</td>
		<td>day</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>msec</td>
		<td>s4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>cycle count / weld count</td>
		<td>s4</td>
	</tr>
</tbody>
</table># 3.4.4 S relay - AXIS_INFO

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
		<td>GET_AXIS_INFO (120)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param. 1</td>
		<td>type<br>1 = current position (axis angle), 2 = current position (base coordinate), 6 = axis speed,
7 = motor speed, 10 = load factor (I/Ir), 11 = load factor (I/Ip), 12 = load factor (continuous),
15 = encoder (temperature), 18 = accumulated distance for each axis</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param. 2</td>
		<td>start axis number (1–)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>-</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>8</td>
		<td rowspan=3>result</td>
		<td>relevant value (for the start axis + axis 0)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>relevant value (for the start axis + axis 1)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>16</td>
		<td>relevant value (for the start axis + axis 2)</td>
		<td>f4</td>
	</tr>
</tbody>
</table># 3.4.5 S relay - TP_KEYPAD

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
		<td>GET_TP_KEYPAD (130)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>-</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
	</tr>
	<tr>
		<td>3</td>
		<td>[0]</td>
		<td rowspan=12>keypad[0–11]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>[1]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>5</td>
		<td>[2]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>6</td>
		<td>[3]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>7</td>
		<td>[4]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>8</td>
		<td>[5]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>9</td>
		<td>[6]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>10</td>
		<td>[7]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>11</td>
		<td>[8]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>12</td>
		<td>[9]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>13</td>
		<td>[10]</td>
		<td>u1</td>
	</tr>
	<tr>
		<td>14</td>
		<td>[11]</td>
		<td>u1</td>
	</tr>
</tbody>
</table># 3.4.6 S relay - TP_APP

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
		<td>GETSET_TP_APP (140)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>get</td>
		<td>the shortcut key number for the teach pendant’s current app (1–9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>set</td>
		<td>the shortcut key number for the teach pendant’s target app whose state needs to be read or controlled (1–9)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>get</td>
		<td>the current state value of the teach pendant’s target app<br>(-1=no operation, 0=not executed, 1=activated, 2=inactivated)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>set</td>
		<td>controlling of the teach pendant’s target app<br>
(0: no operation, 1: activated, 2: inactivated, 8: executed, 9:forced ending)<br>
* will be performed once every time the value changes.</td>
		<td>s2</td>
	</tr>
</tbody>
</table># 3.4.7 S relay - DATE_TIME

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
		<td>GET_DATE_TIME (150)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td rowspan=6>result</td>
		<td>year (e.g., 2022)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>month (1–12)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>date (1–31)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>hour (0–23)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>minute (0–59)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>second (0–59)</td>
		<td>s2</td>
	</tr>
</tbody>
</table># 3.4.8 S relay - CUR_SPOTGUN_NO

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
		<td>GET_CUR_SPOTGUN_NO (2000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>task_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=4>result</td>
		<td>current spot gun number (welder #1, master gun)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>current spot gun number (welder #2, slave gun #1)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>current spot gun number (welder #3, slave gun #2)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>current spot gun number (welder #4, slave gun #3)</td>
		<td>s2</td>
	</tr>
</tbody>
</table># 3.4.9 S realy - SPOTWELD_INFO

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
		<td>GET_SPOTWELD_INFO (2010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>task_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td>param 2</td>
		<td>gun_no (1–4)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td rowspan=5>result</td>
		<td>gun search state (1=complete, 0=incomplete)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>moving electrode consumption amount × 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>fixed electrode consumption amount × 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>squeeze force instruction value × 10</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>squeeze force current value × 10</td>
		<td>s2</td>
	</tr>
</tbody>
</table># 3.4.10 S relay - CONVEYOR_INFO

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
		<td>GET_CONVEYOR_INFO (4000)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=7>result</td>
		<td>conveyor pulse</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>6</td>
		<td>workpiece position</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>8</td>
		<td>conveyor speed</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>10</td>
		<td>workpiece count</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>12</td>
		<td>limit switch input</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>raw pulse</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>14</td>
		<td>encoder resolution</td>
		<td>s4</td>
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
		<td>GET_CONVEYOR_INFO_LIN (4010)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>result</td>
		<td>linear conveyor horizontal angle</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>linear conveyor vertical angle</td>
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
		<td>GET_CONVEYOR_INFO_CIR (4020)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=2>result</td>
		<td>circular conveyor angle (X axis)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>circular conveyor angle (Y axis)</td>
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
		<td>GET_CONVEYOR_INFO_CIR2 (4040)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>2</td>
		<td>param 1</td>
		<td>conv_no (0–7)</td>
		<td>s2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=3>result</td>
		<td>circular conveyor center (X)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>8</td>
		<td>circular conveyor center (Y)</td>
		<td>f4</td>
	</tr>
	<tr>
		<td>12</td>
		<td>circular conveyor center (Z)</td>
		<td>f4</td>
	</tr>
</tbody>
</table>
# 3.5 Designating indirect addresses for relays

SW62–SW79 are system memories for designating indirect addresses. Regardless of the relay type, if a value between -2 and -18 is designated for a relay address, the set value will lead to a designated relay address stored in SW62–SW79.



![](../_assets/rel-addr-concept.png)

For example, when some of the values for SW62–SW79 are as below,

| **relay** | **value** |
| :---      | :---      |
| SW62      | 12        |
| SW70      | 3         |
| SW78      | 56        |

the notation of an indirect address can be interpreted as follows.

*	MW-2 -> MW12
*	FB-10.X3 -> FB3.X3
*	X-18 -> X56
*	FB-10.YW-2 -> FB3.YW12

The embedded programmable logic controller (PLC) example presented below is an example in which the operation of outputting signals Y1–Y128 corresponding to input signals X1–X128 is created using the FOR/NEXT instructions and indirect address designation method.

![](../_assets/rel-addr-for-next.png)# 4. Instructions


A ladder program consists of multiple rungs, and each rung consists of multiple instructions.

The embedded PLC performs logical I/O operations while sequentially executing instructions in the program.

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table>
<thead>
  <tr>
    <td rowspan="11">ladder project</td>
    <td rowspan="7">ladder program</td>
    <td rowspan="3">rung</td>
    <td>instruction</td>
  </tr>
  <tr>
    <td>instruction</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">rung</td>
    <td>instruction</td>
  </tr>
  <tr>
    <td>instruction</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td>...</td>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">ladder program</td>
    <td rowspan="2">rung</td>
    <td>instruction</td>
  </tr>
  <tr>
    <td>instruction</td>
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
</thead>
</table>

<br><br>


An instruction consists of three elements, as shown below.

<table>
<thead>
  <tr>
    <th>instruction (mnemonic)</th>
    <th>type of operation</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>operand</td>
    <td>Argument of an operation.<br>Depending on the instruction, one or multiple operands can be designated, but some instructions do not have operands.</td>
  </tr>
  <tr>
    <td>comments</td>
    <td>Description attached for the readability of a program. Comments do not affect operations.</td>
  </tr>
</tbody>
</table>


# 4.1 List of Instructions


<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

### * Rung and branch
<br>

<table>
<thead>
  <tr>
    <th>Mnemonic</th>
    <th>Name</th>
    <th>Symbol</th>
    <th>Description</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>RUNG</td>
    <td>Rung</td>
    <td>├─┤</td>
    <td>rung</td>
  </tr>
  <tr>
    <td>BST</td>
    <td>Branch Start</td>
    <td>┬─</td>
    <td>start of a branch</td>
  </tr>
  <tr>
    <td>BND</td>
    <td>Branch End</td>
    <td>─┬</td>
    <td>end of a branch</td>
  </tr>
  <tr>
    <td>NXB</td>
    <td>Nested Branch</td>
    <td>└,├</td>
    <td>nest of a branch</td>
  </tr>
</tbody>
</table>

<br><br>  

### * Logic examination instructions: If the examination result is true, the rung is active. If false, the rung is inactive. 
<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>XIC</td>
		<td>Examine if Closed</td>
		<td>-| |-</td>
		<td>examines if the contact is closed (contact A)</td>
	</tr>
	<tr>
		<td>XIO</td>
		<td>Examine if Open</td>
		<td>-|/|-</td>
		<td>examines if the contact is open (contact B)</td>
	</tr>
	<tr>
		<td>INV</td>
		<td>Inverting</td>
		<td>-//-</td>
		<td>inverts the result of the rung (inverting)</td>
	</tr>
	<tr>
		<td>EQU</td>
		<td>Inverting</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if equal (=)</td>
	</tr>
	<tr>
		<td>NEQ</td>
		<td>Inverting</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if not equal (<>)</td>
	</tr>
	<tr>
		<td>LES</td>
		<td>Less Than</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if less than (<)</td>
	</tr>
	<tr>
		<td>GRT</td>
		<td>Greater Than</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if greater than (>)</td>
	</tr>
	<tr>
		<td>LEQ</td>
		<td>Less Than or Equal</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if less than or equal (<=)</td>
	</tr>
	<tr>
		<td>GEQ</td>
		<td>Greater Than or Equal</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>examines if greater than or equal (>=)</td>
	</tr>
</tbody>
</table>

<br><br>  

### * Output instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>OTE</td>
		<td>Output Energize</td>
		<td>-( )-</td>
		<td>the state of the rung (active: ON/inactive: OFF) will be outputted</td>
	</tr>
	<tr>
		<td>OTL</td>
		<td>Output Latch</td>
		<td>-(L)-</td>
		<td>if the rung is active, the output signal will be outputted in the ON (high) state</td>
	</tr>
	<tr>
		<td>OTU</td>
		<td>Output Unlatch</td>
		<td>-(U)-</td>
		<td>if the rung is active, the output signal will be outputted in the OFF (low) state</td>
	</tr>
	<tr>
		<td>OSR</td>
		<td>One Shot Rising</td>
		<td>-(OSR)-</td>
		<td>if the rung is active, the output signal will be outputed in the ON state only for the duration of one scan</td>
	</tr>
	<tr>
		<td>RES</td>
		<td>Reset</td>
		<td>-(RES)-</td>
		<td>if the rung is active, the timer or counter will be reset</td>
	</tr>
</tbody>
</table>



<br><br>  

### * Timer and counter instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TON</td>
		<td>Time ON delay</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>the timer operates only while the rung is active</td>
	</tr>
	<tr>
		<td>CTD</td>
		<td>Count Down</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>the rung's activation (inactive -> active) will be counted down</td>
	</tr>
</tbody>
</table>


<br><br>  

### * Arithmetic operation instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>ADD</td>
		<td>Add</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>addition (+) operation if the rung is active</td>
	</tr>
	<tr>
		<td>SUB</td>
		<td>Subtract</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>subtraction (-) operation if the rung is active</td>
	</tr>
	<tr>
		<td>MUL</td>
		<td>Multiply</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>multiplication (x) operation if the rung is active</td>
	</tr>
	<tr>
		<td>DIV</td>
		<td>Divide</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>division (/) operation if the rung is active</td>
	</tr>
	<tr>
		<td>POW</td>
		<td>Power</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>power (^) operation if the rung is active</td>
	</tr>
</tbody>
</table>




<br><br>  

### * Data conversion instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TOD</td>
		<td>convert an integer to BCD</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, the integer will be converted to BCD</td>
	</tr>
	<tr>
		<td>FRD</td>
		<td>convert BCD to an inetger</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, BCD will be converted to an integer</td>
	</tr>
	<tr>
		<td>SEG</td>
		<td>7-segment</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, conversion to a 7-segment value will occur</td>
	</tr>
</tbody>
</table>


<br><br>  

### * Move and Copy instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>MOV</td>
		<td>Move</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, one piece of data will be copied</td>
	</tr>
	<tr>
		<td>COP</td>
		<td>Copy data</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, multiple pieces of data will be copied</td>
	</tr>
	<tr>
		<td>CCOP</td>
		<td>Conditional copy data</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>multiple pieces of data will be copied depending on the state of the rung</td>
	</tr>
	<tr>
		<td>ROT</td>
		<td>Rotating output</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, sequential outputting will occur</td>
	</tr>
</tbody>
</table>

<br><br>  


### * Block control instructions

<br>

<table>
<thead>
	<tr>
		<th>Mnemonic</th>
		<th>Name</th>
		<th>Symbol</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>FOR</td>
		<td>FOR loop</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, execution in repetition will occur until Next</td>
	</tr>
	<tr>
		<td>NEXT</td>
		<td>NEXT loop</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>jumping to the FOR instruction will occur if the count is within the repetition count</td>
	</tr>
	<tr>
		<td>LBL</td>
		<td>LabeL</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>a position to jump to according to the JMP instruction will be designated</td>
	</tr>
	<tr>
		<td>JMP</td>
		<td>Jump</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, jumping to the LBL position will occur<br>
		(skipping to -n NEXTs if Label&lt;0)</td>
	</tr>
	<tr>
		<td>CALL</td>
		<td>Call</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, a sub-ladder will be called</td>
	</tr>
	<tr>
		<td>END</td>
		<td>End</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>if the rung is active, the sub-ladder will end</td>
	</tr>
</tbody>
</table># 4.2 XIC (Examine if Closed): Examining if Closed


### Description
If the bit value of the operand is 1, the rung will be made active. If 0, it will be made inactive.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

When the Run switch, which is the contact A of input X2, is in the pressed state (1 = active) and the internal state relay M5 is normal (1), the "Run" lamp output Y5 will be switched on. 

![](../_assets/xic.png)
# 4.3 XIO (Examine if Open): Examining if Open


### Description
If the bit value of the operand is 0, the rung will be made active. If 1, it will be made inactive.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

When the "Pause" button, which is the contact B of input X1, is in the pressed state (0 = active), the brake output Y8 will be switched on.  

![](../_assets/xio.png)
# 4.4 INV (Inverting): Inverting


### Description
Inverts (active <-> inactive) the previous result of the rung.

<br>

### Example of use

According to DeMorgand's law, processing an invert will make /(AxB) equal to /A+/B or /(A+B) equal to /Ax/B, allowing a simple configuration that uses the AND logic that has no branches instead of a configuration that uses the OR logic, which has multiple branches.
As such, the logic of the two rungs below will have the same result because (X1+X2+X3) equals to /(/X1x/X2x/X3).

![](../_assets/inv.png)
# 4.5 EQU (Equal): Examining if Equal


### Description
If two values are compared and found to be equal, the rung will be made active (contact active).

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the value of the input XB3 is equal to 100, the output Y7 will be switched on. Otherwise, it will be switched off.

![](../_assets/equ.png)
# 4.6 NEQ (Not Equal): Examining if Not Equal


### Description
If two values are compared and found to be unequal, the rung will be made active (contact active).

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

The output Y8 will switched on if the value of the input XB4 is not equal to 50. Otherwise, it will be switched off.

![](../_assets/neq.png)
# 4.7 LES (Less Than): Examining if Less Than


### Description
If the value of "source a" is less than the value of "source b," the rung will be made active (contact active).

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the value of the input XB7 is less than 70, the output Y9 will be switched on. If it is greater than or equal to 70, the output will be switched off.

![](../_assets/les.png)
# 4.8 GRT (Greater Than): Examining if Greater Than


### Description
If the value of "source a" is greater than the value of "source b," the rung will be made active (contact active).

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the value of the input XB8 is greater than 80, the output Y10 will be switched on. If it is less than or equal to 80, the output will be switched off.

![](../_assets/grt.png)
# 4.9 LEQ (Less Than or Equal): Examining if Less Than or Equal


### Description
If the value of "source a" is less than or equal to the value of "source b," the rung will be made active (contact active).

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the value of the input XB9 is less than or equal to 90, the output Y11 will be switched on. If it is greather than 90, the output will be switched off.

![](../_assets/leq.png)
# 4.10 GEQ (Greater Than or Equal): Examining if Greater Than or Equal


### Description
If the value of "source a" is greater than or equal to the value of "source b," the rung will be made active (contact active).

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the value of the input XB9 is greater than or equal to 100, the output Y12 will be switched on. If it is less than 100, the output will be switched off.

![](../_assets/geq.png)
# 4.11 OTE (Output Energize): Energized Output


### Description
The output signal will be outputted according to the state of the rung. In other words, if the rung is active, the output signal will be outputted in the ON (high) state, but if the rung is inactive, the output signal will be outputted in the OFF (low) state.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

Y12 will be outputted in the state of the input DO12.

![](../_assets/ote.png)
# 4.12 OTL (Output Latch): Latched Output


### Description
If the rung is active, the output signal will be outputted in the ON (high) state. However, if the rung is inactive, the output will remain the same. 

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO13 is in the ON state, Y13 will be in the ON state. Even if DO13 is switched to the OFF state afterward, Y13 will remain in the ON state.

![](../_assets/otl.png)
# 4.13 OTU (Output Unlatch): Unlatched Output


### Description
If the rung is active, the output signal will be outputted in the OFF (low) state. However, if the rung is inactive, the output will remain the same. 

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

When the input DO14 is in the ON state, Y14 will be in the OFF state. Even if DO14 is switched to the OFF state afterward, Y14 will remain in the OFF state.

![](../_assets/otu.png)
# 4.14 OSR (One Shot Rising): One-Shot-Rising Output


### Description
If the rung is active, the output signal will be outputted only for the duration of one scan. In other words, the relevant relay will be in the ON state only for the duration of one scan when the rung switches from the inactive state to the active state.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input X17 is in the ON state, the internal state relay M17 will be in the ON state. M17 will stay in the ON state until the relevant scan is complete, and it will be switched to the OFF state if a new scan starts.

![](../_assets/osr.png)
# 4.15 Reset (RES): Resetting


### Description
 If the rung is active, the timer (T) or counter (C) relay value will be cleared (-1).

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th colspan="2">timer<br>T</th>
    <th colspan="2">count<br>C</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>oprd1</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the internal state relay M18 is in the ON state, the timer relay of T28 will be cleared to -1.

![](../_assets/res.png)
# 4.16 Time on Delay (TON): Timer


### Description
After the time (timer base × preset × 10) [ms] set by calculating the time during which the rung is active, the relevant timer relay will be in the ON (high) state. However, if the rung is inactive, the relevant timer relay will be cleared (-1) immediately. 
Note) The value of T is in units of 1 ms.


<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th colspan="2">timer<br>T</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>timer</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>timer base(1/100s)</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>preset</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

When one second passes after the input DO34 is in the ON state, the timer relay of T32 will be in the ON state. At this time, the output Y34 will be in the ON state.

![](../_assets/ton.png)
# 4.17 Count Down (CTD): Counter


### Description
The rise of the rung (from being inactive to being active) will be counted down.
If the value of the relevant C becomes 0, the relevant counter will be in the ON (high) state, performing no more counting.
When the rung is active but the value of the relevant C is negative, the preset value will be stored in C.
Note) Even if the rung is inactive, C will not be cleared (-1). For clearing, the RES instruction should be executed.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI</th>
    <th colspan="2">memory<br>M, S</th>
    <th colspan="2">count<br>C</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>counter</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>preset</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the internal state relay M19 switches from the OFF state to the ON state, the value of C20 starts at 3 and continues to decrease by 1. When the value of C20 becomes 0, the counter relay will be in the ON state. At this time, the output Y35 will be in the ON state.

![](../_assets/ctd.png)
# 4.18 Add (ADD): Adding


### Description
If the rung is active, the value of “source a” and the value of “source b” will be added together, and the result value will be set in the “destination” relay. If the operation result has an overflow, the setting S7=1 will occur.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

When the input DO36 is active, 50 will be added to the value of XB3, and the result value will be set in the internal state relay MB3.

![](../_assets/add.png)
# 4.19 Subtract (SUB): Subtracting


### Description
If the rung is active, the value of “source b” will be subtracted from the value of “source a,” and the result value will be set in the “destination” relay.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO37 is active, 10 will be subtracted from the value of XB3, and the result value will be set in the internal state relay MB3.

![](../_assets/sub.png)
# 4.20 Multiply (MUL): Multiplying


### Description
If the rung is active, the value of “source a” will be multiplied by the value of “source b,” and the result value will be set in the “destination” relay.
If the operation result has an overflow, the setting S7=1 will occur.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO38 is active, the value of XB3 will be multiplied by 3, and the result value will be set in the internal state relay MB3.

![](../_assets/mul.png)
# 4.21 Divide (DIV): Dividing


### Description
If the rung is active, the value of “source a” will be divided by the value of “source b,” and the result value will be set in the “destination” relay.
If the value of “source b” is 0 or the operation result has an overflow, the setting S7=1 will occur.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO39 is active, the value of XB3 will be divided by 4, and the result value will be set in the internal state relay MB3.

![](../_assets/div.png)
# 4.22 Power (POW): Power


### Description
If the rung is active, the value of “source a” will be raised to the power of the value of “source b,” and the result value will be set in the “destination” relay. If the operation result has an overflow, the setting S7=1 will occur.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Use of example

If the input DO40 is active, the value of XB3 will be raised to the power of 2, and the result value will be set in the internal state relay MB3. 

![](../_assets/pow.png)
# 4.23 TOD (Convert to BCD): Converting to BCD


### Description
If the rung is active, the value of the "source" will be converted to a BCD value, and the converted value will be stored in the "destination."
This instruction will be convenient when using a device that displays values ​​in a 7-segment display in the BCD format.
If the data type for the "destination" is in the byte (B) format, the value of the "source" will be converted to two digits. If it is in the word (W) format, the value of the "source" will be converted to four digits. However, if the value of the "source" is greater than the number of digits to convert to, the setting S6=1 will occur.

<br>

### Types that can be used as an operand
(not possible for X, unsigned integers for u)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>u</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO42 is active, the value of XB3 will be converted to a BCD value, and the converted value will be set in the internal state relay MB3. 
(Note: Binary Coded Decimal (BCD) refers to numbers whose 4-bit code value can have a value ranging from 0 to 9. That is, for BCD numbers, A–F among the numbers 0–F that can be represented with 4 bits are not used.)
If &H7B(123) is converted to a BCD value, the converted value will be &H23(35), and because &H7B(123) is greater than &H63(99), the setting S6=1 will occur.


![](../_assets/tod.png)
# 4.24 FRD (Convert from BCD to Integer): Converting to an Integer


### Description
If the rung is active, the BCD value of the "source" will be converted to an integer, and the converted value will be stored in the "destination." 
This instruction can be conveniently used when the value of the cam switch outputted in BCD format is received as an input.
If the value of the "source" is not a BCD value, the setting S6=1 will occur.
In addition, if the "source" is in the word (W) format, and the "destination" is in the byte (B) format, the maximum value of the "source" to be converted will be &H9999. Therefore, the result of the conversion to an integer will be 9999 (&H270F), which will cause the byte range &Hff to be exceeded and, accordingly, an overflow to occur. In this case, the setting S=6 will occur.

<br>

### Types that can be used as an operand
(not possible for X, unsigned integers for u)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>u</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO43 is active, the value (BCD) of XB3 will be converted to an integer, and the converted value will be set in the internal state relay MB3.
If &H23(35) is converted to an integer, the integer will be &H17(23).



![](../_assets/frd.png)
# 4.25 SEG (7-segment): Converting to an 7-segment Value


### Description
If the rung is active, the value of the "source" will be converted to a 7-segment value (8 bits), and the converted value will be stored in the "destination."
If the "destination" is in the word (W) format, two values in a 7-segment format (8 bits) will be stored in the "destination."


<br>

### Types that can be used as an operand
(not possible for X, unsigned integers for u)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>u</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO44 is active, the 7-segment value corresponding to the value of XB3 will be set in the internal state relay MW3.
For &H17, the value &H0607 combining SEGD_1(SEGM_B|SEGM_C = 0x02|0x04 = 0x06)=&H06 and 
SEGD_7(SEGM_A|SEGM_B|SEGM_C = 0x01|0x02|0x04 = 0x07)=&H07 will be stored in the internal state relay MW3.


![](../_assets/seg.png)


<br>

### 7-segment data

![](../_assets/seg_data.png)

SEGM_A = 0x01<br>
SEGM_B = 0x02<br>
SEGM_C = 0x04<br>
SEGM_D = 0x08<br>
SEGM_E = 0x10<br>
SEGM_F = 0x20<br>
SEGM_G = 0x40<br>
SEGM_DP = 0x80<br>

# 4.26 MOV (Move): Moving


### Description
If the rung is active, the value of the "source" will be copied to the "destination."
If the "source" is in the word (W) format, and the "destination" is in the byte (B) format, only the lower byte of the value of the "source" will be copied to the "destination." 
Because all data of the embedded programmable logic controller (PLC) is processed as signed data, if the "source" is in the byte (B) format and its value is -1(&Hff), this value will be copied to the "destination," which is in the word (W) format, as -1(&HFFFF) (&H00ff becomes the value of 255.)



<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO55 is active, 55 will be set in the internal state relay MB2.

![](../_assets/mov.png)
# 4.27 Copy Data (COP): Copying


### Description
If the rung is active, values will be copied from the location of the “source” to the location of the “destination” as many as the number of the “length.”
If the “source” is a number, the “destination” will be filled with the value of the “source” as much as the number of the “length.” In this case, when the “destination” is in bit format, if the value of the “source” is 0, the “destination” will be filled with OFFs, and if the value of the “source” is not 0, the “destination” will be filled with ONs.
If the “source” is a relay, the data types of the “source” and “destination” should be the same. That is, if the “source” is in the bit format, the “destination” should be in the bit format; if the “source” is in the byte (B) format, then the “destination” should be in the byte (B) format; if the “source” is in the word (W) format, then the “destination” should also be in the word (W) format.
If the “source” + “length” is greater than the maximum number of the “source” relays or the “destination” + “length” is greater than the maximum number of “destination” relays, copying will be performed only up to the maximum number of relays.


<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>length</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO56 is active, the value corresponding to 8 bytes will be copied from the input DOB2 to the output YB2 as a value corresponding to 8 bytes.

![](../_assets/cop.png)
# 4.28 Conditional Copy Data (CCOP): Conditional Copying


### Description
Depending on the state of the rung, values will be copied from the location of the “source a” or “source b” to the location of the “destination” as many as the number of the “length.”
If the “source” is a number, the “destination” will be filled with the relevant value as much as the value of the “length.”. In this case, when the “destination” is in bit format, if the relevant value is 0, the “destination” will be filled with OFFs, and if the relevant value is not 0, the “destination” will be filled with ONs.
If the “source” is a relay, the data types of the “source” and “destination” should be the same. That is, if the “source” is in the bit format, the “destination” should be in the bit format; if the “source” is in the byte (B) format, then the “destination” should be in the byte (B) format; if the “source” is in the word (W) format, then the “destination” should also be in the word (W) format.
If the “source” + “length” is greater than the maximum number of the “source” relays or the “destination” + “length” is greater than the maximum number of “destination” relays, copying will be performed only up to the maximum number of relays.


<br>

### Types that can be used as an operant
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>source a</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>source b</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>length</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO57 is active, the value corresponding to 4 bytes will be copied from the input DOB2 to the output YB2 as a value corresponding to 4 bytes. On the contrary, if the input DO57 is active, the value corresponding to 4 bytes will be copied from the input DOB12 to the output YB2 as a value corresponding to 4 bytes.

![](../_assets/ccop.png)
# 4.29 ROT (Rotating Output): Rotating the Output


### Description
If the rung is active, the relay value, other than 0, within the range of the "count" will be inputted from the "start relay" to the "out relay" for the duration of the "repeat time."
If the "reset relay" has a signal input, the "start relay" will start to be filled with 0 as much as the number of the "count," the value of the timer will be initialized to the value of the "repeat time," and the "out relay" will output 0.
This instruction can be used very conveniently for cases where outputting the error number for a specified period of time while there is only one device available for outputting the error number is required even though there are many types of errors that can occur.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th colspan="2">timer<br>T</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>start relay</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>count</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>timer relay</td>
    <td>X</td>
    <td>X</td>
    <td>x</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>repeat time</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>out relay</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>reset relay</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>temp relay</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If one or more errors related to the error conditions from 1 to 3 are present, the error number will be stored in MW50–MW55. Here, when the input DO58 is active, the error number generated by the ROT instruction will be stored in MW70 for 2 seconds, while the number will be converted to a BCD value by the TOD instruction and displayed sequentially on the display device connected to YB3.
If X3, connected for an external error reset signal, has an input signal, the contents of MW51–MW55 where the error numbers are stored will be cleared to 0 and MW70 and MW80 will be also cleared to 0 with the display device indicating 0 accordingly.

![](../_assets/rot.png)
# 4.30 FOR (FOR): Repeating the Block


### Description
If the rung is active, the block up to the Next instruction will be executed repeatedly, while the "idx" relay value increase by as much as the "step" value from the "init" value to the "final" value.
When the FOR instruction is executed, the "init" value should be unconditionally substituted with the "idx' relay.
The FOR/NEXT instruction can be nested up to 10. For example: → FOR() FOR() FOR() … .NEXT NEXT NEXT
In a state where the "step" value is greater than 0, if the "init" value is greater than the "final" value, no execution will occur. Instead, jumping to the Next instruction will occur.
In a state where the "step" value is less than 0, if the "init" value is less than the "final" value, no execution will occur. Instead, jumping to the Next instruction will occur.
The "final" and "step" can be designated as variables. However, only the values ​​at the point when the FOR instruction started will be used.
To leave in the middle of a FOR instruction under special circumstances, the JMP (negative number) instruction, which will be described later, can be used (refer to the description of the JMP instruction).
Caution: The FOR instruction does not have any additional processing for branching.
Note: For more details on the NEXT instruction, refer to [4.31 NEXT (NEXT)](./31-next)

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>idx</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>initial</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>final</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>step</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

The instruction {XIC(DO-2), OTL(Y-2)} will be executed in repetition, while the value will increase by 1 from 1 to 4 in SW62.  
In other words, in a state where “idx” is using a relay for relative addressing (SW62–SW79), and the DO relay of the XIC instruction and the Y relay of the OTL instruction are “-2”, the number in the value of SW62 will be applied. Therefore, the Y relay number corresponding to the number of a signal in the High state among DO1–DO4 will be outputted in the High state, while the Y output of the number that is not inputted will retain its previous state. 
Note: Relative addressing refers to a method where the relay address will be designated to a value stored in SW62–SW79 if the relevant relay is set to a number ranging from -2 to -9 regardless of the type of relay.


![](../_assets/for.png)
# 4.31 NEXT (NEXT): Next Block


### Description
The operation will be performed according to the "step" of the FOR instructions.
If the "step" value is greater than 0, the execution will occur repeatedly until the "idx" relay value becomes less than or equal to the "final" value.
If the "step" value is less than 0, the execution will occur repeatedly until the "idx" relay value becomes greater than or equal to the "final" value.
If a NEXT instruction is executed without a FOR instruction, the NEXT instruction will be ignored.
Caution:  
The FOR/NEXT instruction does not have any additional processing for branching. As such, if a FOR instruction is recorded inside a branch, and a NEXT instruction is recorded outside the branch or inside another branch, the FOR instructions will not operate correctly.
Note: For more details on the FOR instructions, refer to [4.30 FOR (FOR)](./30-for)

<br>

### Example of use

Refer to the example on the use of the FOR instructions.
# 4.32 LBL (Label): Designating a Label


### Description
The location of the label to jump to with the JMP instruction will be designated as a number (const) greater than 0. 
The LBL instruction will designate the location regardless of whether the rung is active or inactive.
Note: For more details on the JMP instruction, refer to [4.33 JMP (Jump)](./33-jmp)

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>label</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

Because these instructions will be used together with the JMP command, refer to the description of the JMP instructions.
# 4.33 JMP (Jump): Jumping


### Description
If the rung is active, there will be a jump to the location where the LBL instruction matching the value of the label designated in "label" is located. 
In particular, if "label" is specified as a value less than 0, it can be used as a feature for leaving the middle of a FOR instruction (skips according to the number specified in a negative number.)
Caution 1:  
If the location of the label is above the JMP instruction and there is no condition in front of the JMP instruction, infinite looping may occur, which will require your attention. When this occurs, the setting will be S16=1 because the scan time exceeded 5 seconds.
Caution 2:  
Leaving the block by using the JMP (positive number) instruction within the FOR/NEXT instruction block may cause the block control to go wrong. In that case, programming a way to skip to the NEXT instruction by using the JMP instruction (negative number) will be required.
Note: For more details on the LBL instruction, refer to [4.32 LBL (Label)](./32-lbl)

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>idx</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

If the input DO19 is active, there will be a jump to the relevant LBL instruction according to the "label 99" of the JMP instruction. It means the instruction {XIC(DO20), OTE(Y20)} will not be executed.  
If the input DO19 is inactive, the JMP instruction will not be executed, so the {XIC(DO20), OTE(Y20)} instruction written in the next rung will be exeucted.


![](../_assets/jmp.png)
# 4.34 CALL (Call): Calling a Sub-ladder Program


### Description
If the rung is active, the sub-ladder program with a number (1 to 99) designated by the "file number" will be called.
There can be up to 99 file names for the sub-ladder program, which can range from S01xxxx.LAD to S99xxxx.LAD, and for the "xxxx" section of the file name, the user can arbitrarily add up to 15 characters.

<br>

### Types that can be used as an operand
(not possible for X)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>idx</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### Example of use

When the input DO21 is active, files numbered from S01xxxx.LAD to S99xxxx.LAD will be called in rotation.
As a result of executing the CALL instruction, if no sub-ladder program relevant to the number exists or the value of the number is outside of the range of 1 to 99, the setting S17=1 will occur. However, if the CALL instruction is executed normally, the setting S17=0 will occur. Therefore, in cases where there should be a necessary sub-ladder, it is possible to detect errors by using S17 after calling.  
If calling the sub-ladders numbering from 1 to 99 with the CALL instruction in the main ladder program and assigning a sub-ladder number for each application are possible, we can expect a ladder program relevant to the application to be executed automatically by loading the necessary sub-ladder program via the controller depending on each application.


![](../_assets/call.png)
# 4.35 END (End): Ending the Ladder Program


### Description
If the rung is active, the ladder program currently being executed will be ended. 
If the current ladder program is a sub-ladder program, returning to the main ladder program will occur. However, if the current ladder program is the main ladder program, its execution will be ended, and the main ladder program will be executed again from the beginning.

<br>

### Example of use

If the input DO22 is active, the ladder program will be ended by the END instruction, and the instructions of the rung written afterward will not be executed.
If the input DO22 is inactive, the END instruction will not be executed, allowing the instructions of the rung written afterward to be executed naturally.


![](../_assets/end.png)
# 5. Difference in the Embedded PLC between Hi5a and Hi6

The functions of the Hi6 controller's embedded PLC are similar to those of the Hi5a controller's embedded PLC, and the same HRLadder, or the same ladder editor, is used. 
Therefore, users who are already familiar with the functions of the Hi5a controller's embedded PLC can quickly learn from this manual by checking only the different parts in the Hi6 controller.

The following content includes the list of the different parts.

<br>

## HRLadder online connection

HRLadder v2.80 or later supports the Hi6 controller.
Versions of HRLadder earlier than v2.80 allows remote connection through automatic recognition of the controller type when the online button is pressed.
However, for HRLadder v2.80 or later, you need to select the controller type in the attributes of the project, then press the online button.

![](_assets/hrladder-prj-prop.png)

![](_assets/hrladder-prj-prop2.png)

<br>

## Type of relay

### Hi5a

M relays of MW1–MW1000 are supported.
A special relay SP exists.
Dedicated input and output signals are included in SW.

### Hi6

M relays are largely extended to a range of MW0–MW19998, so you can use them as substitutes for others.
SP relays are integrated into the area for special flags of [S relay - Fixed area](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/korean/3-relay/4-sw-relay/1-fixed-area)
For dedicated input and output signals, support will be provided with SI and SO. 


<br>


## Index

### Hi5a
The index starts with 1.
The index for word, long, and float increases by 1. 
For example, DO16–DO23 are the same as DOW1


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
The index starts with 0.
The index of word, long and flow will increase by matching the byte location.
For example, DOW increases in the form of DOW0, DOW2, DOW4, DOW6..., and DOL increases in the form of DOL0, DOL4, DOL8...
As shown in the figure below, DO16–DO23 are the same as DOW2.

Refer to [3.2 Designating a relay](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/korean/3-relay/2-relay-expression)

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


## System relay (SW relay)

### Hi5a

In most cases, there is a fixed SW relay index address for each monitoring item.
However, among the index addresses, SW220–249 are for 10 multipurpose slots, and it is possible to put a desired code, among the codes for system variables, mainboard storage space, analog input/output, date/time, and GE variables, into the desired slot and perform monitoring.

- Most items: Fixed area
- Some items: Optional items area (slot)

<br>

### Hi6

The area of SB0–SB1999 is the [S Relay Fixed Area](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/korean/3-relay/4-sw-relay/1-fixed-area), which has a fixed index address for each item just like Hi5a.

However, the area of SB2000– is the [Optional items area](https://hrbook-hrc.web.app/#/view/doc-hi6-embedded-plc/korean/3-relay/4-sw-relay/README), which has about 900 multipurpose slots, permitting their use by inserting instructions for desired items.


Nearly most of the items will be montored via the optional items area.

- Most items: Optional items area (slot)
- Some items: Fixed area
