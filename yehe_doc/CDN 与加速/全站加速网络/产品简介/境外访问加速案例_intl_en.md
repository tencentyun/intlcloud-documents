## Test Description
### Test methods
A third-party network application performance monitoring and speed test method widely used in the industry is adopted, and the test service provider is Bonree.

### Test parameters
<table style="width: 80%;display: table;margin-bottom:40px;">
	<tbody>
		<tr>
			<th scope="row" style="width:102px">Test time</th> 
			<td style="width:385px"> May 24, 2010 00:00–May 30, 2018 20:00 </td> 
		</tr>
		<tr>
			<th scope="row" style="width:102px">Client address</th> 
			<td style="width:385px"> Countries and regions such as Hong Kong (China), Singapore, and Malaysia </td> 
		</tr>
		<tr>
			<th scope="row" style="width:102px">Origin server address</th> 
			<td style="width:385px"> IDC in Virginia, US</td>
		</tr>
		<tr>
			<th scope="row" style="width:102px">Test link</th> 
			<td style="width:385px"> https://****/**/GetPage?PageId=7141974606000205</td>
		</tr>
		<tr>
			<th scope="row" style="width:102px">Comparison method</th> 
			<td style="width:385px"> The same test link is used to compare the direct access to the origin server and ECDN accelerated access by setting host IP and CNAME resolution respectively</td>
		</tr>
	</tbody>
</table>

## Test Results

### Performance curve

![](https://main.qcloudimg.com/raw/b0825a24b98665637335aa8d672bec51.png)

### Usability curve

![](https://main.qcloudimg.com/raw/af8c79e78a2d7b6fc906491804d69511.png)

> **Summary**  
> 1. After ECDN is used, the average access performance of the product is improved by 104.71% **, and the page loading performance is significantly improved;  
> 2. In cross-border access scenarios, traditional public network access is affected by network packet losses and long delays, and the access stability fluctuates greatly. After ECDN is used, the **availability and stability** of page access are greatly improved.

### Data summary analysis

<table style="display:table;">
	<tbody>
		<tr>
			<th rowspan="2" style="text-align: center;width: 100px;"> Monitoring Task </th>
			<th colspan="3" style="text-align: center"> Performance (Seconds) </th>
			<th colspan="3" style="text-align: center"> Availability (%) </th>
			<th colspan="2" style="text-align: center"> Monitors </th>
		</tr>
		<tr>
			<th style="text-align: center; width: 70px;"> Average </th>
			<th colspan="1" style="text-align: center; width: 70px;"> Best </th>
			<th colspan="1" style="text-align: center; width: 70px;"> Worse </th>
			<th style="text-align: center; width: 70px;"> Average </th>
			<th colspan="1" style="text-align: center; width: 70px;"> Best </th>
			<th colspan="1" style="text-align: center; width: 70px;"> Worse </th>
			<th colspan="1" style="text-align: center; width: 70px;"> Erroneous Points </th>
			<th colspan="1" style="text-align: center; width: 70px;"> Monitored Points </th>
		</tr>
		<tr>
			<td style="width: 58px; text-align: center;"> ECDN Accelerated Access </td>
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
			<td style="width: 58px; text-align: center;"> Direct Access to Origin Server </td>
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

### Data details

<table  style="display: table;">
	<tbody>
		<tr>
			<th rowspan="2" style="text-align: center; width: 150px;"> Time </th>
			<th colspan="3" style="text-align: center; width: 270px;"> ECDN Accelerated Access </th>
			<th colspan="3" style="text-align: center; width: 270px;"> Direct Access to Origin Server </th>
		</tr>
		<tr>
			<th style="text-align: center; width: 90px;"> Performance (Seconds) </th>
			<th style="text-align: center; width: 90px;"> Availability (%) </th>
			<th style="text-align: center; width: 90px;"> Monitored Points </th>
			<th style="text-align: center; width: 90px;"> Performance (Seconds) </th>
			<th style="text-align: center; width: 90px;"> Availability (%) </th>
			<th style="text-align: center; width: 90px;"> Monitored Points </th>
		</tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 01:00</td>
      <td style="text-align: center;">0.583</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.287</td>
      <td style="text-align: center;">98.39</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 03:00</td>
      <td style="text-align: center;">0.622</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.454</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 05:00</td>
      <td style="text-align: center;">0.648</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.256</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">108</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 07:00</td>
      <td style="text-align: center;">0.664</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.241</td>
      <td style="text-align: center;">98.33</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 09:00</td>
      <td style="text-align: center;">0.586</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.159</td>
      <td style="text-align: center;">96.77</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 11:00</td>
      <td style="text-align: center;">0.614</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.319</td>
      <td style="text-align: center;">97.41</td>
      <td style="text-align: center;">116</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 13:00</td>
      <td style="text-align: center;">0.696</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.335</td>
      <td style="text-align: center;">98.39</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 15:00</td>
      <td style="text-align: center;">0.621</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">116</td>
      <td style="text-align: center;">1.152</td>
      <td style="text-align: center;">97.58</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 17:00</td>
      <td style="text-align: center;">0.547</td>
      <td style="text-align: center;">98.44</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.181</td>
      <td style="text-align: center;">98.33</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 19:00</td>
      <td style="text-align: center;">0.723</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.302</td>
      <td style="text-align: center;">95.31</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 21:00</td>
      <td style="text-align: center;">0.693</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.209</td>
      <td style="text-align: center;">99.19</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 24, 2018 23:00</td>
      <td style="text-align: center;">0.734</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.257</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 01:00</td>
      <td style="text-align: center;">0.589</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.254</td>
      <td style="text-align: center;">98.44</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 03:00</td>
      <td style="text-align: center;">0.636</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">144</td>
      <td style="text-align: center;">1.277</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 05:00</td>
      <td style="text-align: center;">0.578</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.262</td>
      <td style="text-align: center;">99.17</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 07:00</td>
      <td style="text-align: center;">0.606</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">116</td>
      <td style="text-align: center;">1.343</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 09:00</td>
      <td style="text-align: center;">0.706</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.305</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 11:00</td>
      <td style="text-align: center;">0.563</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.253</td>
      <td style="text-align: center;">99.22</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 13:00</td>
      <td style="text-align: center;">0.701</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.255</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 15:00</td>
      <td style="text-align: center;">0.624</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.277</td>
      <td style="text-align: center;">97.66</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 17:00</td>
      <td style="text-align: center;">0.698</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.359</td>
      <td style="text-align: center;">96.09</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 19:00</td>
      <td style="text-align: center;">0.697</td>
      <td style="text-align: center;">99.11</td>
      <td style="text-align: center;">112</td>
      <td style="text-align: center;">1.160</td>
      <td style="text-align: center;">96.77</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 21:00</td>
      <td style="text-align: center;">0.744</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.312</td>
      <td style="text-align: center;">96.43</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 25, 2018 23:00</td>
      <td style="text-align: center;">0.711</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.284</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 01:00</td>
      <td style="text-align: center;">0.643</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.316</td>
      <td style="text-align: center;">99.22</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 03:00</td>
      <td style="text-align: center;">0.683</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.248</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 05:00</td>
      <td style="text-align: center;">0.596</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.307</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 07:00</td>
      <td style="text-align: center;">0.678</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.258</td>
      <td style="text-align: center;">97.66</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 09:00</td>
      <td style="text-align: center;">0.709</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.298</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 11:00</td>
      <td style="text-align: center;">0.601</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.315</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 13:00</td>
      <td style="text-align: center;">0.553</td>
      <td style="text-align: center;">98.57</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.195</td>
      <td style="text-align: center;">97.66</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 15:00</td>
      <td style="text-align: center;">0.583</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.153</td>
      <td style="text-align: center;">97.41</td>
      <td style="text-align: center;">116</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 17:00</td>
      <td style="text-align: center;">0.658</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.414</td>
      <td style="text-align: center;">98.53</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 19:00</td>
      <td style="text-align: center;">0.768</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.430</td>
      <td style="text-align: center;">96.32</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 21:00</td>
      <td style="text-align: center;">0.603</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.285</td>
      <td style="text-align: center;">98.48</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 26, 2018 23:00</td>
      <td style="text-align: center;">0.792</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.218</td>
      <td style="text-align: center;">97.58</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 01:00</td>
      <td style="text-align: center;">0.659</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.249</td>
      <td style="text-align: center;">98.48</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 03:00</td>
      <td style="text-align: center;">0.667</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.310</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 05:00</td>
      <td style="text-align: center;">0.617</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.396</td>
      <td style="text-align: center;">97.73</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 07:00</td>
      <td style="text-align: center;">0.627</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.374</td>
      <td style="text-align: center;">98.48</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 09:00</td>
      <td style="text-align: center;">0.580</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.399</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 11:00</td>
      <td style="text-align: center;">0.600</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.317</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 13:00</td>
      <td style="text-align: center;">0.661</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.420</td>
      <td style="text-align: center;">96.97</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 15:00</td>
      <td style="text-align: center;">0.668</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.463</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 17:00</td>
      <td style="text-align: center;">0.544</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.233</td>
      <td style="text-align: center;">93.97</td>
      <td style="text-align: center;">116</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 19:00</td>
      <td style="text-align: center;">0.722</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.374</td>
      <td style="text-align: center;">97.14</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 21:00</td>
      <td style="text-align: center;">0.764</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">116</td>
      <td style="text-align: center;">1.281</td>
      <td style="text-align: center;">93.55</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 27, 2018 23:00</td>
      <td style="text-align: center;">0.686</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.272</td>
      <td style="text-align: center;">93.94</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 01:00</td>
      <td style="text-align: center;">0.666</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.473</td>
      <td style="text-align: center;">97.79</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 03:00</td>
      <td style="text-align: center;">0.603</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.297</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 05:00</td>
      <td style="text-align: center;">0.549</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.467</td>
      <td style="text-align: center;">99.29</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 07:00</td>
      <td style="text-align: center;">0.589</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.312</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 09:00</td>
      <td style="text-align: center;">0.601</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.415</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 11:00</td>
      <td style="text-align: center;">0.602</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.263</td>
      <td style="text-align: center;">99.17</td>
      <td style="text-align: center;">120</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 13:00</td>
      <td style="text-align: center;">0.613</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.372</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 15:00</td>
      <td style="text-align: center;">0.663</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">122</td>
      <td style="text-align: center;">1.531</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 17:00</td>
      <td style="text-align: center;">0.576</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.309</td>
      <td style="text-align: center;">98.53</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 19:00</td>
      <td style="text-align: center;">0.614</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.290</td>
      <td style="text-align: center;">95.00</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 21:00</td>
      <td style="text-align: center;">0.583</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.275</td>
      <td style="text-align: center;">95.00</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 28, 2018 23:00</td>
      <td style="text-align: center;">0.674</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.239</td>
      <td style="text-align: center;">99.26</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 01:00</td>
      <td style="text-align: center;">0.657</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.503</td>
      <td style="text-align: center;">99.29</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 03:00</td>
      <td style="text-align: center;">0.565</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.469</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 05:00</td>
      <td style="text-align: center;">0.544</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.162</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 07:00</td>
      <td style="text-align: center;">0.579</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.343</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 09:00</td>
      <td style="text-align: center;">0.567</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">120</td>
      <td style="text-align: center;">1.310</td>
      <td style="text-align: center;">98.39</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 11:00</td>
      <td style="text-align: center;">0.585</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.262</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 13:00</td>
      <td style="text-align: center;">0.606</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.309</td>
      <td style="text-align: center;">97.86</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 15:00</td>
      <td style="text-align: center;">0.655</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">144</td>
      <td style="text-align: center;">1.253</td>
      <td style="text-align: center;">99.26</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 17:00</td>
      <td style="text-align: center;">0.536</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.408</td>
      <td style="text-align: center;">94.29</td>
      <td style="text-align: center;">140</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 19:00</td>
      <td style="text-align: center;">0.735</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.255</td>
      <td style="text-align: center;">95.45</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 21:00</td>
      <td style="text-align: center;">0.655</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.305</td>
      <td style="text-align: center;">97.32</td>
      <td style="text-align: center;">112</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 29, 2018 23:00</td>
      <td style="text-align: center;">0.668</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">128</td>
      <td style="text-align: center;">1.222</td>
      <td style="text-align: center;">99.22</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 01:00</td>
      <td style="text-align: center;">0.568</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.252</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 03:00</td>
      <td style="text-align: center;">0.647</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">144</td>
      <td style="text-align: center;">1.262</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 05:00</td>
      <td style="text-align: center;">0.607</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">140</td>
      <td style="text-align: center;">1.156</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 07:00</td>
      <td style="text-align: center;">0.573</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">124</td>
      <td style="text-align: center;">1.263</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 09:00</td>
      <td style="text-align: center;">0.680</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
      <td style="text-align: center;">1.417</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 11:00</td>
      <td style="text-align: center;">0.621</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.461</td>
      <td style="text-align: center;">99.24</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 13:00</td>
      <td style="text-align: center;">0.606</td>
      <td style="text-align: center;">99.26</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.296</td>
      <td style="text-align: center;">99.22</td>
      <td style="text-align: center;">128</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 15:00</td>
      <td style="text-align: center;">0.769</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">136</td>
      <td style="text-align: center;">1.335</td>
      <td style="text-align: center;">95.45</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 17:00</td>
      <td style="text-align: center;">0.522</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">130</td>
      <td style="text-align: center;">1.199</td>
      <td style="text-align: center;">96.97</td>
      <td style="text-align: center;">132</td>
   </tr>
   <tr>
      <td style="text-align: center;">May 30, 2018 19:00</td>
      <td style="text-align: center;">0.703</td>
      <td style="text-align: center;">100.00</td>
      <td style="text-align: center;">146</td>
      <td style="text-align: center;">1.204</td>
      <td style="text-align: center;">96.53</td>
      <td style="text-align: center;">144</td>
   </tr>
	</tbody>
</table>

## Notes
1. Data in the above case comes from a third-party performance monitoring service provider, and the actual performance is subject to actual end user access results.
2. The above acceleration effect is for reference only, which is subject to factors such as customer business type and origin server network conditions.
