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
</table>