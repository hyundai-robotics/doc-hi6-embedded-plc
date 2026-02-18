# 3.4.14.7 S 继电器 - EtherCAT 主状态

<style type="text/css">
table  {border-collapse:collapse;}
td {border-color:gray;border-style:solid;border-width:1px;}
.grayed {background-color:lightgray;}
.powderblued {background-color:powderblue;}
</style>


<br>

<br>

{% hint style="info" %}
\.		如果您想监控从站是否处于活动状态，请检查“IO交换中的从站列表”。
{% endhint %}

<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 EtherCAT 状态 = 1018</td>
	</tr>
	<tr>
```html
<td>2</td>
<td>1</td>
<td>参数 1</td>
<td colspan=8>插槽编号 = 1 ~ 3</td>
</tr>
<tr>
<td>3</td>
<td>1</td>
<td>参数 2</td>
<td colspan=8>已配置从站列表 = 5</td>
</tr>
<tr>
<td>4</td>
<td rowspan=16>16</td>
<td rowspan=16>从站列表</td>
<td>节点 7</td>
<td>节点 6</td>
<td>节点 5</td>
<td>节点 4</td>
<td>节点 3</td>
<td>节点 2</td>
<td>节点 1</td>
<td>节点 0</td>
</tr>
<tr>
<td>5</td>
<td>节点 15</td>
<td>节点 14</td>
<td>节点 13</td>
<td>节点 12</td>
<td>节点 11</td>
<td>节点 10</td>
<td>节点 9</td>
<td>节点 8</td>
</tr>
<tr>
<td>6</td>
<td>节点 23</td>
<td>节点 22</td>
<td>节点 21</td>
<td>节点 20</td>
<td>节点 19</td>
<td>节点 18</td>
<td>节点 17</td>
<td>节点 16</td>
</tr>
<tr>
<td>7</td>
<td>节点 31</td>
<td>节点 30</td>
```
<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
</tr>
		<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
```html
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
</tr>
<tr>
<td>17</td>
<td>节点 111</td>
<td>节点 110</td>
<td>节点 109</td>
<td>节点 108</td>
<td>节点 107</td>
<td>节点 106</td>
<td>节点 105</td>
<td>节点 104</td>
</tr>
<tr>
<td>18</td>
<td>节点 119</td>
<td>节点 118</td>
<td>节点 117</td>
<td>节点 116</td>
<td>节点 115</td>
<td>节点 114</td>
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移量</th>
<th>名称</th>
```
	<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>继电器</td>
		<td class='powderblued'>位 7</td>
		<td class='powderblued'>位 6</td>
		<td class='powderblued'>位 5</td>
		<td class='powderblued'>位 4</td>
		<td class='powderblued'>位 3</td>
		<td class='powderblued'>位 2</td>
		<td class='powderblued'>位 1</td>
		<td class='powderblued'>位 0</td>
	</tr>
	<tr>
		<td>0</td>
		<td>2</td>
		<td>命令</td>
		<td colspan=8>获取 EtherCAT 状态 = 1018</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>IO 交换中的从设备列表 = 6</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
		<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
<td>节点 42</td>
<td>节点 41</td>
<td>节点 40</td>
</tr>
<tr>
<td>10</td>
<td>节点 55</td>
<td>节点 54</td>
<td>节点 53</td>
<td>节点 52</td>
<td>节点 51</td>
<td>节点 50</td>
<td>节点 49</td>
<td>节点 48</td>
</tr>
<tr>
<td>11</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
<tr>
<td>12</td>
<td>节点 71</td>
<td>节点 70</td>
<td>节点 69</td>
<td>节点 68</td>
<td>节点 67</td>
<td>节点 66</td>
<td>节点 65</td>
<td>节点 64</td>
</tr>
<tr>
<td>13</td>
<td>节点 79</td>
<td>节点 78</td>
<td>节点 77</td>
<td>节点 76</td>
<td>节点 75</td>
<td>节点 74</td>
<td>节点 73</td>
<td>节点 72</td>
</tr>
<tr>
<td>14</td>
```html
<td>节点 87</td>
<td>节点 86</td>
<td>节点 85</td>
<td>节点 84</td>
<td>节点 83</td>
<td>节点 82</td>
<td>节点 81</td>
<td>节点 80</td>
</tr>
<tr>
<td>15</td>
<td>节点 95</td>
<td>节点 94</td>
<td>节点 93</td>
<td>节点 92</td>
<td>节点 91</td>
<td>节点 90</td>
<td>节点 89</td>
<td>节点 88</td>
</tr>
<tr>
<td>16</td>
<td>节点 103</td>
<td>节点 102</td>
<td>节点 101</td>
<td>节点 100</td>
<td>节点 99</td>
<td>节点 98</td>
<td>节点 97</td>
<td>节点 96</td>
</tr>
<tr>
<td>17</td>
<td>节点 111</td>
<td>节点 110</td>
<td>节点 109</td>
<td>节点 108</td>
<td>节点 107</td>
<td>节点 106</td>
<td>节点 105</td>
<td>节点 104</td>
</tr>
<tr>
<td>18</td>
<td>节点 119</td>
<td>节点 118</td>
<td>节点 117</td>
<td>节点 116</td>
<td>节点 115</td>
<td>节点 114</td>
```
```html
<td>节点 113</td>
<td>节点 112</td>
</tr>
<tr>
<td>19</td>
<td>节点 127</td>
<td>节点 126</td>
<td>节点 125</td>
<td>节点 124</td>
<td>节点 123</td>
<td>节点 122</td>
<td>节点 121</td>
<td>节点 120</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
<tr>
<th colspan=2>S 偏移</th>
<th>名称</th>
<th colspan=8>描述或位索引</th>
</tr>
</thead>

<tbody>
<tr>
<td class='powderblued'>开始</td>
<td class='powderblued'>大小</td>
<td class='powderblued'>继电器</td>
<td class='powderblued'>位 7</td>
<td class='powderblued'>位 6</td>
<td class='powderblued'>位 5</td>
<td class='powderblued'>位 4</td>
<td class='powderblued'>位 3</td>
<td class='powderblued'>位 2</td>
<td class='powderblued'>位 1</td>
<td class='powderblued'>位 0</td>
</tr>
<tr>
<td>0</td>
<td>2</td>
<td>command</td>
<td colspan=8>获取 EtherCAT 状态 = 1018</td>
</tr>
<tr>
```
<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>诊断从设备列表 = 7</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=16>16</td>
		<td rowspan=16>从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
		<td>节点 0</td>
	</tr>
	<tr>
		<td>5</td>
		<td>节点 15</td>
		<td>节点 14</td>
		<td>节点 13</td>
		<td>节点 12</td>
		<td>节点 11</td>
		<td>节点 10</td>
		<td>节点 9</td>
		<td>节点 8</td>
	</tr>
		<tr>
		<td>6</td>
		<td>节点 23</td>
		<td>节点 22</td>
		<td>节点 21</td>
		<td>节点 20</td>
		<td>节点 19</td>
		<td>节点 18</td>
		<td>节点 17</td>
		<td>节点 16</td>
	</tr>
		<tr>
		<td>7</td>
		<td>节点 31</td>
		<td>节点 30</td>
<td>节点 29</td>
		<td>节点 28</td>
		<td>节点 27</td>
		<td>节点 26</td>
		<td>节点 25</td>
		<td>节点 24</td>
	</tr>
		<tr>
		<td>8</td>
		<td>节点 39</td>
		<td>节点 38</td>
		<td>节点 37</td>
		<td>节点 36</td>
		<td>节点 35</td>
		<td>节点 34</td>
		<td>节点 33</td>
		<td>节点 32</td>
	</tr>
		<tr>
		<td>9</td>
		<td>节点 47</td>
		<td>节点 46</td>
		<td>节点 45</td>
		<td>节点 44</td>
		<td>节点 43</td>
		<td>节点 42</td>
		<td>节点 41</td>
		<td>节点 40</td>
	</tr>
		<tr>
		<td>10</td>
		<td>节点 55</td>
		<td>节点 54</td>
		<td>节点 53</td>
		<td>节点 52</td>
		<td>节点 51</td>
		<td>节点 50</td>
		<td>节点 49</td>
		<td>节点 48</td>
	</tr>
		<tr>
		<td>11</td>
		<td>节点 63</td>
		<td>节点 62</td>
		<td>节点 61</td>
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
</tr>
		<tr>
		<td>12</td>
		<td>节点 71</td>
		<td>节点 70</td>
		<td>节点 69</td>
		<td>节点 68</td>
		<td>节点 67</td>
		<td>节点 66</td>
		<td>节点 65</td>
		<td>节点 64</td>
	</tr>
		<tr>
		<td>13</td>
		<td>节点 79</td>
		<td>节点 78</td>
		<td>节点 77</td>
		<td>节点 76</td>
		<td>节点 75</td>
		<td>节点 74</td>
		<td>节点 73</td>
		<td>节点 72</td>
	</tr>
		<tr>
		<td>14</td>
		<td>节点 87</td>
		<td>节点 86</td>
		<td>节点 85</td>
		<td>节点 84</td>
		<td>节点 83</td>
		<td>节点 82</td>
		<td>节点 81</td>
		<td>节点 80</td>
	</tr>
		<tr>
		<td>15</td>
		<td>节点 95</td>
		<td>节点 94</td>
		<td>节点 93</td>
		<td>节点 92</td>
		<td>节点 91</td>
		<td>节点 90</td>
		<td>节点 89</td>
		<td>节点 88</td>
	</tr>
		<tr>
		<td>16</td>
		<td>节点 103</td>
		<td>节点 102</td>
		<td>节点 101</td>
<<<SOURCE_MARKDOWN_START>>>		<td>节点 100</td>
		<td>节点 99</td>
		<td>节点 98</td>
		<td>节点 97</td>
		<td>节点 96</td>
	</tr>
		<tr>
		<td>17</td>
		<td>节点 111</td>
		<td>节点 110</td>
		<td>节点 109</td>
		<td>节点 108</td>
		<td>节点 107</td>
		<td>节点 106</td>
		<td>节点 105</td>
		<td>节点 104</td>
	</tr>
		<tr>
		<td>18</td>
		<td>节点 119</td>
		<td>节点 118</td>
		<td>节点 117</td>
		<td>节点 116</td>
		<td>节点 115</td>
		<td>节点 114</td>
		<td>节点 113</td>
		<td>节点 112</td>
	</tr>
		<tr>
		<td>19</td>
		<td>节点 127</td>
		<td>节点 126</td>
		<td>节点 125</td>
		<td>节点 124</td>
		<td>节点 123</td>
		<td>节点 122</td>
		<td>节点 121</td>
		<td>节点 120</td>
	</tr>
</tbody>
</table><<<SOURCE_MARKDOWN_END>>>