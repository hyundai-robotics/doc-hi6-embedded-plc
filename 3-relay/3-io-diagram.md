# 3.3 Input/output diagram

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
