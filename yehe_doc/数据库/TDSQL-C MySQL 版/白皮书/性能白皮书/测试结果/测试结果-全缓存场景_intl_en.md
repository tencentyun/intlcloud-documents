This document lists the performance comparison test results between TDSQL-C for MySQL and TencentDB for MySQL in the full cache scenario.

## Full Cache Scenario Overview
In the full cache scenario, as all data can be put into the cache, the disk doesn't need to be read and written to update the cache during queries.

## Full Cache Scenario Test Conclusion
- The higher the instance specification, the more obvious the performance advantage of TDSQL-C for MySQL. TencentDB for MySQL's write and read-write performance reaches a bottleneck at the 32-core specification, but TDSQL-C for MySQL can further increase the QPS with more CPU cores.
- In most scenarios, TDSQL-C for MySQL can achieve a CPU utilization of above 90% on compute nodes. The test shows that the resource utilization of TDSQL-C for MySQL is better than that of TencentDB for MySQL.
- TDSQL-C for MySQL is more stable in terms of request delay (RTT) and almost doesn't jitter at all when the dataset is fully cached.

<table>
<tr><th>Dataset Characteristics</th><th>Test Scenario</th><th>Read Type</th><th>Conclusion</th></tr>
<tr><td rowspan = "5" >Full cache</td><td>Write</td><td>-</td><td>TDSQL-C for MySQL has a higher performance</td></tr>
<tr><td>Read</td><td>POINT SELECT</td><td>TDSQL-C for MySQL has a higher performance</td></tr>
<tr><td>Read</td><td>RANGE SELECT</td><td>TDSQL-C for MySQL and TencentDB for MySQL have generally the same performance under low specifications, but the latter outperforms the former under high specifications</td></tr>
<tr><td>Read-write</td><td>POINT SELECT</td><td>TDSQL-C for MySQL has a higher performance</td></tr>
<tr><td>Read-write</td><td>RANGE SELECT</td><td>TDSQL-C for MySQL and TencentDB for MySQL have generally the same performance under most specifications</td></tr>
</table>

## Full Cache Scenario Test Results
**Scenario 1: Write**
![](https://qcloudimg.tencent-cloud.cn/raw/0a79d537b10dc1748c35608871b167d1.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>96</td><td>25000</td><td>250</td><td>15665</td><td>30054</td></tr>
<tr><td>4-core 16 GB MEM</td><td>192</td><td>25000</td><td>250</td><td>40574</td><td>53334</td></tr>
<tr><td>4-core 32 GB MEM</td><td>192</td><td>25000</td><td>250</td><td>42966</td><td>53713</td></tr>
<tr><td>8-core 32 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>67229</td><td>100737</td></tr>
<tr><td>8-core 64 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>76955</td><td>99480</td></tr>
<tr><td>16-core 64 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>134590</td><td>181035</td></tr>
<tr><td>16-core 96 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>142419</td><td>181029</td></tr>
<tr><td>16-core 128 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>144529</td><td>181482</td></tr>
<tr><td>32-core 128 GB MEM</td><td>1000</td><td>25000</td><td>250</td><td>224786</td><td>319913</td></tr>
<tr><td>32-core 256 GB MEM</td><td>1000</td><td>25000</td><td>250</td><td>220350</td><td>370294</td></tr>
<tr><td>64-core 256 GB MEM</td><td>1000</td><td>25000</td><td>250</td><td>236079</td><td>448221</td></tr>
</table>
**Scenario 2: Read (POINT SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/515386ed6e93b4ac12e10e160cf53aef.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>1500</td><td>25000</td><td>250</td><td>38633</td><td>57153</td></tr>
<tr><td>4-core 16 GB MEM</td><td>1500</td><td>25000</td><td>250</td><td>80398</td><td>108368</td></tr>
<tr><td>4-core 32 GB MEM</td><td>1500</td><td>25000</td><td>250</td><td>81100</td><td>108639</td></tr>
<tr><td>8-core 32 GB MEM</td><td>1500</td><td>25000</td><td>250</td><td>159885</td><td>185710</td></tr>
<tr><td>8-core 64 GB MEM</td><td>1500</td><td>25000</td><td>250</td><td>172800</td><td>206007</td></tr>
<tr><td>16-core 64 GB MEM</td><td>2000</td><td>25000</td><td>250</td><td>313223</td><td>402101</td></tr>
<tr><td>16-core 96 GB MEM</td><td>2000</td><td>25000</td><td>250</td><td>321229</td><td>402101</td></tr>
<tr><td>16-core 128 GB MEM</td><td>2000</td><td>25000</td><td>250</td><td>321617</td><td>403809</td></tr>
<tr><td>32-core 128 GB MEM</td><td>2000</td><td>25000</td><td>250</td><td>409118</td><td>715886</td></tr>
<tr><td>32-core 256 GB MEM</td><td>2000</td><td>25000</td><td>250</td><td>549297</td><td>719295</td></tr>
<tr><td>64-core 256 GB MEM</td><td>2000</td><td>25000</td><td>250</td><td>670026</td><td>1125180</td></tr>
</table>
**Scenario 3: Read (RANGE SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/e56fb83b37704c12a632588d80d91001.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>64</td><td>25000</td><td>250</td><td>14474</td><td>15837</td></tr>
<tr><td>4-core 16 GB MEM</td><td>64</td><td>25000</td><td>250</td><td>31523</td><td>31169</td></tr>
<tr><td>4-core 32 GB MEM</td><td>64</td><td>25000</td><td>250</td><td>31988</td><td>31048</td></tr>
<tr><td>8-core 32 GB MEM</td><td>64</td><td>25000</td><td>250</td><td>50362</td><td>59531</td></tr>
<tr><td>8-core 64 GB MEM</td><td>64</td><td>25000</td><td>250</td><td>63686</td><td>59008</td></tr>
<tr><td>16-core 64 GB MEM</td><td>128</td><td>25000</td><td>250</td><td>113098</td><td>113779</td></tr>
<tr><td>16-core 96 GB MEM</td><td>128</td><td>25000</td><td>250</td><td>124928</td><td>113377</td></tr>
<tr><td>16-core 128 GB MEM</td><td>128</td><td>25000</td><td>250</td><td>128728</td><td>113606</td></tr>
<tr><td>32-core 128 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>212540</td><td>197144</td></tr>
<tr><td>32-core 256 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>199970</td><td>197796</td></tr>
<tr><td>64-core 256 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>304502</td><td>289460</td></tr>
</table>
**Scenario 4: Read-write (POINT SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/8837bbf199d4db6bd20c1bb52505a542.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>22554</td><td>38001</td></tr>
<tr><td>4-core 16 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>57841</td><td>71560</td></tr>
<tr><td>4-core 32 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>60797</td><td>72625</td></tr>
<tr><td>8-core 32 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>97243</td><td>138499</td></tr>
<tr><td>8-core 64 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>112912</td><td>138784</td></tr>
<tr><td>16-core 64 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>198182</td><td>247586</td></tr>
<tr><td>16-core 96 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>203479</td><td>247631</td></tr>
<tr><td>16-core 128 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>209947</td><td>248301</td></tr>
<tr><td>32-core 128 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>348721</td><td>400126</td></tr>
<tr><td>32-core 256 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>333932</td><td>379531</td></tr>
<tr><td>64-core 256 GB MEM</td><td>512</td><td>25000</td><td>250</td><td>439984</td><td>553040</td></tr>
</table>
**Scenario 5: Read-write (RANGE SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/74449ca1d0cdf30b2f148ca6fe7c4888.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>64</td><td>25000</td><td>250</td><td>13568</td><td>16072</td></tr>
<tr><td>4-core 16 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>33318</td><td>34553</td></tr>
<tr><td>4-core 32 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>33766</td><td>34321</td></tr>
<tr><td>8-core 32 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>55588</td><td>65190</td></tr>
<tr><td>8-core 64 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>62616</td><td>65701</td></tr>
<tr><td>16-core 64 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>111148</td><td>123984</td></tr>
<tr><td>16-core 96 GB MEM</td><td>256</td><td>25000</td><td>250</td><td>131182</td><td>124659</td></tr>
<tr><td>16-core 128 GB MEM</td><td>384</td><td>25000</td><td>250</td><td>130767</td><td>125947</td></tr>
<tr><td>32-core 128 GB MEM</td><td>384</td><td>25000</td><td>250</td><td>218580</td><td>214861</td></tr>
<tr><td>32-core 256 GB MEM</td><td>384</td><td>25000</td><td>250</td><td>210922</td><td>216303</td></tr>
<tr><td>64-core 256 GB MEM</td><td>384</td><td>25000</td><td>250</td><td>308399</td><td>312941</td></tr>
</table>
