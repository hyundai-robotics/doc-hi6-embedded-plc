# 3.3.2 SI - System input

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
</style>

<table class="tg">
<thead>
	<tr>
		<th>System board</th>
		<th>Byte</th>
		<th>Bit</th>
		<th>Name</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td rowspan=32>BD630</td>
		<td rowspan=8>sib0</td>
		<td>si0</td>
		<td>Lift Axis/Arm Limit</td>
	</tr>
	<tr>
		<td>si1</td>
		<td>Primary Axis Limit</td>
	</tr>
	<tr>
		<td>si2</td>
		<td>Add Axis Limit</td>
	</tr>
	<tr>
		<td>si3</td>
		<td>Ext Axis Limit</td>
	</tr>
	<tr>
		<td>si4</td>
		<td>Emergency stop (OP)</td>
	</tr>
	<tr>
		<td>si5</td>
		<td>Emergency stop (TP)</td>
	</tr>
	<tr>
		<td>si6</td>
		<td>Emergency stop (Ext)</td>
	</tr>
	<tr>
		<td>si7</td>
		<td>Safety chain</td>
	</tr>
	<tr>
		<td rowspan=7>sib1</td>
		<td>si8</td>
		<td>Mode switch (Auto)</td>
	</tr>
	<tr>
		<td>si9</td>
		<td>Mode switch (Manual)</td>
	</tr>
	<tr>
		<td>si10</td>
		<td>Mode switch (Remote)</td>
	</tr>	
	<tr>
		<td>si11</td>
		<td>TP Enabling switch</td>
	</tr>	
	<tr>
		<td>si12</td>
		<td>Safety guard (Auto)</td>
	</tr>	
	<tr>
		<td>si13</td>
		<td>Safety guard (Auto ext.)</td>
	</tr>	
	<tr>
		<td>si14</td>
		<td>Safety guard (General)</td>
	</tr>	
	<tr>
		<td rowspan=8>sib2</td>
		<td>si16</td>
		<td>PreCharge</td>
	</tr>
	<tr>
		<td>si17</td>
		<td>Motors Power</td>
	</tr>
	<tr>
		<td>si18</td>
		<td>DisCharge</td>
	</tr>	
	<tr>
		<td>si19</td>
		<td>Motor ON (TP)</td>
	</tr>	
	<tr>
		<td>si20</td>
		<td>Start (TP)</td>
	</tr>	
	<tr>
		<td>si21</td>
		<td>Stop (TP)</td>
	</tr>	
	<tr>
		<td>si22</td>
		<td>OP installed</td>
	</tr>	
	<tr>
		<td>si23</td>
		<td>Motor ON(Ext.)</td>
	</tr>	
	<tr>
		<td rowspan=2>sib3</td>
		<td>si24</td>
		<td>Heartbeat 1</td>
	</tr>
	<tr>
		<td>si25</td>
		<td>Heartbeat 2</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640 - 1</td>
		<td rowspan=8>sib4</td>
		<td>si32</td>
		<td>Brake status 1</td>
	</tr>
	<tr>
		<td>si33</td>
		<td>Brake status 2</td>
	</tr>
	<tr>
		<td>si34</td>
		<td>Brake status 3</td>
	</tr>
	<tr>
		<td>si35</td>
		<td>Brake status 4</td>
	</tr>
	<tr>
		<td>si36</td>
		<td>Brake status 5</td>
	</tr>
	<tr>
		<td>si37</td>
		<td>Brake status 6</td>
	</tr>
	<tr>
		<td>si38</td>
		<td>Brake status 7</td>
	</tr>
	<tr>
		<td>si39</td>
		<td>Brake status 8</td>
	</tr>
	<tr>
		<td rowspan=8>sib5</td>
		<td>si40</td>
		<td>Precharge relay on</td>
	</tr>
	<tr>
		<td>si41</td>
		<td>Dynamic resistor overheat</td>
	</tr>
	<tr>
		<td>si42</td>
		<td>Over voltage</td>
	</tr>
	<tr>
		<td>si43</td>
		<td>Under voltage</td>
	</tr>
	<tr>
		<td>si44</td>
		<td>Dynamic brake status</td>
	</tr>
	<tr>
		<td>si45</td>
		<td>/SVON (Servo ON)</td>
	</tr>
	<tr>
		<td>si46</td>
		<td>Robot-fan failure</td>
	</tr>
	<tr>
		<td>si47</td>
		<td>Diode module overheat</td>
	</tr>
	<tr>
		<td rowspan=8>sib6</td>
		<td>si48</td>
		<td>User 1</td>
	</tr>
	<tr>
		<td>si49</td>
		<td>User 2</td>
	</tr>
	<tr>
		<td>si50</td>
		<td>User 3</td>
	</tr>
	<tr>
		<td>si51</td>
		<td>User 4</td>
	</tr>
	<tr>
		<td>si52</td>
		<td>User 5 (BD640T)</td>
	</tr>
	<tr>
		<td>si53</td>
		<td>User 6 (BD640T)</td>
	</tr>
	<tr>
		<td>si54</td>
		<td>User 7 (BD640T)</td>
	</tr>
	<tr>
		<td>si55</td>
		<td>User 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=2>sib7</td>
		<td>si56</td>
		<td>Brake power fail</td>
	</tr>
	<tr>
		<td>si57</td>
		<td>AC voltage down</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640 - 2</td>
		<td rowspan=8>sib8</td>
		<td>si64</td>
		<td>Brake status 1</td>
	</tr>
	<tr>
		<td>si65</td>
		<td>Brake status 2</td>
	</tr>
	<tr>
		<td>si66</td>
		<td>Brake status 3</td>
	</tr>
	<tr>
		<td>si67</td>
		<td>Brake status 4</td>
	</tr>
	<tr>
		<td>si68</td>
		<td>Brake status 5</td>
	</tr>
	<tr>
		<td>si69</td>
		<td>Brake status 6</td>
	</tr>
	<tr>
		<td>si70</td>
		<td>Brake status 7</td>
	</tr>
	<tr>
		<td>si71</td>
		<td>Brake status 8</td>
	</tr>
	<tr>
		<td rowspan=8>sib9</td>
		<td>si72</td>
		<td>Precharge relay on</td>
	</tr>
	<tr>
		<td>si73</td>
		<td>Dynamic resistor overheat</td>
	</tr>
	<tr>
		<td>si74</td>
		<td>Over voltage</td>
	</tr>
	<tr>
		<td>si75</td>
		<td>Under voltage</td>
	</tr>
	<tr>
		<td>si76</td>
		<td>Dynamic brake status</td>
	</tr>
	<tr>
		<td>si77</td>
		<td>/SVON (Servo ON)</td>
	</tr>
	<tr>
		<td>si78</td>
		<td>Robot-fan failure</td>
	</tr>
	<tr>
		<td>si79</td>
		<td>Diode module overheat</td>
	</tr>
	<tr>
		<td rowspan=8>sib10</td>
		<td>si80</td>
		<td>User 1</td>
	</tr>
	<tr>
		<td>si81</td>
		<td>User 2</td>
	</tr>
	<tr>
		<td>si82</td>
		<td>User 3</td>
	</tr>
	<tr>
		<td>si83</td>
		<td>User 4</td>
	</tr>
	<tr>
		<td>si84</td>
		<td>User 5 (BD640T)</td>
	</tr>
	<tr>
		<td>si85</td>
		<td>User 6 (BD640T)</td>
	</tr>
	<tr>
		<td>si86</td>
		<td>User 7 (BD640T)</td>
	</tr>
	<tr>
		<td>si87</td>
		<td>User 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=2>sib11</td>
		<td>si88</td>
		<td>Brake power fail</td>
	</tr>
	<tr>
		<td>si89</td>
		<td>AC voltage down</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640 - 3</td>
		<td rowspan=8>sib12</td>
		<td>si96</td>
		<td>Brake status 1</td>
	</tr>
	<tr>
		<td>si97</td>
		<td>Brake status 2</td>
	</tr>
	<tr>
		<td>si98</td>
		<td>Brake status 3</td>
	</tr>
	<tr>
		<td>si99</td>
		<td>Brake status 4</td>
	</tr>
	<tr>
		<td>si100</td>
		<td>Brake status 5</td>
	</tr>
	<tr>
		<td>si101</td>
		<td>Brake status 6</td>
	</tr>
	<tr>
		<td>si102</td>
		<td>Brake status 7</td>
	</tr>
	<tr>
		<td>si103</td>
		<td>Brake status 8</td>
	</tr>
	<tr>
		<td rowspan=8>sib13</td>
		<td>si104</td>
		<td>Precharge relay on</td>
	</tr>
	<tr>
		<td>si105</td>
		<td>Dynamic resistor overheat</td>
	</tr>
	<tr>
		<td>si106</td>
		<td>Over voltage</td>
	</tr>
	<tr>
		<td>si107</td>
		<td>Under voltage</td>
	</tr>
	<tr>
		<td>si108</td>
		<td>Dynamic brake status</td>
	</tr>
	<tr>
		<td>si109</td>
		<td>/SVON (Servo ON)</td>
	</tr>
	<tr>
		<td>si110</td>
		<td>Robot-fan failure</td>
	</tr>
	<tr>
		<td>si111</td>
		<td>Diode module overheat</td>
	</tr>
	<tr>
		<td rowspan=8>sib14</td>
		<td>si112</td>
		<td>User 1</td>
	</tr>
	<tr>
		<td>si113</td>
		<td>User 2</td>
	</tr>
	<tr>
		<td>si114</td>
		<td>User 3</td>
	</tr>
	<tr>
		<td>si115</td>
		<td>User 4</td>
	</tr>
	<tr>
		<td>si116</td>
		<td>User 5 (BD640T)</td>
	</tr>
	<tr>
		<td>si117</td>
		<td>User 6 (BD640T)</td>
	</tr>
	<tr>
		<td>si118</td>
		<td>User 7 (BD640T)</td>
	</tr>
	<tr>
		<td>si119</td>
		<td>User 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=2>sib15</td>
		<td>si120</td>
		<td>Brake power fail</td>
	</tr>
	<tr>
		<td>si121</td>
		<td>AC voltage down</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640 - 4</td>
		<td rowspan=8>sib16</td>
		<td>si128</td>
		<td>Brake status 1</td>
	</tr>
	<tr>
		<td>si129</td>
		<td>Brake status 2</td>
	</tr>
	<tr>
		<td>si130</td>
		<td>Brake status 3</td>
	</tr>
	<tr>
		<td>si131</td>
		<td>Brake status 4</td>
	</tr>
	<tr>
		<td>si132</td>
		<td>Brake status 5</td>
	</tr>
	<tr>
		<td>si133</td>
		<td>Brake status 6</td>
	</tr>
	<tr>
		<td>si134</td>
		<td>Brake status 7</td>
	</tr>
	<tr>
		<td>si135</td>
		<td>Brake status 8</td>
	</tr>
	<tr>
		<td rowspan=8>sib17</td>
		<td>si136</td>
		<td>Precharge relay on</td>
	</tr>
	<tr>
		<td>si137</td>
		<td>Dynamic resistor overheat</td>
	</tr>
	<tr>
		<td>si138</td>
		<td>Over voltage</td>
	</tr>
	<tr>
		<td>si139</td>
		<td>Under voltage</td>
	</tr>
	<tr>
		<td>si140</td>
		<td>Dynamic brake status</td>
	</tr>
	<tr>
		<td>si141</td>
		<td>/SVON (Servo ON)</td>
	</tr>
	<tr>
		<td>si142</td>
		<td>Robot-fan failure</td>
	</tr>
	<tr>
		<td>si143</td>
		<td>Diode module overheat</td>
	</tr>
	<tr>
		<td rowspan=8>sib18</td>
		<td>si144</td>
		<td>User 1</td>
	</tr>
	<tr>
		<td>si145</td>
		<td>User 2</td>
	</tr>
	<tr>
		<td>si146</td>
		<td>User 3</td>
	</tr>
	<tr>
		<td>si147</td>
		<td>User 4</td>
	</tr>
	<tr>
		<td>si148</td>
		<td>User 5 (BD640T)</td>
	</tr>
	<tr>
		<td>si149</td>
		<td>User 6 (BD640T)</td>
	</tr>
	<tr>
		<td>si150</td>
		<td>User 7 (BD640T)</td>
	</tr>
	<tr>
		<td>si151</td>
		<td>User 8 (BD640T)</td>
	</tr>
	<tr>
		<td rowspan=2>sib19</td>
		<td>si152</td>
		<td>Brake power fail</td>
	</tr>
	<tr>
		<td>si153</td>
		<td>AC voltage down</td>
	</tr>
</tbody>

<tbody>
	<tr>
		<td rowspan=32>BD640T Conveyor</td>
		<td rowspan=1>sib42<br>sib43</td>
		<td></td>
		<td>ch1 - pulse counter (16bit)</td>
	</tr>
	<tr>
		<td rowspan=1>sib44<br>sib45</td>
		<td></td>
		<td>ch1 - pulse counter (16bit)</td>
	</tr>
	<tr>
		<td rowspan=4>sib46</td>
		<td>si368</td>
		<td>ch1- line error</td>
	</tr>
	<tr>
		<td>si369</td>
		<td>ch1- limit swich</td>
	</tr>
	<tr>
		<td>si370</td>
		<td>ch1- line error</td>
	</tr>
	<tr>
		<td>si371</td>
		<td>ch2- limit swich</td>
	</tr>
</tbody>

</table>
