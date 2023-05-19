# 4.35 END (End): Ending the Ladder Program


### Description
If the rung is active, the ladder program currently being executed will be ended. 
If the current ladder program is a sub-ladder program, returning to the main ladder program will occur. However, if the current ladder program is the main ladder program, its execution will be ended, and the main ladder program will be executed again from the beginning.

<br>

### Example of use

If the input DO22 is active, the ladder program will be ended by the END instruction, and the instructions of the rung written afterward will not be executed.
If the input DO22 is inactive, the END instruction will not be executed, allowing the instructions of the rung written afterward to be executed naturally.


![](../_assets/end.png)
