<blockquote class="d-mod-alarm">
              <div class="d-mod-title d-alarm-title">
                <i class="d-icon-alarm"></i>Notice:
              </div>
               <p>Field value "HTTP/3" for the HTTP protocol identifier (the 14th field in the offline log) in general logs will be in beta from September 13, 2021, which will not affect the CDN console and APIs. Please note that getting log data from offline log packages may require adjustment.</br></br>QUIC access has been in beta. For more details, see <a href="https://cloud.tencent.com/document/product/228/51800">QUIC</a>.</p>
            </blockquote>



## Features

After a domain name is connected to CDN, all requests will be scheduled to a CDN node. If the requested resource is cached on the node, the resource will be returned directly; otherwise, the request will be passed to the origin server to pull the requested resource.

CDN nodes respond to most of the user requests. To facilitate access analysis, CDN packages access logs of the entire network at an hourly granularity and retains them for 30 days by default. These logs can also be downloaded.

>? 
>- Currently origin-pull logs are not provided. Only node access logs are provided.
>- ECDN domain name offline logs cannot be queried by regions for now. For more information, see [Log Management](https://intl.cloud.tencent.com/document/product/570/15258).

## Use Cases
### Access behavior analysis
You can download access logs and analyze popular resources and active users.

### Service quality monitoring
By downloading access logs, you can stay on top of the service status of all CDN nodes and calculate the average response time, average download speed, and other metrics.

## Directions
### How to use
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), click **Log Service** on the left sidebar, and select a domain name and time range to query access logs. You can select multiple log packages and download them in batches:


>!
>- The access logs are packaged by hour by default. If there is no request to the domain name for the hour, no log package will be generated for this hour.
>- For the same domain name, logs of accesses from within and outside the Chinese mainland are packaged separately. Log packages are named in the format of "[time]-[domain name]-[acceleration region]".
>- The access logs are collected from each CDN cache node, so the delay may vary. Generally, the delay for querying and downloading log packages is about 30 minutes. Log packages will be added continuously and will stabilize after around 24 hours.
>- The access log packages of a domain name are retained for 30 days. You can use an SCF function to transfer the log packages to COS as instructed in [Regularly Storing CDN Logs](https://intl.cloud.tencent.com/document/product/228/36014) for permanent storage.

### Fields
The fields (from left to right) in the logs are listed as below:
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">No.</th>
<th align="left" style="width:560px;font-weight:700">Fields  </th>
</tr>
</thead>
<tbody><tr>
<td>1</td>
<td>Request time</td>
</tr>
</tbody>
<tbody><tr>
<td>2</td>
<td>Client IP</td>
</tr>
</tbody>
<tbody><tr>
<td>3</td>
<td>Domain name</td>
</tr>
</tbody>
<tbody><tr>
<td>4</td>
<td>Request path</td>
</tr>
</tbody>
<tbody><tr>
<td>5</td>
<td>Number of bytes accessed this time, including the size of the file itself and the size of the request header.</td>
</tr>
</tbody>
<tbody><tr>
<td>6</td>
<td>Province numbers for Chinese mainland logs; region numbers for logs outside the Chinese mainland (see the mapping table below).</td>
</tr>
</tbody>
<tbody><tr>
<td>7</td>
<td>ISP numbers for Chinese mainland logs; `-1` will be used for logs outside the Chinese mainland (see the mapping table below).</td>
</tr>
</tbody>
<tbody><tr>
<td>8</td>
<td>HTTP status code</td>
</tr>
</tbody>
<tbody><tr>
<td>9</td>
<td>Referer information</td>
</tr>
</tbody>
<tbody><tr>
<td>10</td>
<td>Response time (in milliseconds), which refers to the time it takes for a node to return all packets to the client after receiving a request.</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>11</td>
<td>User-Agent information</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>12</td>
<td>Range parameter</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>13</td>
<td>HTTP method</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>14</td>
<td>HTTP protocol identifier</td>
</tr>
</tbody>
</tbody>
<tbody><tr>
<td>15</td>
<td>Cache hit/miss. A hit in a CDN edge server or parent node will be marked as hit.</td>
</tr>
<td>16</td>
<td>A port connecting the client and CDN nodes. This field will be displayed as `-` if the port does not exist.</td>
</tr>
</tbody></table>

### Region/ISP mappings

[](id:.E7.9C.81.E4.BB.BD.E6.98.A0.E5.B0.84)
#### Chinese mainland provinces
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">Region ID</th>
<th align="left" style="width:120px;font-weight:700">Region</th>
<th align="left" style="width:100px;font-weight:700">Region ID</th>
<th align="left" style="width:120px;font-weight:700">Region</th>
<th align="left" style="width:100px;font-weight:700">Region ID</th>
<th align="left" style="width:120px;font-weight:700">Region</th>
</tr>
</thead>
<tbody><tr>
<td>22</td>
<td>Beijing</td>
<td>86</td>
<td>Inner Mongolia</td>
<td>146</td>
<td>Shanxi</td>
</tr>
<tr>
<td>1069</td>
<td>Hebei</td>
<td>1177</td>
<td>Tianjin</td>
<td>119</td>
<td>Ningxia</td>
</tr>
<tr>
<td>152</td>
<td>Shaanxi</td>
<td>1208</td>
<td>Gansu</td>
<td>1467</td>
<td>Qinghai</td>
</tr>
<tr>
<td>1468</td>
<td>Xinjiang</td>
<td>145</td>
<td>Heilongjiang</td>
<td>1445</td>
<td>Jilin</td>
</tr>
<tr>
<td>1464</td>
<td>Liaoning</td>
<td>2</td>
<td>Fujian</td>
<td>120</td>
<td>Jiangsu</td>
</tr>
<tr>
<td>121</td>
<td>Anhui</td>
<td>122</td>
<td>Shandong</td>
<td>1050</td>
<td>Shanghai</td>
</tr>
<tr>
<td>1442</td>
<td>Zhejiang</td>
<td>182</td>
<td>Henan</td>
<td>1135</td>
<td>Hubei</td>
</tr>
<tr>
<td>1465</td>
<td>Jiangxi</td>
<td>1466</td>
<td>Hunan</td>
<td>118</td>
<td>Guizhou</td>
</tr>
<tr>
<td>153</td>
<td>Yunnan</td>
<td>1051</td>
<td>Chongqing</td>
<td>1068</td>
<td>Sichuan</td>
</tr>
<tr>
<td>1155</td>
<td>Tibet</td>
<td>4</td>
<td>Guangdong</td>
<td>173</td>
<td>Guangxi</td>
</tr>
<tr>
<td>1441</td>
<td>Hainan</td>
<td>0</td>
<td>Other</td>
<td>1</td>
<td>Hong Kong (China), Macao (China), and Taiwan (China)</td>
</tr>
<tr>
<td>-1</td>
<td>Outside the Chinese mainland</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody></table>


#### Chinese mainland ISPs
<table style="width:660px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ISP ID</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
<th align="left" style="width:100px;font-weight:700">ISP ID</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
<th align="left" style="width:100px;font-weight:700">ISP ID</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
</tr>
</thead>
<tbody><tr>
<td>2</td>
<td>China Telecom</td>
<td>26</td>
<td>China Unicom</td>
<td>38</td>
<td>CERNET</td>
</tr>
</tbody>
<tbody><tr>
<td>43</td>
<td>Great Wall Broadband Network</td>
<td>1046</td>
<td>China Mobile</td>
<td>3947</td>
<td>China Mobile Tietong</td>
</tr>
</tbody>
<tbody><tr>
<td>-1</td>
<td>ISPs outside the Chinese mainland</td>
<td>0</td>
<td>Other ISPs</td>
<td></td>
<td></td>
</tr>
</tbody>
</table>


#### Regions outside the Chinese mainland
<table style="width:710px">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">Region ID</th>
<th align="left" style="width:170px;font-weight:700">Region</th>
<th align="left" style="width:100px;font-weight:700">Region ID</th>
<th align="left" style="width:120px;font-weight:700">Region</th>
<th align="left" style="width:100px;font-weight:700">Region ID</th>
<th align="left" style="width:120px;font-weight:700">Region</th>
</tr>
</thead>
<tbody><tr>
<td>2000000001</td>
<td>Asia Pacific Zone 1 (service area)</td>
<td>765</td>
<td>Slovakia</td>
<td>1613</td>
<td>Angola</td>
</tr>
<tr>
<td>2000000002</td>
<td>Asia Pacific Zone 2 (service area)</td>
<td>766</td>
<td>Serbia</td>
<td>1617</td>
<td>Ivory Coast</td>
</tr>
<tr>
<td>2000000003</td>
<td>Asia Pacific Zone 3 (service area)</td>
<td>770</td>
<td>Finland</td>
<td>1620</td>
<td>Sudan</td>
</tr>
<tr>
<td>2000000004</td>
<td>Middle East (service area)</td>
<td>773</td>
<td>Belgium</td>
<td>1681</td>
<td>Mauritius</td>
</tr>
<tr>
<td>2000000005</td>
<td>North America (service area)</td>
<td>809</td>
<td>Bulgaria</td>
<td>1693</td>
<td>Morocco</td>
</tr>
<tr>
<td>2000000006</td>
<td>Europe (service area)</td>
<td>811</td>
<td>Slovenia</td>
<td>1695</td>
<td>Algeria</td>
</tr>
<tr>
<td>2000000007</td>
<td>South America (service area)</td>
<td>812</td>
<td>Moldova</td>
<td>1698</td>
<td>Guinea</td>
</tr>
<tr>
<td>2000000008</td>
<td>Africa (service area)</td>
<td>813</td>
<td>Macedonia</td>
<td>1730</td>
<td>Senegal</td>
</tr>
<tr>
<td>-20</td>
<td>Asia (client area)</td>
<td>824</td>
<td>Estonia</td>
<td>1864</td>
<td>Tunisia</td>
</tr>
<tr>
<td>-21</td>
<td>South America (client area)</td>
<td>835</td>
<td>Croatia</td>
<td>1909</td>
<td>Uruguay</td>
</tr>
<tr>
<td>-22</td>
<td>North America (client area)</td>
<td>837</td>
<td>Poland</td>
<td>1916</td>
<td>Greenland</td>
</tr>
<tr>
<td>-23</td>
<td>Europe (client area)</td>
<td>852</td>
<td>Latvia</td>
<td>2026</td>
<td>Taiwan (China)</td>
</tr>
<tr>
<td>-24</td>
<td>Africa (client area)</td>
<td>857</td>
<td>Jordan</td>
<td>2083</td>
<td>Myanmar</td>
</tr>
<tr>
<td>-25</td>
<td>Oceania (client area)</td>
<td>884</td>
<td>Kyrgyzstan</td>
<td>2087</td>
<td>Brunei</td>
</tr>
<tr>
<td>35</td>
<td>Nepal</td>
<td>896</td>
<td>Ireland</td>
<td>2094</td>
<td>Sri Lanka</td>
</tr>
<tr>
<td>57</td>
<td>Thailand</td>
<td>901</td>
<td>Libya</td>
<td>2150</td>
<td>Panama</td>
</tr>
<tr>
<td>73</td>
<td>India</td>
<td>904</td>
<td>Armenia</td>
<td>2175</td>
<td>Colombia</td>
</tr>
<tr>
<td>144</td>
<td>Vietnam</td>
<td>921</td>
<td>Yemen</td>
<td>2273</td>
<td>Monaco</td>
</tr>
<tr>
<td>192</td>
<td>France</td>
<td>926</td>
<td>Belarus</td>
<td>2343</td>
<td>Andorra</td>
</tr>
<tr>
<td>207</td>
<td>United Kingdom</td>
<td>971</td>
<td>Luxembourg</td>
<td>2421</td>
<td>Turkmenistan</td>
</tr>
<tr>
<td>208</td>
<td>Sweden</td>
<td>1036</td>
<td>New Zealand</td>
<td>2435</td>
<td>Laos</td>
</tr>
<tr>
<td>209</td>
<td>Germany</td>
<td>1044</td>
<td>Japan</td>
<td>2488</td>
<td>East Timor</td>
</tr>
<tr>
<td>213</td>
<td>Italy</td>
<td>1066</td>
<td>Pakistan</td>
<td>2490</td>
<td>Tonga</td>
</tr>
<tr>
<td>214</td>
<td>Spain</td>
<td>1070</td>
<td>Malta</td>
<td>2588</td>
<td>Philippines</td>
</tr>
<tr>
<td>386</td>
<td>United Arab Emirates</td>
<td>1091</td>
<td>Bahamas</td>
<td>2609</td>
<td>Venezuela</td>
</tr>
<tr>
<td>391</td>
<td>Israel</td>
<td>1129</td>
<td>Argentina</td>
<td>2612</td>
<td>Bolivia</td>
</tr>
<tr>
<td>397</td>
<td>Ukraine</td>
<td>1134</td>
<td>Bangladesh</td>
<td>2613</td>
<td>Brazil</td>
</tr>
<tr>
<td>398</td>
<td>Russia</td>
<td>1158</td>
<td>Cambodia</td>
<td>2623</td>
<td>Costa Rica</td>
</tr>
<tr>
<td>417</td>
<td>Kazakhstan</td>
<td>1159</td>
<td>Macao (China)</td>
<td>2626</td>
<td>Mexico</td>
</tr>
<tr>
<td>428</td>
<td>Portugal</td>
<td>1176</td>
<td>Singapore</td>
<td>2639</td>
<td>Honduras</td>
</tr>
<tr>
<td>443</td>
<td>Greece</td>
<td>1179</td>
<td>Maldives</td>
<td>2645</td>
<td>El Salvador</td>
</tr>
<tr>
<td>471</td>
<td>Saudi Arabia</td>
<td>1180</td>
<td>Afghanistan</td>
<td>2647</td>
<td>Paraguay</td>
</tr>
<tr>
<td>529</td>
<td>Denmark</td>
<td>1185</td>
<td>Fiji</td>
<td>2661</td>
<td>Peru</td>
</tr>
<tr>
<td>565</td>
<td>Iran</td>
<td>1186</td>
<td>Mongolia</td>
<td>2728</td>
<td>Nicaragua</td>
</tr>
<tr>
<td>578</td>
<td>Norway</td>
<td>1195</td>
<td>Indonesia</td>
<td>2734</td>
<td>Ecuador</td>
</tr>
<tr>
<td>669</td>
<td>United States</td>
<td>1200</td>
<td>Hong Kong (China)</td>
<td>2768</td>
<td>Guatemala</td>
</tr>
<tr>
<td>692</td>
<td>Syria</td>
<td>1233</td>
<td>Qatar</td>
<td>2999</td>
<td>Aruba</td>
</tr>
<tr>
<td>704</td>
<td>Cyprus</td>
<td>1255</td>
<td>Iceland</td>
<td>3058</td>
<td>Ethiopia</td>
</tr>
<tr>
<td>706</td>
<td>Czech</td>
<td>1289</td>
<td>Albania</td>
<td>3144</td>
<td>Bosnia and Herzegovina</td>
</tr>
<tr>
<td>707</td>
<td>Switzerland</td>
<td>1353</td>
<td>Uzbekistan</td>
<td>3216</td>
<td>Dominican</td>
</tr>
<tr>
<td>708</td>
<td>Iraq</td>
<td>1407</td>
<td>San Marino</td>
<td>3379</td>
<td>South Korea</td>
</tr>
<tr>
<td>714</td>
<td>Netherlands</td>
<td>1416</td>
<td>Kuwait</td>
<td>3701</td>
<td>Malaysia</td>
</tr>
<tr>
<td>717</td>
<td>Romania</td>
<td>1417</td>
<td>Montenegro</td>
<td>3839</td>
<td>Canada</td>
</tr>
<tr>
<td>721</td>
<td>Lebanon</td>
<td>1493</td>
<td>Tajikistan</td>
<td>4450</td>
<td>Australia</td>
</tr>
<tr>
<td>725</td>
<td>Hungary</td>
<td>1501</td>
<td>Bahrain</td>
<td>4460</td>
<td>Chinese mainland</td>
</tr>
<tr>
<td>726</td>
<td>Georgia</td>
<td>1543</td>
<td>Chile</td>
<td>-15</td>
<td>Asia - other</td>
</tr>
<tr>
<td>731</td>
<td>Azerbaijan</td>
<td>1559</td>
<td>South Africa</td>
<td>-14</td>
<td>South America - other</td>
</tr>
<tr>
<td>734</td>
<td>Austria</td>
<td>1567</td>
<td>Egypt</td>
<td>-13</td>
<td>North America - other</td>
</tr>
<tr>
<td>736</td>
<td>Palestine</td>
<td>1590</td>
<td>Kenya</td>
<td>-12</td>
<td>Europe - other</td>
</tr>
<tr>
<td>737</td>
<td>Türkiye</td>
<td>1592</td>
<td>Nigeria</td>
<td>-11</td>
<td>Africa - other</td>
</tr>
<tr>
<td>759</td>
<td>Lithuania</td>
<td>1598</td>
<td>Tanzania</td>
<td>-10</td>
<td>Oceania - other</td>
</tr>
<tr>
<td>763</td>
<td>Oman</td>
<td>1611</td>
<td>Madagascar</td>
<td>-2</td>
<td>Outside the Chinese mainland - other</td>
</tr>
</tbody></table>


#### ISPs outside the Chinese mainland
<table style="width:220px;">
<thead>
<tr>
<th align="left" style="width:100px;font-weight:700">ISP ID</th>
<th align="left" style="width:120px;font-weight:700">ISP</th>
</tr>
</thead>
<tbody><tr>
<td>-1</td>
<td>ISPs outside the Chinese mainland</td>
</tr>
</tbody>
</table>

### Notes
The traffic/bandwidth data calculated based on the number of bytes recorded in the fifth field of an access log is different from the billable CDN traffic/bandwidth data for the following reason:
- Only application-layer data can be recorded in access logs. During actual data transfer, the traffic generated over the network is around 5-15% more than the application-layer traffic, including the following two parts:
	- Consumption by TCP/IP headers: in TCP/IP-based HTTP requests, each packet has a maximum size of 1,500 bytes and includes TCP and IP headers of 40 bytes, which generate traffic during transfer but cannot be counted by the application layer. The overhead of this part is around 3%.
	- TCP retransmission: during normal data transfer over the network, around 3% to 10% of packets are lost on the Internet and retransmitted by the server. This type of traffic, which accounts for 3-7% of the total traffic, cannot be counted at the application layer.
- As an industry standard, the billable traffic is the sum of the application-layer traffic and the overheads described above. Tencent Cloud CDN takes 10% as the overheads proportion, so the monitored traffic is around 110% of the logged traffic.

## Examples

### Sample log of accesses from within the Chinese mainland
![](https://mc.qcloudimg.com/static/img/a3ef1ea051dc277872ec10a7135872df/logs.png)

### Sample log of accesses from outside the Chinese mainland
![](https://main.qcloudimg.com/raw/b0612a5204abdbdc6a4364ad02972900.png)

