# 4.3 S 릴레이

Hi6 제어기 내의 다양한 상태값이 S릴레이에 매핑되어 있습니다. 또한 일부 S릴레이에 값을 써서 Hi6의 상태를 바꿀 수 있습니다.

따라서, 공정 PLC나 PC 같은 외부 장치는 필드버스, MODBUS 등을 통해 S 릴레이 값을 읽어 Hi6 제어기의 상태를 원격 모니터링할 수 있으며, S 릴레이에 값을 써서 Hi6 제어기를 원격 제어할 수 있습니다. 


<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
</style>

<table class="tg">
<thead>
  <tr>
    <th>릴레이</th>
    <th>설명</th>
    <th>비고</th>
  </tr>
</thead>

<tbody>
  <tr>
    <td>SW3</th>
    <td>PLC실행모드<br>
    (4: PLC OFF, 5: 프로그램 없음, 0:STOP, 1:R.STOP, 2:R.RUN, 3:RUN)</td>
    <td></td>
  </tr>
  <tr>
    <td>SW5</td>
    <td>Main SW Version<br>
    HSB: MAJOR, LSB: MINOR<br>
    e.g. V60.05-08인 경우, SB?:60, SB?:5, SB?:8 @@@
    </td>
    <td></td>
  </tr>
  <tr>
    <td>SW10</td>
    <td>scan time</td>
    <td>ms</td>
  </tr>

</tbody>
</table>