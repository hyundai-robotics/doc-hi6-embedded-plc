# 3.4.14.4 S 继电器 - DeviceNet 主状态

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
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
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
<td>参数. 2</td>
<td colspan=8>状态  = 1</td>
</tr>
<tr>
<td>4</td>
<td>1</td>
<td>全球位 <br> (Profibus 主控)</td>
<td>检查重复的 MAC ID</td>
<td>重复的 MAC ID</td>
<td>主机未准备好</td>
<td>总线事件错误</td>
<td>致命错误</td>
<td>非交换错误</td>
<td>自动清除错误</td>
<td>控制错误</td>
</tr>
<tr>
<td>5</td>
<td>1</td>
<td>主控状态</td>
<td colspan=8>0x00 = 离线, <br> 0x40 = 停止, <br> 0x80 = 空闲, <br> 0xC0 = 运行</td>
</tr>
<tr>
<td>6</td>
<td>1</td>
<td>错误站地址</td>
<td colspan=8></td>
</tr>
<tr>
<td>7</td>
<td>1</td>
<td>错误代码</td>
<td colspan=8>DeviceNet 主控仅 <br> 52 = 未知过程数据握手模式, <br> 53 = 波特率错误, <br> 54 = MAC ID 错误, <br> 57 = 重复的 MAC ID, <br> 58 = 无设备, <br> 210 = 无配置, <br> 212 = 读取配置失败, <br> 220 = 用户看门狗失败, <br> 221 = 用户数据无响应, <br> 223 = 主控停止 (CAN 总线关闭), <br> 226 = 设备不是主控</td>
</tr>
<tr>
<td>8</td>
<td>2</td>
<td>总线数据事务错误计数</td>
<td colspan=8></td>
</tr>
<tr>
<td>10</td>
<td>2</td>
<td>总线关闭错误计数</td>
<td colspan=8></td>
</tr>
<tr>
<td>12</td>
<td>4</td>
<td>总线错误代码</td>
<td colspan=8></td>
	</tr>
	<tr>
		<td>16</td>
		<td>4</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>

	
<br>

{% hint style="info" %}
\.		如果您想监视从设备是否处于活动状态，请检查“IO交换中的从设备列表”。
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
		<td colspan=8>获取设备网络状态 = 1012</td>
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
		<td colspan=8>已激活 / 未激活从站列表 = 2</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>已激活从站列表</td>
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
```html
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
```
<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td rowspan=8>8</td>
		<td rowspan=8>停用从属设备列表</td>
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
		<td>13</td>
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
		<td>14</td>
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
		<td>15</td>
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
		<td>16</td>
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
<td>17</td>
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
<td>18</td>
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
<td>19</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
```html
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
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>param. 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>param. 2</td>
		<td colspan=8>从设备列表（显式消息 / IO 交换） = 3</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>激活显式消息的从设备列表</td>
		<td>节点 7</td>
		<td>节点 6</td>
		<td>节点 5</td>
		<td>节点 4</td>
		<td>节点 3</td>
		<td>节点 2</td>
		<td>节点 1</td>
```
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
<td rowspan=8>8</td>
<td rowspan=8>IO 交换中的从属设备列表</td>
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
<td>13</td>
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
		<td>14</td>
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
		<td>15</td>
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
		<td>16</td>
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
		<td>17</td>
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
		<td>18</td>
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
<td>19</td>
<td>节点 63</td>
<td>节点 62</td>
<td>节点 61</td>
<td>节点 60</td>
<td>节点 59</td>
<td>节点 58</td>
<td>节点 57</td>
<td>节点 56</td>
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
		<td>命令</td>
		<td colspan=8>获取设备网络状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>诊断从站列表 = 4</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>从站列表</td>
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
```html
		<td>节点 60</td>
		<td>节点 59</td>
		<td>节点 58</td>
		<td>节点 57</td>
		<td>节点 56</td>
	</tr>
	<tr>
		<td>12</td>
		<td>8</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移量</th>
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
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
```
```html
		<td>参数 1</td>
		<td colspan=8>插槽编号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>已配置从属设备列表 = 5</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>从设备列表</td>
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
```
```html
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
```
```html
<td>12</td>
<td>8</td>
<td>保留</td>
<td colspan=8></td>
</tr>
</tbody>
</table>


<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移量</th>
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
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
```
<td colspan=8>已激活从属设备列表 = 6</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>从属设备列表</td>
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
		<td>8</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>
<br>

<table class="tg">
<thead>
	<tr>
		<th colspan=2>S 偏移量</th>
		<th>名称</th>
		<th colspan=8>描述或位索引</th>
	</tr>
</thead>

<tbody>
	<tr>
		<td class='powderblued'>开始</td>
		<td class='powderblued'>大小</td>
		<td class='powderblued'>中继</td>
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
		<td colspan=8>获取 DeviceNet 状态 = 1012</td>
	</tr>
	<tr>
		<td>2</td>
		<td>1</td>
		<td>参数 1</td>
		<td colspan=8>插槽号 = 1 ~ 3</td>
	</tr>
	<tr>
		<td>3</td>
		<td>1</td>
		<td>参数 2</td>
		<td colspan=8>诊断列表 = 7</td>
	</tr>
	<tr>
		<td>4</td>
		<td rowspan=8>8</td>
		<td rowspan=8>从设备列表</td>
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
		<td>8</td>
		<td>保留</td>
		<td colspan=8></td>
	</tr>
</tbody>
</table>