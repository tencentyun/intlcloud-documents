## 测试说明
### 测试方法
采用业界通用的第三方网络应用性能监控测速方法，测试服务提供商为北京博睿宏远数据。

### 测试参数
<table style="width: 80%;display: table;margin-bottom:40px;">
	<tbody>
		<tr>
			<th scope="row" style="width:102px">测试时间</th> 
			<td style="width:385px"> 2018/05/24 00:00 - 2018/05/30 20:00 </td> 
		</tr>
		<tr>
			<th scope="row" style="width:102px">客户端地址</th> 
			<td style="width:385px"> 中国香港、新加坡、马来西亚等地区和国家 </td> 
		</tr>
		<tr>
			<th scope="row" style="width:102px">源站地址</th> 
			<td style="width:385px"> 美国弗吉尼亚 IDC 机房 </td>
		</tr>
		<tr>
			<th scope="row" style="width:102px">测试链接</th> 
			<td style="width:385px"> https://****/**/GetPage?PageId=7141974606000205</td>
		</tr>
		<tr>
			<th scope="row" style="width:102px">对比方式</th> 
			<td style="width:385px"> 测试使用同一个测试链接，分别通过设置 host IP 和 CNAME 解析的方式，对比直接访问源站和使用 ECDN 加速的访问效果</td>
		</tr>
	</tbody>
</table>

## 测试结果

### 性能曲线

![](https://main.qcloudimg.com/raw/b0825a24b98665637335aa8d672bec51.png)

### 可用性曲线

![](https://main.qcloudimg.com/raw/af8c79e78a2d7b6fc906491804d69511.png)

> **总结说明**  
>1、使用全站加速后，产品平均访问性能提升**104.71%**，页面加载性能改善明显；  
>2、在跨国访问场景下，传统公网访问受网络丢包和长延时的影响，访问稳定性波动较大，使用 ECDN 全站加速后，页面访问的**可用性和稳定性**提升明显。

### 数据汇总分析

<table style="display:table;">
	<tbody>
		<tr>
			<th rowspan="2" style="text-align: center;width: 100px;"> 监测任务 </th>
			<th colspan="3" style="text-align: center"> 性能(秒) </th>
			<th colspan="3" style="text-align: center"> 可用性(%) </th>
			<th colspan="2" style="text-align: center"> 监测次数 </th>
		</tr>
		<tr>
			<th style="text-align: center; width: 70px;"> 均值 </th>
			<th colspan="1" style="text-align: center; width: 70px;"> 最好 </th>
			<th colspan="1" style="text-align: center; width: 70px;"> 最差 </th>
			<th style="text-align: center; width: 70px;"> 均值 </th>
			<th colspan="1" style="text-align: center; width: 70px;"> 最好 </th>
			<th colspan="1" style="text-align: center; width: 70px;"> 最差 </th>
			<th colspan="1" style="text-align: center; width: 70px;"> 错误点数 </th>
			<th colspan="1" style="text-align: center; width: 70px;"> 监测总数 </th>
		</tr>
		<tr>
			<td style="width: 58px; text-align: center;"> ECDN 加速访问 </td>
			<td style="text-align: center; width: 43px;"> 0.637 </td>
			<td style="text-align: center; width: 38px;"> 0.337 </td>
			<td style="text-align: center; width: 51px;"> 1.440 </td>
			<td style="text-align: center; width: 45px;"> 99.93 </td>
			<td style="text-align: center; width: 43px;"> 100.00 </td>
			<td style="text-align: center; width: 43px;"> 98.44 </td>
			<td style="text-align: center; width: 43px;"> 7 </td>
			<td style="text-align: center; width: 43px;"> 10694 </td>
		</tr>
		<tr>
			<td style="width: 58px; text-align: center;"> 直接访问源站 </td>
			<td style="text-align: center; width: 43px;"> 1.304 </td>
			<td style="text-align: center; width: 38px;"> 0.989 </td>
			<td style="text-align: center; width: 51px;"> 2.872 </td>
			<td style="text-align: center; width: 45px;"> 98.37 </td>
			<td style="text-align: center; width: 43px;"> 100.00 </td>
			<td style="text-align: center; width: 43px;"> 93.55 </td>
			<td style="text-align: center; width: 43px;"> 173 </td>
			<td style="text-align: center; width: 43px;"> 10620  </td>
		</tr>
	</tbody>
</table>

### 数据明细

<table  style="display: table;">
	<tbody>
		<tr>
			<th rowspan="2" style="text-align: center; width: 150px;"> 时间 </th>
			<th colspan="3" style="text-align: center; width: 270px;"> ECDN 加速访问 </th>
			<th colspan="3" style="text-align: center; width: 270px;"> 直接访问源站 </th>
		</tr>
		<tr>
			<th style="text-align: center; width: 90px;"> 性能(秒) </th>
			<th style="text-align: center; width: 90px;"> 可用性(%) </th>
			<th style="text-align: center; width: 90px;"> 监测点数 </th>
			<th style="text-align: center; width: 90px;"> 性能(秒) </th>
			<th style="text-align: center; width: 90px;"> 可用性(%) </th>
			<th style="text-align: center; width: 90px;"> 监测点数 </th>
		</tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 01:00</td>
      <td style="text-align: center;">0.583</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.287</td>
      <td style="text-align: center;">98.39</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 03:00</td>
      <td style="text-align: center;">0.622</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.454</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 05:00</td>
      <td style="text-align: center;">0.648</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.256</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">108</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 07:00</td>
      <td style="text-align: center;">0.664</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.241</td>
      <td style="text-align: center;">98.33</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 09:00</td>
      <td style="text-align: center;">0.586</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.159</td>
      <td style="text-align: center;">96.77</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 11:00</td>
      <td style="text-align: center;">0.614</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.319</td>
      <td style="text-align: center;">97.41</td>
      <td style="text-align: center;">116</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 13:00</td>
      <td style="text-align: center;">0.696</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.335</td>
      <td style="text-align: center;">98.39</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 15:00</td>
      <td style="text-align: center;">0.621</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">116</td>
      <td style="text-align: center;">1.152</td>
      <td style="text-align: center;">97.58</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 17:00</td>
      <td style="text-align: center;">0.547</td>
      <td style="text-align: center;">98.44</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.181</td>
      <td style="text-align: center;">98.33</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 19:00</td>
      <td style="text-align: center;">0.723</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.302</td>
      <td style="text-align: center;">95.31</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 21:00</td>
      <td style="text-align: center;">0.693</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.209</td>
      <td style="text-align: center;">99.19</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月24日 23:00</td>
      <td style="text-align: center;">0.734</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.257</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 01:00</td>
      <td style="text-align: center;">0.589</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.254</td>
      <td style="text-align: center;">98.44</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 03:00</td>
      <td style="text-align: center;">0.636</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">144</td>
      <td style="text-align: center;">1.277</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 05:00</td>
      <td style="text-align: center;">0.578</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.262</td>
      <td style="text-align: center;">99.17</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 07:00</td>
      <td style="text-align: center;">0.606</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">116</td>
      <td style="text-align: center;">1.343</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 09:00</td>
      <td style="text-align: center;">0.706</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.305</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 11:00</td>
      <td style="text-align: center;">0.563</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.253</td>
      <td style="text-align: center;">99.22</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 13:00</td>
      <td style="text-align: center;">0.701</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.255</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 15:00</td>
      <td style="text-align: center;">0.624</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.277</td>
      <td style="text-align: center;">97.66</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 17:00</td>
      <td style="text-align: center;">0.698</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.359</td>
      <td style="text-align: center;">96.09</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 19:00</td>
      <td style="text-align: center;">0.697</td>
      <td style="text-align: center;">99.11</td>
      <td style="text-align: center;">112</td>
      <td style="text-align: center;">1.160</td>
      <td style="text-align: center;">96.77</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 21:00</td>
      <td style="text-align: center;">0.744</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.312</td>
      <td style="text-align: center;">96.43</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月25日 23:00</td>
      <td style="text-align: center;">0.711</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.284</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 01:00</td>
      <td style="text-align: center;">0.643</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.316</td>
      <td style="text-align: center;">99.22</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 03:00</td>
      <td style="text-align: center;">0.683</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.248</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 05:00</td>
      <td style="text-align: center;">0.596</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.307</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 07:00</td>
      <td style="text-align: center;">0.678</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.258</td>
      <td style="text-align: center;">97.66</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 09:00</td>
      <td style="text-align: center;">0.709</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.298</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 11:00</td>
      <td style="text-align: center;">0.601</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.315</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 13:00</td>
      <td style="text-align: center;">0.553</td>
      <td style="text-align: center;">98.57</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.195</td>
      <td style="text-align: center;">97.66</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 15:00</td>
      <td style="text-align: center;">0.583</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.153</td>
      <td style="text-align: center;">97.41</td>
      <td style="text-align: center;">116</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 17:00</td>
      <td style="text-align: center;">0.658</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.414</td>
      <td style="text-align: center;">98.53</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 19:00</td>
      <td style="text-align: center;">0.768</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.430</td>
      <td style="text-align: center;">96.32</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 21:00</td>
      <td style="text-align: center;">0.603</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.285</td>
      <td style="text-align: center;">98.48</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月26日 23:00</td>
      <td style="text-align: center;">0.792</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.218</td>
      <td style="text-align: center;">97.58</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 01:00</td>
      <td style="text-align: center;">0.659</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.249</td>
      <td style="text-align: center;">98.48</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 03:00</td>
      <td style="text-align: center;">0.667</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.310</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 05:00</td>
      <td style="text-align: center;">0.617</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.396</td>
      <td style="text-align: center;">97.73</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 07:00</td>
      <td style="text-align: center;">0.627</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.374</td>
      <td style="text-align: center;">98.48</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 09:00</td>
      <td style="text-align: center;">0.580</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.399</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 11:00</td>
      <td style="text-align: center;">0.600</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.317</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 13:00</td>
      <td style="text-align: center;">0.661</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.420</td>
      <td style="text-align: center;">96.97</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 15:00</td>
      <td style="text-align: center;">0.668</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.463</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 17:00</td>
      <td style="text-align: center;">0.544</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.233</td>
      <td style="text-align: center;">93.97</td>
      <td style="text-align: center;">116</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 19:00</td>
      <td style="text-align: center;">0.722</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.374</td>
      <td style="text-align: center;">97.14</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 21:00</td>
      <td style="text-align: center;">0.764</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">116</td>
      <td style="text-align: center;">1.281</td>
      <td style="text-align: center;">93.55</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月27日 23:00</td>
      <td style="text-align: center;">0.686</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.272</td>
      <td style="text-align: center;">93.94</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 01:00</td>
      <td style="text-align: center;">0.666</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.473</td>
      <td style="text-align: center;">97.79</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 03:00</td>
      <td style="text-align: center;">0.603</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.297</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 05:00</td>
      <td style="text-align: center;">0.549</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.467</td>
      <td style="text-align: center;">99.29</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 07:00</td>
      <td style="text-align: center;">0.589</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.312</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 09:00</td>
      <td style="text-align: center;">0.601</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.415</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 11:00</td>
      <td style="text-align: center;">0.602</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.263</td>
      <td style="text-align: center;">99.17</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 13:00</td>
      <td style="text-align: center;">0.613</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.372</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 15:00</td>
      <td style="text-align: center;">0.663</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">122</td>
      <td style="text-align: center;">1.531</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 17:00</td>
      <td style="text-align: center;">0.576</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.309</td>
      <td style="text-align: center;">98.53</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 19:00</td>
      <td style="text-align: center;">0.614</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.290</td>
      <td style="text-align: center;">95.00</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 21:00</td>
      <td style="text-align: center;">0.583</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.275</td>
      <td style="text-align: center;">95.00</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月28日 23:00</td>
      <td style="text-align: center;">0.674</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.239</td>
      <td style="text-align: center;">99.26</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 01:00</td>
      <td style="text-align: center;">0.657</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.503</td>
      <td style="text-align: center;">99.29</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 03:00</td>
      <td style="text-align: center;">0.565</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.469</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 05:00</td>
      <td style="text-align: center;">0.544</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.162</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 07:00</td>
      <td style="text-align: center;">0.579</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.343</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 09:00</td>
      <td style="text-align: center;">0.567</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.310</td>
      <td style="text-align: center;">98.39</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 11:00</td>
      <td style="text-align: center;">0.585</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.262</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 13:00</td>
      <td style="text-align: center;">0.606</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.309</td>
      <td style="text-align: center;">97.86</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 15:00</td>
      <td style="text-align: center;">0.655</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">144</td>
      <td style="text-align: center;">1.253</td>
      <td style="text-align: center;">99.26</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 17:00</td>
      <td style="text-align: center;">0.536</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.408</td>
      <td style="text-align: center;">94.29</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 19:00</td>
      <td style="text-align: center;">0.735</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.255</td>
      <td style="text-align: center;">95.45</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 21:00</td>
      <td style="text-align: center;">0.655</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.305</td>
      <td style="text-align: center;">97.32</td>
      <td style="text-align: center;">112</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月29日 23:00</td>
      <td style="text-align: center;">0.668</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.222</td>
      <td style="text-align: center;">99.22</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 01:00</td>
      <td style="text-align: center;">0.568</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.252</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 03:00</td>
      <td style="text-align: center;">0.647</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">144</td>
      <td style="text-align: center;">1.262</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 05:00</td>
      <td style="text-align: center;">0.607</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.156</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 07:00</td>
      <td style="text-align: center;">0.573</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.263</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 09:00</td>
      <td style="text-align: center;">0.680</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.417</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 11:00</td>
      <td style="text-align: center;">0.621</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.461</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 13:00</td>
      <td style="text-align: center;">0.606</td>
      <td style="text-align: center;">99.26</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.296</td>
      <td style="text-align: center;">99.22</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 15:00</td>
      <td style="text-align: center;">0.769</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.335</td>
      <td style="text-align: center;">95.45</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 17:00</td>
      <td style="text-align: center;">0.522</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">130</td>
      <td style="text-align: center;">1.199</td>
      <td style="text-align: center;">96.97</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">2018年5月30日 19:00</td>
      <td style="text-align: center;">0.703</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">146</td>
      <td style="text-align: center;">1.204</td>
      <td style="text-align: center;">96.53</td>
      <td style="text-align: center;">144</td>
   </tr>
	</tbody>
</table>

## 补充说明
1、以上案例数据来自第三方性能监控服务提供方，以实际终端用户访问结果为准。
2、以上加速效果仅供参考使用，产品加速效果还受客户业务类型和源站网络条件等因素的影响，以实际测试效果为准。
