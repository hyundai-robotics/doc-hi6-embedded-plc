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
