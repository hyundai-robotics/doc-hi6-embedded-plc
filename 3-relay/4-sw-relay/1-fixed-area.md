# 3.4.1 S relay - Fixed area

Please refer to the table shown below for the SB0-SB1999 areas for which fixed items are provided.

<style type="text/css">
table  {border-collapse:collapse;}
td {
    border-color:gray;
    border-style:solid;
    border-width:1px;
    padding: 1px 4px;
    height: auto !important;
}
.grayed {background-color:lightgray;}
</style>

<div class="page-break"></div>

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
		<td class='grayed'></td>
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
	<tr>
		<td>SB3</td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td class='grayed'></td>
		<td>Self diagnosis completed </td>
		<td>T/P booting completed</td>
		<td></td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

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
		<td>PLC execution mode</td>
		<td>0=stop, 1=R.stop, 2=R.run,<br>
		 3= run, 4=off, 5=no program</td>
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
		<td>Software version: First</td>
		<td>e.g., In the case of V60.05-08, 60</td>
	</tr>
	<tr>
		<td>SB15</td>
		<td>Software version: Second</td>
		<td>e.g., In the case of V60.05-08, 5</td>
	</tr>
	<tr>
		<td>SB16</td>
		<td>Software version: Small-fix</td>
		<td>e.g., In the case of V60.05-08, 8</td>
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
		<td>SB30</td>
		<td>Gun output status</td>
		<td></td>
	</tr>
	<tr>
		<td>SB39</td>
		<td>Current user coordinate number</td>
		<td></td>
	</tr>
	<tr>
		<td>SB40</td>
		<td>Current tool number</td>
		<td></td>
	</tr>
	<tr>
		<td>SB41</td>
		<td>Robot state</td>
		<td>0=stop, 1=run, 2=wait</td>
	</tr>
	<tr>
		<td>SB42</td>
		<td>Playback speed</td>
		<td>%</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SW44</td>
		<td>Step go/back max speed</td>
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
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
</tbody>
</table>

<div class="page-break"></div>

<table class="tg">
<tbody>
	<tr>
		<td>SW50</td>
		<td>Error/warning auxiliary information</td>
		<td></td>
	</tr>
	<tr>
		<td>SW62</td>
		<td>Indirect address designation (relay-2)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW64</td>
		<td>Indirect address designation (relay-4)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW66</td>
		<td>Indirect address designation (relay-6)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW68</td>
		<td>Indirect address designation (relay-8)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW70</td>
		<td>Indirect address designation (relay-10)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW72</td>
		<td>Indirect address designation (relay-12)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW74</td>
		<td>Indirect address designation (relay-14)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW76</td>
		<td>Indirect address designation (relay-16)</td>
		<td></td>
	</tr>
	<tr>
		<td>SW78</td>
		<td>Indirect address designation (relay-18)</td>
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
		<td>SB111</td>
		<td>Run time selection</td>
		<td>1=Total (after initialization),<br>
		2=Total (after power input),<br>
		3=Last cycle,<br>
		4=Current cycle
			</td>
	</tr>
	<tr>
		<td>SL112</td>
		<td>Motor on (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL116</td>
		<td>Motor on (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL120</td>
		<td>Run time (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL124</td>
		<td>Run time (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL128</td>
		<td>Movement time (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL132</td>
		<td>Movement time (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL136</td>
		<td>Cycle count</td>
		<td></td>
	</tr>
	<tr>
		<td>SL140</td>
		<td>wait, di wait time (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL144</td>
		<td>wait, di wait time (ms)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL148</td>
		<td>delay wait time (day)</td>
		<td></td>
	</tr>
	<tr>
		<td>SL152</td>
		<td>delay wait time (ms)</td>
		<td></td>
	</tr>
	</tbody>
</table>

<div class="page-break"></div>

<table class="tg">
<tbody>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB159</td>
		<td>Axis information selection</td>
		<td>1 = Current position 
		<br>(axis angle),<br>
		2 = Current position 
		<br>(base coordinate),<br>
		3 = Current position 
		<br>(base/user coordinate)<br>
		6 = Axis speed,<br>
		7 = Motor speed<br>
		8 = Motor speed command <br>
		when speed control(rpm)<br>
		10 = Load factor(I/Ir),<br>
		11 = Load factor(I/Ip),<br>
		13 = Load factor(continuous)<br>
		15 = Encoder temperature<br>
		18 = Accumulated distance<br>
		for each axis<br>
		111 = Position deviation<br>
		(current),<br>
		112 = Position deviation<br>
		(maximum)<br>
		124 = Encoder communication failure count</td>
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
		<tr>
		<td>SL200</td>
		<td>Control status of each axis<br>
		(0=off, 1=on)</td>
		<td></td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	</tbody>
</table>

<div class="page-break"></div>

<table class="tg">
<tbody>
	<tr>
		<td>SW210</br>
		...</br>
		SW280</td>
		<td>Program Number
		<td>(main task = sw210,<br>
		subtask 1 = sw220,<br>
		subtask 2 = sw230,<br> 
		subtask 3 = sw240,<br>
		subtask 4 = sw250,<br>
		subtask 5 = sw260,<br>
		subtask 6 = sw270,<br>
		subtask 7 = sw280)</td>
	</tr>
	<tr>
		<td>SW212</br>
		...</br>
		SW282</td>
		<td>Step Number</td>
		<td>(main task = sw212,<br>
		subtask 1 = sw222,<br>
		subtask 2 = sw232,<br>
		subtask 3 = sw242,<br>
		subtask 4 = sw252,<br>
		subtask 5 = sw262,<br>
		subtask 6 = sw272,<br>
		subtask 7 = sw282)</td></td>
	</tr>
	<tr>
		<td>SW214</br>
		...</br>
		SW284</td>
		<td>Function Number</td>
		<td>(main task = sw214,<br>
		subtask 1 = sw224,<br>
		 subtask 2 = sw234,<br>
		 subtask 3 = sw244,<br>
		subtask 4 = sw254,<br>
		subtask 5 = sw264,<br>
		subtask 6 = sw274,<br>
		subtask 7 = sw284)</td>
	</tr>
	<tr>
		<td>SW216</br>
		...</br>
		SW286</td>
		<td>Main Program Number</td>
		<td>(main task = sw216,<br>
		subtask 1 = sw226,<br>
		 subtask 2 = sw236,<br>
		 subtask 3 = sw246,<br>
		subtask 4 = sw256,<br>
		subtask 5 = sw266,<br>
		subtask 6 = sw276,<br>
		subtask 7 = sw286)</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>
	<tr>
		<td>SB499</td>
		<td>Function enables</td>
		<td>b0 (S3992) = Axis collision detection,<br>
		    b1 (S3993) = Model-based impact detection
		</td>
	</tr>
	<tr class='grayed'><td>-</td><td>-</td><td>-</td></tr>	
	<tr>
		<td>SW500</td>
		<td>Gun Number</td>
		<td>0=Currently selected gun,<br>
		1-16</td>
	</tr>
	<tr>
		<td>SW502</td>
		<td>Gun Search Status</td>
		<td>1=Complete, 0=Incomplete</td>
	</tr>
	<tr>
		<td>SW504</td>
		<td>Moving Electrode<br>
		Wear Amount x 100</td>
		<td></td>
	</tr>
	<tr>
		<td>SW506</td>
		<td>Fixed Electrode<br>
		Wear Amount x 100</td>
		<td></td>
	</tr>
	<tr>
		<td>SW508</td>
		<td>Pressurizing Force<br>
		Command Value x 10</td>
		<td></td>
	</tr>
	<tr>
		<td>SW510</td>
		<td>Pressurizing Force<br>
		Current Value x 10</td>
		<td></td>
	</tr>
</tbody>
</table>
</tbody>
</table>

<div class="page-break"></div>
