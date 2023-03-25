# 4.30 FOR(FOR) : 블록 반복


### 설명
Rung이 활성이면, NEXT까지의 블록을 "init"부터 "final"까지 "idx" 릴레이 값을 "step"씩 증가하면서 반복 실행합니다.  
FOR문을 실행할 때 무조건 "idx" 릴레이에 "init"값을 대입합니다.  
FOR/NEXT문은 최대 10개까지 중첩시킬 수 있습니다. → FOR() FOR() FOR() ….NEXT NEXT NEXT  
"step"이 0보다 큰 경우, "init" 값이 "final" 값보다 크면 실행하지 않고 NEXT로 Jump합니다.  
"step"이 0보다 작은 경우, "init" 값이 "final" 값보다 작으면 실행하지 않고 NEXT로 Jump합니다.  
"final"과 "step"은 변수로 지정해도 FOR문을 처음 시작할 때의 값만을 사용합니다.  
특수하게 FOR문의 중간에서 빠져나가고자 할 때에는 뒤에서 설명할 JMP(음수)명령을 사용할 수 있습니다. (JMP명령설명 참조)   
주의) FOR명령은 브랜치를 위한 별도의 처리를 하지 않습니다.  
참고) NEXT 명령에 대한 내용은 [4.31 NEXT(NEXT)](./31-next)를 참조하십시오.

<br>

### 오퍼랜드로 사용할 수 있는 type
(X는 불가)
<style type="text/css">
table  {border-collapse:collapse;}
th {background-color:#efefef; border-style:solid;border-width:1px;color:black;text-align:center;}
td {border-color:gray;border-style:solid;border-width:1px;text-align:center;}
.hd{background-color:#efefef;color:black;font-weight:bold;}
</style>

<table>
<thead>
  <tr>
    <th>relay type</th>
    <th colspan="2">input<br>X, DO</th>
    <th colspan="2">output<br>Y, DI, R, K</th>
    <th colspan="2">memory<br>M, S</th>
    <th>const.<br>32bit</th>
  </tr>
  <tr>
    <th>data-type</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>bit</th>
    <th>B,W,L,F</th>
    <th>L,F</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class='hd'>idx</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>initial</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>final</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>step</td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td>X</td>
    <td></td>
    <td></td>
  </tr>
</tbody>
</table>

<br>

### 사용 예

SW62에 1부터 4까지 1씩 증가하면서 {XIC(DO-2), OTL(Y-2)}명령을 반복 실행 합니다.  
즉, "idx"가 상대어드레싱(SW62~SW79)을 위한 릴레이를 사용하고 있고, 그 XIC의 DO릴레이와 OTL의 Y릴레이가 “-2”이므로 SW62의 값에 있는 번호가 적용되기 때문에, DO1~DO4중 High인 신호번호에 해당하는 Y릴레이 번호만 High로 출력하고 입력되지 않는 번호의 Y출력은 이전상태를 유지합니다.  
참고) 상대어드레싱이란 어떤 형식의 릴레이든지 그 번지를 -2~-9값으로 설정하면 SW62~SW79에 저장된 값으로 릴레이 번지가 지정되는 방식을 말합니다.


![](../_assets/for.png)
