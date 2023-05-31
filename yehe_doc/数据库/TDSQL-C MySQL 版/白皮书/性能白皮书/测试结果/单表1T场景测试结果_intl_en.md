
This document lists the performance comparison test results between TDSQL-C for MySQL and TencentDB for MySQL in the 1 TB single table scenario.

### Overview
In the 1 TB single table scenario, the test dataset contains 4 billion data records in one single table with a storage space of 1 TB.

### Test Conclusion
- In the read scenario, TDSQL-C for MySQL can achieve a CPU utilization of above 90% on compute nodes. The test shows that the resource utilization of TDSQL-C for MySQL is better than that of TencentDB for MySQL.
- In the write scenario, TDSQL-C for MySQL outperforms TencentDB for MySQL under lower specifications, and as the specifications and data volume increase, its performance advantage gets much greater.

<table>
<tr><th>Dataset Characteristics</th><th>Test Scenario</th><th>Read Type</th><th>Conclusion</th></tr>
<tr><td rowspan = "5" >1 TB single table</td><td>Write</td><td>-</td><td>TDSQL-C for MySQL has a higher performance</td></tr>
<tr><td>Read</td><td>POINT SELECT</td><td>TDSQL-C for MySQL and TencentDB for MySQL have generally the same performance under most specifications, but the former outperforms the latter under the maximum specification</td></tr>
<tr><td>Read</td><td>RANGE SELECT</td><td>TDSQL-C for MySQL and TencentDB for MySQL have generally the same performance under most specifications</td></tr>
<tr><td>Read-write</td><td>POINT SELECT</td><td>TDSQL-C for MySQL has a higher performance</td></tr>
<tr><td>Read-write</td><td>RANGE SELECT</td><td>TDSQL-C for MySQL and TencentDB for MySQL have generally the same performance under most specifications</td></tr>
</table>

### Test Results
**Scenario 1: Write**
![](https://qcloudimg.tencent-cloud.cn/raw/596a3818289c1286562b0992eb6afee0.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>256</td><td>4000000000</td><td>1</td><td>10881</td><td>17816</td></tr>
<tr><td>4-core 16 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>26827</td><td>33700</td></tr>
<tr><td>4-core 32 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>31404</td><td>41098</td></tr>
<tr><td>8-core 32 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>44167</td><td>76047</td></tr>
<tr><td>8-core 64 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>55609</td><td>81191</td></tr>
<tr><td>16-core 64 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>88401</td><td>134317</td></tr>
<tr><td>16-core 96 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>97068</td><td>134923</td></tr>
<tr><td>16-core 128 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>101274</td><td>134340</td></tr>
<tr><td>32-core 128 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>111626</td><td>196333</td></tr>
<tr><td>32-core 256 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>131058</td><td>206395</td></tr>
<tr><td>64-core 256 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>140587</td><td>256415</td></tr>
</table>
**Scenario 2: Read (POINT SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/993bf681e7ccb9eecb41096623b09505.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>256</td><td>4000000000</td><td>1</td><td>29135</td><td>31504</td></tr>
<tr><td>4-core 16 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>59667</td><td>61128</td></tr>
<tr><td>4-core 32 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>66219</td><td>64707</td></tr>
<tr><td>8-core 32 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>119374</td><td>128884</td></tr>
<tr><td>8-core 64 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>127005</td><td>129857</td></tr>
<tr><td>16-core 64 GB MEM</td><td>1000</td><td>4000000000</td><td>1</td><td>229007</td><td>210873</td></tr>
<tr><td>16-core 96 GB MEM</td><td>1000</td><td>4000000000</td><td>1</td><td>230460</td><td>217415</td></tr>
<tr><td>16-core 128 GB MEM</td><td>1000</td><td>4000000000</td><td>1</td><td>236767</td><td>228319</td></tr>
<tr><td>32-core 128 GB MEM</td><td>1000</td><td>4000000000</td><td>1</td><td>377009</td><td>368868</td></tr>
<tr><td>32-core 256 GB MEM</td><td>1000</td><td>4000000000</td><td>1</td><td>412356</td><td>421931</td></tr>
<tr><td>64-core 256 GB MEM</td><td>1000</td><td>4000000000</td><td>1</td><td>569523</td><td>794997</td></tr>
</table>
**Scenario 3: Read (RANGE SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/cf77715bcecaa6a88529a0787855c350.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>32</td><td>4000000000</td><td>1</td><td>11773</td><td>14358</td></tr>
<tr><td>4-core 16 GB MEM</td><td>64</td><td>4000000000</td><td>1</td><td>25688</td><td>26093</td></tr>
<tr><td>4-core 32 GB MEM</td><td>64</td><td>4000000000</td><td>1</td><td>26826</td><td>28748</td></tr>
<tr><td>8-core 32 GB MEM</td><td>128</td><td>4000000000</td><td>1</td><td>48998</td><td>54387</td></tr>
<tr><td>8-core 64 GB MEM</td><td>128</td><td>4000000000</td><td>1</td><td>54987</td><td>60345</td></tr>
<tr><td>16-core 64 GB MEM</td><td>256</td><td>4000000000</td><td>1</td><td>103212</td><td>113117</td></tr>
<tr><td>16-core 96 GB MEM</td><td>256</td><td>4000000000</td><td>1</td><td>105302</td><td>113609</td></tr>
<tr><td>16-core 128 GB MEM</td><td>256</td><td>4000000000</td><td>1</td><td>108209</td><td>114218</td></tr>
<tr><td>32-core 128 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>187161</td><td>190716</td></tr>
<tr><td>32-core 256 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>192407</td><td>190472</td></tr>
<tr><td>64-core 256 GB MEM</td><td>1000</td><td>4000000000</td><td>1</td><td>308631</td><td>319047</td></tr>
</table>
**Scenario 4: Read-write (POINT SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/b3a0f1eed9b3b4de14f584f4222485b2.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>64</td><td>4000000000</td><td>1</td><td>16313</td><td>24150</td></tr>
<tr><td>4-core 16 GB MEM</td><td>64</td><td>4000000000</td><td>1</td><td>38896</td><td>42051</td></tr>
<tr><td>4-core 32 GB MEM</td><td>128</td><td>4000000000</td><td>1</td><td>47036</td><td>53506</td></tr>
<tr><td>8-core 32 GB MEM</td><td>256</td><td>4000000000</td><td>1</td><td>80167</td><td>103935</td></tr>
<tr><td>8-core 64 GB MEM</td><td>256</td><td>4000000000</td><td>1</td><td>93335</td><td>123395</td></tr>
<tr><td>16-core 64 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>135267</td><td>220769</td></tr>
<tr><td>16-core 96 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>140926</td><td>229214</td></tr>
<tr><td>16-core 128 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>152629</td><td>234357</td></tr>
<tr><td>32-core 128 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>199042</td><td>381067</td></tr>
<tr><td>32-core 256 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>223027</td><td>384323</td></tr>
<tr><td>64-core 256 GB MEM</td><td>1000</td><td>4000000000</td><td>1</td><td>283722</td><td>520265</td></tr>
</table>

**Scenario 5: Read-write (RANGE SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/354be9b6cd7490f5ef0536291c5c926b.png)
<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>256</td><td>4000000000</td><td>1</td><td>10177</td><td>12129</td></tr>
<tr><td>4-core 16 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>23475</td><td>22560</td></tr>
<tr><td>4-core 32 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>27023</td><td>26009</td></tr>
<tr><td>8-core 32 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>48087</td><td>52183</td></tr>
<tr><td>8-core 64 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>53915</td><td>53766</td></tr>
<tr><td>16-core 64 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>98038</td><td>95518</td></tr>
<tr><td>16-core 96 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>97504</td><td>97117</td></tr>
<tr><td>16-core 128 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>101461</td><td>99140</td></tr>
<tr><td>32-core 128 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>154222</td><td>171150</td></tr>
<tr><td>32-core 256 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>182955</td><td>183249</td></tr>
<tr><td>64-core 256 GB MEM</td><td>512</td><td>4000000000</td><td>1</td><td>246526</td><td>266539</td></tr>
</table>
