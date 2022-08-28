# 5. 명령 (instruction)


래더 프로그램은 다수의 rung으로 구성되며, 각 rung은 다수의 명령들로 구성됩니다.

내장 PLC는 프로그램 내의 명령들을 순차적으로 수행하면서 논리적인 I/O 동작을 수행합니다.

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.tg-kftd{background-color:#efefef;}
</style>

<table>
<thead>
  <tr>
    <td rowspan="11">래더 프로젝트</td>
    <td rowspan="7">래더 프로그램</td>
    <td rowspan="3">rung</td>
    <td>명령</td>
  </tr>
  <tr>
    <td>명령</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">rung</td>
    <td>명령</td>
  </tr>
  <tr>
    <td>명령</td>
  </tr>
  <tr>
    <td>...</td>
  </tr>
  <tr>
    <td>...</td>
    <td>...</td>
  </tr>
  <tr>
    <td rowspan="3">래더 프로그램</td>
    <td rowspan="2">rung</td>
    <td>명령</td>
  </tr>
  <tr>
    <td>명령</td>
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
</thead>
</table>

<br><br>

명령은 아래와 같이 3가지 요소로 구성됩니다.

<table>
<thead>
  <tr>
    <th>명령어 (mnemonic)</th>
    <th>동작의 종류</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>오퍼랜드 (operand)</td>
    <td>동작의 인수.<br>명령어에 따라 오퍼랜드가 1개나 여러개가 지정되며, 오퍼랜드가 없는 명령어도 있습니다.</td>
  </tr>
  <tr>
    <td>주석</td>
    <td>프로그램의 가독성을 위해 붙이는 설명. 동작에는 영향을 주지 않습니다.</td>
  </tr>
</tbody>
</table>


