# 4.24 FRD(Convert from BCD to Integer) : integer로 변환


### 설명
Rung이 활성이면, "source"의 BCD값을 integer로 변환하여 "destination"에 저장합니다.  
이 명령은 BCD형태로 출력되는 캠 스위치의 값을 입력으로 받아드리는 경우에 편리하게 사용할 수 있습니다.  
만일, "source"의 값이 BCD가 아닌 경우에는 S6=1로 설정합니다.
또한, "source"가 워드(W) 형식이고, "destination"이 바이트(B) 형식인 경우, 변환할 "source"의 최대값은 &H9999이므로 integer의 변환결과가 9999(&H270F)로 되어 바이트의 범위 &Hff를 초과하므로 오버플로우가 발생하게 되며, 이 경우에는 S6=1로 설정합니다.

<br>

### 오퍼랜드로 사용할 수 있는 type
(X는 불가, u는 부호없는 정수)
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
    <td class='hd'>source</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>u</td>
  </tr>
</tbody>
<tbody>
  <tr>
    <td class='hd'>destination</td>
    <td>X</td>
    <td>X</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
    <td>u</td>
    <td>X</td>
  </tr>
</tbody>
</table>

<br>

### 사용 예

입력 DO43이 활성화 되면 XB3의 값(BCD)을 integer로 변환하여 그 결과를 내부 상태 MB3에 설정합니다.  
만일 &H23(35)을 integer로 변환하면 &H17(23)이 됩니다.


![](../_assets/frd.png)
