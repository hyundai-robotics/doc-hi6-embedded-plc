# 3.4.14.2 S relay - CIFX PCI Communication Control

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>

<br>

#### Supported version: TBD 

<br>


<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>Name</th>
		<th colspan=8>Description or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>Start</td>
		<td class='powderblued'>Size</td>
		<td class='powderblued'>Relay</td>
		<td class='powderblued'>Bit 7</td>
		<td class='powderblued'>Bit 6</td>
		<td class='powderblued'>Bit 5</td>
		<td class='powderblued'>Bit 4</td>
		<td class='powderblued'>Bit 3</td>
		<td class='powderblued'>Bit 2</td>
		<td class='powderblued'>Bit 1</td>
		<td class='powderblued'>Bit 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>command</td>
		<td colspan=8>Get CIFX Control = 1001</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>Slot Number = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>Control Group = 1</td>
	</tr>
	<tr>
		<td>4</td>
		<td>1</td>
		<td>Communication Reset</td>
		<td colspan=8>Reset when the signal changes 0 -> 1 </td>
	</tr>
	<tr>
		<td>5</td>
		<td>1</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>6</td>
		<td>1</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>7</td>
		<td>1</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>8</td>
		<td>2</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>10</td>
		<td>2</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
	<tr>
		<td>12</td>
		<td>8</td>
		<td>Reserved</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>
