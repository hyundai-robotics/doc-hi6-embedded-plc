# 3.4.14.4 S 릴레이 - Profinet IO Master 상태 릴레이

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>이름</th>
		<th colspan=8>설명 or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>시작</td>
		<td class='powderblued'>크기</td>
		<td class='powderblued'>릴레이</td>
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
		<td colspan=8>Get Profinet IO Status = 1016</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>Slot 번호 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8> 연결된 슬레이브 리스트 = 5</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>슬레이브 리스트</td>
		<td>Node 7</td>
		<td>Node 6</td>
		<td>Node 5</td>
		<td>Node 4</td>
		<td>Node 3</td>
		<td>Node 2</td>
		<td>Node 1</td>
		<td>Node 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>Node 15</td>
		<td>Node 14</td>
		<td>Node 13</td>
		<td>Node 12</td>
		<td>Node 11</td>
		<td>Node 10</td>
		<td>Node 9</td>
		<td>Node 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>Node 23</td>
		<td>Node 22</td>
		<td>Node 21</td>
		<td>Node 20</td>
		<td>Node 19</td>
		<td>Node 18</td>
		<td>Node 17</td>
		<td>Node 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>Node 31</td>
		<td>Node 30</td>
		<td>Node 29</td>
		<td>Node 28</td>
		<td>Node 27</td>
		<td>Node 26</td>
		<td>Node 25</td>
		<td>Node 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>Node 39</td>
		<td>Node 38</td>
		<td>Node 37</td>
		<td>Node 36</td>
		<td>Node 35</td>
		<td>Node 34</td>
		<td>Node 33</td>
		<td>Node 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>Node 47</td>
		<td>Node 46</td>
		<td>Node 45</td>
		<td>Node 44</td>
		<td>Node 43</td>
		<td>Node 42</td>
		<td>Node 41</td>
		<td>Node 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>Node 55</td>
		<td>Node 54</td>
		<td>Node 53</td>
		<td>Node 52</td>
		<td>Node 51</td>
		<td>Node 50</td>
		<td>Node 49</td>
		<td>Node 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>Node 63</td>
		<td>Node 62</td>
		<td>Node 61</td>
		<td>Node 60</td>
		<td>Node 59</td>
		<td>Node 58</td>
		<td>Node 57</td>
		<td>Node 56</td>
	</tr>
		<tr>
		<td>12</td>
		<td>Node 71</td>
		<td>Node 70</td>
		<td>Node 69</td>
		<td>Node 68</td>
		<td>Node 67</td>
		<td>Node 66</td>
		<td>Node 65</td>
		<td>Node 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>Node 79</td>
		<td>Node 78</td>
		<td>Node 77</td>
		<td>Node 76</td>
		<td>Node 75</td>
		<td>Node 74</td>
		<td>Node 73</td>
		<td>Node 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>Node 87</td>
		<td>Node 86</td>
		<td>Node 85</td>
		<td>Node 84</td>
		<td>Node 83</td>
		<td>Node 82</td>
		<td>Node 81</td>
		<td>Node 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>Node 95</td>
		<td>Node 94</td>
		<td>Node 93</td>
		<td>Node 92</td>
		<td>Node 91</td>
		<td>Node 90</td>
		<td>Node 89</td>
		<td>Node 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>Node 103</td>
		<td>Node 102</td>
		<td>Node 101</td>
		<td>Node 100</td>
		<td>Node 99</td>
		<td>Node 98</td>
		<td>Node 97</td>
		<td>Node 96</td>
	</tr>
		<tr>
		<td>17</td>
		<td>Node 111</td>
		<td>Node 110</td>
		<td>Node 109</td>
		<td>Node 108</td>
		<td>Node 107</td>
		<td>Node 106</td>
		<td>Node 105</td>
		<td>Node 104</td>
	</tr>
		<tr>
		<td>18</td>
		<td>Node 119</td>
		<td>Node 118</td>
		<td>Node 117</td>
		<td>Node 116</td>
		<td>Node 115</td>
		<td>Node 114</td>
		<td>Node 113</td>
		<td>Node 112</td>
	</tr>
		<tr>
		<td>19</td>
		<td>Node 127</td>
		<td>Node 126</td>
		<td>Node 125</td>
		<td>Node 124</td>
		<td>Node 123</td>
		<td>Node 122</td>
		<td>Node 121</td>
		<td>Node 120</td>
	</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>이름</th>
		<th colspan=8>설명 or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>시작</td>
		<td class='powderblued'>크기</td>
		<td class='powderblued'>릴레이</td>
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
		<td colspan=8>Get Profinet IO Status = 1016</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>Slot 번호 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>IO 교환 슬레이브 리스트 = 6</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>슬레이브 리스트</td>
		<td>Node 7</td>
		<td>Node 6</td>
		<td>Node 5</td>
		<td>Node 4</td>
		<td>Node 3</td>
		<td>Node 2</td>
		<td>Node 1</td>
		<td>Node 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>Node 15</td>
		<td>Node 14</td>
		<td>Node 13</td>
		<td>Node 12</td>
		<td>Node 11</td>
		<td>Node 10</td>
		<td>Node 9</td>
		<td>Node 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>Node 23</td>
		<td>Node 22</td>
		<td>Node 21</td>
		<td>Node 20</td>
		<td>Node 19</td>
		<td>Node 18</td>
		<td>Node 17</td>
		<td>Node 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>Node 31</td>
		<td>Node 30</td>
		<td>Node 29</td>
		<td>Node 28</td>
		<td>Node 27</td>
		<td>Node 26</td>
		<td>Node 25</td>
		<td>Node 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>Node 39</td>
		<td>Node 38</td>
		<td>Node 37</td>
		<td>Node 36</td>
		<td>Node 35</td>
		<td>Node 34</td>
		<td>Node 33</td>
		<td>Node 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>Node 47</td>
		<td>Node 46</td>
		<td>Node 45</td>
		<td>Node 44</td>
		<td>Node 43</td>
		<td>Node 42</td>
		<td>Node 41</td>
		<td>Node 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>Node 55</td>
		<td>Node 54</td>
		<td>Node 53</td>
		<td>Node 52</td>
		<td>Node 51</td>
		<td>Node 50</td>
		<td>Node 49</td>
		<td>Node 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>Node 63</td>
		<td>Node 62</td>
		<td>Node 61</td>
		<td>Node 60</td>
		<td>Node 59</td>
		<td>Node 58</td>
		<td>Node 57</td>
		<td>Node 56</td>
	</tr>
		<tr>
		<td>12</td>
		<td>Node 71</td>
		<td>Node 70</td>
		<td>Node 69</td>
		<td>Node 68</td>
		<td>Node 67</td>
		<td>Node 66</td>
		<td>Node 65</td>
		<td>Node 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>Node 79</td>
		<td>Node 78</td>
		<td>Node 77</td>
		<td>Node 76</td>
		<td>Node 75</td>
		<td>Node 74</td>
		<td>Node 73</td>
		<td>Node 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>Node 87</td>
		<td>Node 86</td>
		<td>Node 85</td>
		<td>Node 84</td>
		<td>Node 83</td>
		<td>Node 82</td>
		<td>Node 81</td>
		<td>Node 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>Node 95</td>
		<td>Node 94</td>
		<td>Node 93</td>
		<td>Node 92</td>
		<td>Node 91</td>
		<td>Node 90</td>
		<td>Node 89</td>
		<td>Node 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>Node 103</td>
		<td>Node 102</td>
		<td>Node 101</td>
		<td>Node 100</td>
		<td>Node 99</td>
		<td>Node 98</td>
		<td>Node 97</td>
		<td>Node 96</td>
	</tr>
		<tr>
		<td>17</td>
		<td>Node 111</td>
		<td>Node 110</td>
		<td>Node 109</td>
		<td>Node 108</td>
		<td>Node 107</td>
		<td>Node 106</td>
		<td>Node 105</td>
		<td>Node 104</td>
	</tr>
		<tr>
		<td>18</td>
		<td>Node 119</td>
		<td>Node 118</td>
		<td>Node 117</td>
		<td>Node 116</td>
		<td>Node 115</td>
		<td>Node 114</td>
		<td>Node 113</td>
		<td>Node 112</td>
	</tr>
		<tr>
		<td>19</td>
		<td>Node 127</td>
		<td>Node 126</td>
		<td>Node 125</td>
		<td>Node 124</td>
		<td>Node 123</td>
		<td>Node 122</td>
		<td>Node 121</td>
		<td>Node 120</td>
	</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S Offset</th>
		<th>이름</th>
		<th colspan=8>설명 or Bit Index</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>시작</td>
		<td class='powderblued'>크기</td>
		<td class='powderblued'>릴레이</td>
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
		<td colspan=8>Get Profinet IO Status = 1016</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>Slot 번호 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>진단 슬레이브 리스트 = 7</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>슬레이브 리스트</td>
		<td>Node 7</td>
		<td>Node 6</td>
		<td>Node 5</td>
		<td>Node 4</td>
		<td>Node 3</td>
		<td>Node 2</td>
		<td>Node 1</td>
		<td>Node 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>Node 15</td>
		<td>Node 14</td>
		<td>Node 13</td>
		<td>Node 12</td>
		<td>Node 11</td>
		<td>Node 10</td>
		<td>Node 9</td>
		<td>Node 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>Node 23</td>
		<td>Node 22</td>
		<td>Node 21</td>
		<td>Node 20</td>
		<td>Node 19</td>
		<td>Node 18</td>
		<td>Node 17</td>
		<td>Node 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>Node 31</td>
		<td>Node 30</td>
		<td>Node 29</td>
		<td>Node 28</td>
		<td>Node 27</td>
		<td>Node 26</td>
		<td>Node 25</td>
		<td>Node 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>Node 39</td>
		<td>Node 38</td>
		<td>Node 37</td>
		<td>Node 36</td>
		<td>Node 35</td>
		<td>Node 34</td>
		<td>Node 33</td>
		<td>Node 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>Node 47</td>
		<td>Node 46</td>
		<td>Node 45</td>
		<td>Node 44</td>
		<td>Node 43</td>
		<td>Node 42</td>
		<td>Node 41</td>
		<td>Node 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>Node 55</td>
		<td>Node 54</td>
		<td>Node 53</td>
		<td>Node 52</td>
		<td>Node 51</td>
		<td>Node 50</td>
		<td>Node 49</td>
		<td>Node 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>Node 63</td>
		<td>Node 62</td>
		<td>Node 61</td>
		<td>Node 60</td>
		<td>Node 59</td>
		<td>Node 58</td>
		<td>Node 57</td>
		<td>Node 56</td>
	</tr>
		<tr>
		<td>12</td>
		<td>Node 71</td>
		<td>Node 70</td>
		<td>Node 69</td>
		<td>Node 68</td>
		<td>Node 67</td>
		<td>Node 66</td>
		<td>Node 65</td>
		<td>Node 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>Node 79</td>
		<td>Node 78</td>
		<td>Node 77</td>
		<td>Node 76</td>
		<td>Node 75</td>
		<td>Node 74</td>
		<td>Node 73</td>
		<td>Node 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>Node 87</td>
		<td>Node 86</td>
		<td>Node 85</td>
		<td>Node 84</td>
		<td>Node 83</td>
		<td>Node 82</td>
		<td>Node 81</td>
		<td>Node 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>Node 95</td>
		<td>Node 94</td>
		<td>Node 93</td>
		<td>Node 92</td>
		<td>Node 91</td>
		<td>Node 90</td>
		<td>Node 89</td>
		<td>Node 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>Node 103</td>
		<td>Node 102</td>
		<td>Node 101</td>
		<td>Node 100</td>
		<td>Node 99</td>
		<td>Node 98</td>
		<td>Node 97</td>
		<td>Node 96</td>
	</tr>
		<tr>
		<td>17</td>
		<td>Node 111</td>
		<td>Node 110</td>
		<td>Node 109</td>
		<td>Node 108</td>
		<td>Node 107</td>
		<td>Node 106</td>
		<td>Node 105</td>
		<td>Node 104</td>
	</tr>
		<tr>
		<td>18</td>
		<td>Node 119</td>
		<td>Node 118</td>
		<td>Node 117</td>
		<td>Node 116</td>
		<td>Node 115</td>
		<td>Node 114</td>
		<td>Node 113</td>
		<td>Node 112</td>
	</tr>
		<tr>
		<td>19</td>
		<td>Node 127</td>
		<td>Node 126</td>
		<td>Node 125</td>
		<td>Node 124</td>
		<td>Node 123</td>
		<td>Node 122</td>
		<td>Node 121</td>
		<td>Node 120</td>
	</tr>
</tbody>
</table>