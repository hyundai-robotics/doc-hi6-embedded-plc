# 4.1 指令列表


<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

### * 梯子和分支

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
    <td>梯子</td>
    <td>├─┤</td>
    <td>梯子</td>
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

### * 逻辑检查指令：如果检查结果为真，则梯子处于活动状态。如果为假，则梯子处于非活动状态。 

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
		<td>检查接触是否关闭（接触A）</td>
	</tr>
	<tr>
		<td>XIO</td>
		<td>检查是否打开</td>
		<td>-|/|-</td>
		<td>检查接触是否打开（接触B）</td>
	</tr>
	<tr>
		<td>INV</td>
		<td>反转</td>
		<td>-//-</td>
		<td>反转梯子的结果（反转）</td>
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

<div class="page-break"></div>

### * 输出指令

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
		<td>梯子的状态（活动：ON/非活动：OFF）将被输出</td>
	</tr>
	<tr>
		<td>OTL</td>
		<td>输出保持</td>
		<td>-(L)-</td>
		<td>如果梯子处于活动状态，则输出信号将以ON（高）状态输出</td>
	</tr>
	<tr>
		<td>OTU</td>
		<td>输出释放</td>
		<td>-(U)-</td>
		<td>如果梯子处于活动状态，则输出信号将以OFF（低）状态输出</td>
	</tr>
	<tr>
		<td>OSR</td>
		<td>单次上升</td>
		<td>-(OSR)-</td>
		<td>如果梯子处于活动状态，则输出信号将在一次扫描的持续时间内仅输出为ON状态</td>
	</tr>
	<tr>
		<td>RES</td>
		<td>重置</td>
		<td>-(RES)-</td>
		<td>如果梯子处于活动状态，则计时器或计数器将被重置</td>
	</tr>
</tbody>
</table>

### * 计时器和计数器指令

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
		<td>开机延迟时间</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>计时器仅在梯子处于活动状态时工作</td>
	</tr>
	<tr>
		<td>CTD</td>
		<td>倒计时</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>梯子的激活（非活动 -> 活动）将被倒计时</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

### * 算术运算指令

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
		<td>如果梯子处于活动状态，则进行加法 (+) 操作</td>
	</tr>
	<tr>
		<td>SUB</td>
		<td>减法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行减法 (-) 操作</td>
	</tr>
	<tr>
		<td>MUL</td>
		<td>乘法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行乘法 (x) 操作</td>
	</tr>
	<tr>
		<td>DIV</td>
		<td>除法</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行除法 (/) 操作</td>
	</tr>
	<tr>
		<td>POW</td>
		<td>幂</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行幂 (^) 操作</td>
	</tr>
	<tr>
		<td>AND</td>
		<td>按位与</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行按位与 (&) 操作</td>
	</tr>
	<tr>
		<td>OR</td>
		<td>按位或</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则进行按位或 (|) 操作</td>
	</tr>
</tbody>
</table>

### * 数据转换指令

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
		<td>如果梯子处于活动状态，则整数将被转换为BCD</td>
	</tr>
	<tr>
		<td>FRD</td>
		<td>将BCD转换为整数</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，则BCD将被转换为整数</td>
	</tr>
	<tr>
		<td>SEG</td>
		<td>7段</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将进行7段值的转换</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

### * 移动和复制指令

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
		<td>如果梯子处于活动状态，将复制一条数据</td>
	</tr>
	<tr>
		<td>COP</td>
		<td>复制数据</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将复制多条数据</td>
	</tr>
	<tr>
		<td>CCOP</td>
		<td>条件复制数据</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>根据梯子的状态，将复制多条数据</td>
	</tr>
	<tr>
		<td>ROT</td>
		<td>旋转输出</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将进行顺序输出</td>
	</tr>
</tbody>
</table>

<div class="page-break"></div>

### * 块控制指令

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
		<td>如果梯子处于活动状态，将发生重复执行直到Next</td>
	</tr>
	<tr>
		<td>NEXT</td>
		<td>NEXT 循环</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果计数在重复次数内，将跳转到FOR指令</td>
	</tr>
	<tr>
		<td>LBL</td>
		<td>标签</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>根据JMP指令，指定跳转的位置</td>
	</tr>
	<tr>
		<td>JMP</td>
		<td>跳跃</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将跳转到LBL位置<br>
		（如果Label&lt;0，将跳过-n NEXTs）</td>
	</tr>
	<tr>
		<td>CALL</td>
		<td>调用</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，将调用子梯子</td>
	</tr>
	<tr>
		<td>END</td>
		<td>结束</td>
		<td>-[&nbsp;&nbsp;&nbsp;]-</td>
		<td>如果梯子处于活动状态，子梯子将结束</td>
	</tr>
</tbody>
</table>