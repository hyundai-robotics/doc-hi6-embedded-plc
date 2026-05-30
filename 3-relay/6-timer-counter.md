# 3.6 Timer & Counter relay

(1) All timer and counter relays support down-counting only.  
*	The timer base can be set by the user in 10msec units.  
*	Since the timer value is internally processed as a 32-bit value, it can count up to 2,147,483,647 [msec] (approximately 597 hours). 
<br>
<br>

(2) The values   of the Timer & Counter have the following meanings:  
<table class="tg">
<thead>
	<tr>
		<th>Timer & Counter value</th>
		<th>Description</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>0</td>
		<td>Contact On (=counting completed)</td>
	</tr>
	<tr>
		<td>-1</td>
		<td>Contact Off</td>
	</tr>
	<tr>
		<td>Others</td>
		<td>Contact Off; timing & counting (in progress)</td>
	</tr>
</tbody>
</table>
<br>

(3) If the rung to which the Timer & Counter relay is connected is inactive,  
*	TON: The value of TL(Timer) become -1.  
*	CTD: The value of CL(Counter) is maintained continuously. 
<br>
<br>

(4) While the rung to which the Timer & Counter relay is connected is active, 
*	TON <br> 
    If the value of TL is less than 0, the initial value of TL is stored as "timer base x preset x 10", and if the value of TL is greater than 0, it decreases by 5 every 5 msec. 

*	CTD <br>
    If the CL value is less than 0, the initial CL value becomes the preset value. If the CL value is greater than 0, the value decreases by 1 each time the CL changes from inactive to active. 

