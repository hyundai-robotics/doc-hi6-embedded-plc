# 4.1 指令列表


<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

### * 梯子和分支
<br>

<table>
<thead>
  <tr>
    <th>助记符</th>
    <th>名称</th>
    <th>符号</th>
    <th>描述</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>RUNG</td>
    <td>梯级</td>
    <td>├─┤</td>
    <td>梯级</td>
  </tr>
  <tr>
    <td>BST</td>
    <td>分支开始</td>
    <td>┬─</td>
    <td>分支的开始</td>
  </tr>
  <tr>
    <td>BND</td>
    <td>分支结束</td>
    <td>─┬</td>
    <td>分支的结束</td>
  </tr>
  <tr>
    <td>NXB</td>
    <td>嵌套分支</td>
    <td>└,├</td>
    <td>分支的嵌套</td>
  </tr>
</tbody>
</table>
### * 逻辑检查说明：如果检查结果为真，则梯级处于活动状态。如果为假，则梯级处于非活动状态。 
<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>XIC</td>
		<td>检查是否关闭</td>
		<td>-| |-</td>
		<td>检查接触点是否关闭（接触点 A）</td>
	</tr>
	<tr>
		<td>XIO</td>
		<td>检查是否打开</td>
		<td>-|/|-</td>
		<td>检查接触点是否打开（接触点 B）</td>
	</tr>
	<tr>
		<td>INV</td>
		<td>反转</td>
		<td>-//-</td>
		<td>反转梯级的结果（反转）</td>
	</tr>
	<tr>
		<td>EQU</td>
		<td>反转</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否相等 (=)</td>
	</tr>
	<tr>
		<td>NEQ</td>
		<td>反转</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否不相等 (<>)</td>
	</tr>
	<tr>
		<td>LES</td>
		<td>小于</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否小于 (<)</td>
</tr>
	<tr>
		<td>GRT</td>
		<td>大于</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否大于 (>)</td>
	</tr>
	<tr>
		<td>LEQ</td>
		<td>小于或等于</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否小于或等于 (<=)</td>
	</tr>
	<tr>
		<td>GEQ</td>
		<td>大于或等于</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>检查是否大于或等于 (>=)</td>
	</tr>
</tbody>
</table>

<br><br>  

### * 输出说明

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>OTE</td>
		<td>输出激活</td>
		<td>-( )-</td>
		<td>梯级的状态 (激活: ON/未激活: OFF) 将被输出</td>
	</tr>
	<tr>
		<td>OTL</td>
		<td>输出锁存</td>
		<td>-(L)-</td>
		<td>如果梯级是激活的，输出信号将以 ON (高) 状态输出</td>
	</tr>
<tr>
		<td>OTU</td>
		<td>输出解锁</td>
		<td>-(U)-</td>
		<td>如果梯级处于活动状态，则输出信号将以关闭（低）状态输出</td>
	</tr>
	<tr>
		<td>OSR</td>
		<td>单次上升</td>
		<td>-(OSR)-</td>
		<td>如果梯级处于活动状态，则输出信号仅在一次扫描的持续时间内以开启状态输出</td>
	</tr>
	<tr>
		<td>RES</td>
		<td>重置</td>
		<td>-(RES)-</td>
		<td>如果梯级处于活动状态，则定时器或计数器将被重置</td>
	</tr>
</tbody>
</table>



<br><br>  

### * 定时器和计数器指令

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TON</td>
		<td>定时开启延迟</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>定时器仅在梯级处于活动状态时工作</td>
	</tr>
	<tr>
		<td>CTD</td>
		<td>倒计时</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>梯级的激活（非活动 -> 活动）将被倒计时</td>
</tr>
</tbody>
</table>


<br><br>  

### * 算术操作说明

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>ADD</td>
		<td>加法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行加法 (+) 操作</td>
	</tr>
	<tr>
		<td>SUB</td>
		<td>减法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行减法 (-) 操作</td>
	</tr>
	<tr>
		<td>MUL</td>
		<td>乘法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行乘法 (x) 操作</td>
	</tr>
	<tr>
		<td>DIV</td>
		<td>除法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行除法 (/) 操作</td>
	</tr>
	<tr>
		<td>POW</td>
		<td>幂</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>在梯级活跃时进行幂 (^) 操作</td>
</tr>
	<tr>
		<td>与</td>
		<td>按位与</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，则执行按位与 (&) 操作</td>
	</tr>
	<tr>
		<td>或</td>
		<td>按位或</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，则执行按位或 (|) 操作</td>
	</tr>
</tbody>
</table>




<br><br>  

### * 数据转换说明

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>TOD</td>
		<td>将整数转换为BCD</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，则整数将被转换为BCD</td>
	</tr>
	<tr>
		<td>FRD</td>
		<td>将BCD转换为整数</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，则BCD将被转换为整数</td>
	</tr>
	<tr>
		<td>SEG</td>
		<td>7段</td>
<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于激活状态，则将转换为7段值</td>
	</tr>
</tbody>
</table>


<br><br>  

### * 移动和复制指令

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>MOV</td>
		<td>移动</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于激活状态，则将复制一条数据</td>
	</tr>
	<tr>
		<td>COP</td>
		<td>复制数据</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于激活状态，则将复制多条数据</td>
	</tr>
	<tr>
		<td>CCOP</td>
		<td>条件复制数据</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>根据梯级的状态将复制多条数据</td>
	</tr>
	<tr>
		<td>ROT</td>
		<td>旋转输出</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于激活状态，则将进行顺序输出</td>
	</tr>
</tbody>
</table>
### * 阻塞控制指令

<br>

<table>
<thead>
	<tr>
		<th>助记符</th>
		<th>名称</th>
		<th>符号</th>
		<th>描述</th>
	</tr>
</thead>
<tbody>
	<tr>
		<td>FOR</td>
		<td>FOR 循环</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，将进行重复执行，直到 Next</td>
	</tr>
	<tr>
		<td>NEXT</td>
		<td>NEXT 循环</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果计数在重复计数范围内，将跳转到 FOR 指令</td>
	</tr>
	<tr>
		<td>LBL</td>
		<td>标签</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>根据 JMP 指令指定一个跳转位置</td>
	</tr>
	<tr>
		<td>JMP</td>
		<td>跳转</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，将跳转到 LBL 位置<br>
		(如果 Label&lt;0，跳过 -n NEXTs)</td>
	</tr>
	<tr>
		<td>CALL</td>
		<td>调用</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，将调用一个子梯级</td>
	</tr>
	<tr>
		<td>END</td>
<td>结束</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯级处于活动状态，从梯子将结束</td>
	</tr>
</tbody>
</table>