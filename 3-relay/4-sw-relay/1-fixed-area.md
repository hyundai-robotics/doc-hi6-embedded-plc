# 3.4.1 S relay - Fixed area

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
</table>