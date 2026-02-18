# 2.1. 设置嵌入式PLC的模式

在 "[F7: Condition setting] - PLC的操作模式" 中，您可以选择嵌入式可编程逻辑控制器（PLC）的操作模式，包括 Off、Stop、R-Stop、R-Run 或 Run 模式。 R-Stop 和 R-Run 分别指代远程停止和远程运行，每个状态都表示该模式可以通过以太网连接的PC上的HRLadder远程更改。

![图 2.1 设置嵌入式PLC的模式](../_assets/plc_run_mode.png)

<br>
<br>
根据所选模式，状态将在教学挂件屏幕的右上角用图标指示。即在PLC=R-Run或PLC=Run的情况下，将显示如上图所示的PLC图标；在PLC=Off的情况下，PLC图标将消失，如下图所示；在PLC=Stop的情况下，PLC图标上将显示红色禁止标记。

![图 2.2 嵌入式PLC在关闭状态](../_assets/plc_mode_off.png)

 
![图 2.3 嵌入式PLC在停止状态](../_assets/plc_mode_stop.png)


* Off  
嵌入式PLC的功能将被关闭。当这种情况发生时，机器人控制器的逻辑输出FB0.DO0-FB9.DO959将自动作为物理输出（意味着旁路）输出，FB0.Y0-FB9.Y959，物理输入FB0.X0-FB9.X959将自动作为逻辑输入FB0.DI0-FB9.DI595输入。

* R-Stop/Stop  
嵌入式PLC的操作将被停止。R-Stop表示一种远程状态，可以通过HRLadder进行更改。如果设置了Stop模式，将无法通过HRLadder更改操作模式。 
当嵌入式PLC停止时，PLC输出信号的DI和Y继电器将自动变为0。 *(DI从机器人语言或分配的角度来看是输入，但从嵌入式PLC的角度来看是输出。)*  

* R-Run/Run  
嵌入式PLC将被执行。R-Run表示一种远程状态，可以通过HRLadder进行更改。如果设置了Run模式，将无法通过HRLadder更改操作模式。