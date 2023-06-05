
This document lists the performance comparison test results between TDSQL-C for MySQL and TencentDB for MySQL in the big dataset scenario.

## Big Dataset Scenario Overview
In the big dataset scenario, the entire volume of data cannot be all stored in the cache (the data volume is twice the memory size), and the disk needs to be read and written to update the cache during queries.

## Test Conclusion for Big Dataset Scenario
- In the read scenario, TDSQL-C for MySQL can achieve a CPU utilization of above 90% on compute nodes. The test shows that the resource utilization of TDSQL-C for MySQL is better than that of TencentDB for MySQL.
- In the write scenario, TDSQL-C for MySQL outperforms TencentDB for MySQL under lower specifications, and as the specifications and data volume increase, its performance advantage gets much greater.

<table>
<tr><th>Dataset Characteristics</th><th>Test Scenario</th><th>Read Type</th><th>Conclusion</th></tr>
<tr><td rowspan = "5" >Big dataset</td><td>Write</td><td>-</td><td>TDSQL-C for MySQL outperforms TencentDB for MySQL, especially under high specifications</td></tr>
<tr><td>Read</td><td>POINT SELECT</td><td>TDSQL-C for MySQL has a higher performance</td></tr>
<tr><td>Read</td><td>RANGE SELECT</td><td>TDSQL-C for MySQL and TencentDB for MySQL have generally the same performance under most specifications</td></tr>
<tr><td>Read-write</td><td>POINT SELECT</td><td>TDSQL-C for MySQL has a higher performance</td></tr>
<tr><td>Read-write</td><td>RANGE SELECT</td><td>TDSQL-C for MySQL and TencentDB for MySQL have generally the same performance under most specifications</td></tr>
</table>

## Test Results for Big Dataset Scenario
**Scenario 1: Write**
![](https://qcloudimg.tencent-cloud.cn/raw/024f78c2c564545f3e0765ebc4b7de4f.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>96</td><td>800000</td><td>150</td><td>14772</td><td>26864</td></tr>
<tr><td>4-core 16 GB MEM</td><td>96</td><td>800000</td><td>300</td><td>31140</td><td>45881</td></tr>
<tr><td>4-core 32 GB MEM</td><td>192</td><td>800000</td><td>300</td><td>31539</td><td>53082</td></tr>
<tr><td>8-core 32 GB MEM</td><td>192</td><td>800000</td><td>300</td><td>54397</td><td>97005</td></tr>
<tr><td>8-core 64 GB MEM</td><td>192</td><td>800000</td><td>450</td><td>54945</td><td>92988</td></tr>
<tr><td>16-core 64 GB MEM</td><td>192</td><td>800000</td><td>450</td><td>60948</td><td>111596</td></tr>
<tr><td>16-core 96 GB MEM</td><td>256</td><td>800000</td><td>600</td><td>79163</td><td>109014</td></tr>
<tr><td>16-core 128 GB MEM</td><td>384</td><td>5000000</td><td>300</td><td>105781</td><td>142165</td></tr>
<tr><td>32-core 128 GB MEM</td><td>384</td><td>5000000</td><td>300</td><td>81662</td><td>252668</td></tr>
<tr><td>32-core 256 GB MEM</td><td>384</td><td>5000000</td><td>400</td><td>101277</td><td>270367</td></tr>
<tr><td>64-core 256 GB MEM</td><td>384</td><td>6000000</td><td>450</td><td>115992</td><td>301974</td></tr>
</table>
**Scenario 2: Read (POINT SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/66323fa7b3751f3ad6105843883650b9.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>512</td><td>800000</td><td>150</td><td>38594</td><td>45597</td></tr>
<tr><td>4-core 16 GB MEM</td><td>512</td><td>800000</td><td>300</td><td>73117</td><td>75483</td></tr>
<tr><td>4-core 32 GB MEM</td><td>1000</td><td>800000</td><td>300</td><td>74664</td><td>92117</td></tr>
<tr><td>8-core 32 GB MEM</td><td>1000</td><td>800000</td><td>300</td><td>142866</td><td>181402</td></tr>
<tr><td>8-core 64 GB MEM</td><td>1000</td><td>800000</td><td>450</td><td>149526</td><td>172378</td></tr>
<tr><td>16-core 64 GB MEM</td><td>1000</td><td>800000</td><td>450</td><td>303341</td><td>325878</td></tr>
<tr><td>16-core 96 GB MEM</td><td>1000</td><td>800000</td><td>600</td><td>311256</td><td>336011</td></tr>
<tr><td>16-core 128 GB MEM</td><td>1000</td><td>5000000</td><td>300</td><td>262724</td><td>323877</td></tr>
<tr><td>32-core 128 GB MEM</td><td>1000</td><td>5000000</td><td>300</td><td>483449</td><td>573631</td></tr>
<tr><td>32-core 256 GB MEM</td><td>1000</td><td>5000000</td><td>400</td><td>474329</td><td>615283</td></tr>
<tr><td>64-core 256 GB MEM</td><td>1000</td><td>6000000</td><td>450</td><td>663715</td><td>940105</td></tr>
</table>
**Scenario 3: Read (RANGE SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/87bdf44b07e30f1b5985166449861acf.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>64</td><td>800000</td><td>150</td><td>13571</td><td>14388</td></tr>
<tr><td>4-core 16 GB MEM</td><td>64</td><td>800000</td><td>300</td><td>28962</td><td>26079</td></tr>
<tr><td>4-core 32 GB MEM</td><td>64</td><td>800000</td><td>300</td><td>30045</td><td>28314</td></tr>
<tr><td>8-core 32 GB MEM</td><td>64</td><td>800000</td><td>300</td><td>47298</td><td>57353</td></tr>
<tr><td>8-core 64 GB MEM</td><td>64</td><td>800000</td><td>450</td><td>58638</td><td>57281</td></tr>
<tr><td>16-core 64 GB MEM</td><td>128</td><td>800000</td><td>450</td><td>104072</td><td>98246</td></tr>
<tr><td>16-core 96 GB MEM</td><td>128</td><td>800000</td><td>600</td><td>114502</td><td>106160</td></tr>
<tr><td>16-core 128 GB MEM</td><td>128</td><td>5000000</td><td>300</td><td>121297</td><td>109978</td></tr>
<tr><td>32-core 128 GB MEM</td><td>256</td><td>5000000</td><td>300</td><td>192649</td><td>183658</td></tr>
<tr><td>32-core 256 GB MEM</td><td>256</td><td>5000000</td><td>400</td><td>185941</td><td>184855</td></tr>
<tr><td>64-core 256 GB MEM</td><td>256</td><td>6000000</td><td>450</td><td>283903</td><td>278997</td></tr>
</table>
**Scenario 4: Read-write (POINT SELECT)**
![](https://qcloudimg.tencent-cloud.cn/raw/d3af517dab8c75055814cd42b33444f8.png)

<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>64</td><td>800000</td><td>150</td><td>20726</td><td>22997</td></tr>
<tr><td>4-core 16 GB MEM</td><td>256</td><td>800000</td><td>300</td><td>47820</td><td>51545</td></tr>
<tr><td>4-core 32 GB MEM</td><td>256</td><td>800000</td><td>300</td><td>52680</td><td>62105</td></tr>
<tr><td>8-core 32 GB MEM</td><td>256</td><td>800000</td><td>300</td><td>94132</td><td>108540</td></tr>
<tr><td>8-core 64 GB MEM</td><td>256</td><td>800000</td><td>450</td><td>100882</td><td>120153</td></tr>
<tr><td>16-core 64 GB MEM</td><td>256</td><td>800000</td><td>450</td><td>192474</td><td>193744</td></tr>
<tr><td>16-core 96 GB MEM</td><td>256</td><td>800000</td><td>600</td><td>186854</td><td>184257</td></tr>
<tr><td>16-core 128 GB MEM</td><td>512</td><td>5000000</td><td>300</td><td>188389</td><td>195375</td></tr>
<tr><td>32-core 128 GB MEM</td><td>512</td><td>5000000</td><td>300</td><td>227494</td><td>306809</td></tr>
<tr><td>32-core 256 GB MEM</td><td>512</td><td>5000000</td><td>400</td><td>245819</td><td>307072</td></tr>
<tr><td>64-core 256 GB MEM</td><td>512</td><td>6000000</td><td>450</td><td>335819</td><td>453163</td></tr>
</table>

**Scenario 5: Read-write (RANGE SELECT)**
 ![](https://qcloudimg.tencent-cloud.cn/raw/c827a894bff90223ed54ebeb7a0318a1.png) 
<table>
<tr><th rowspan = "2"  width="15%">Specification</th>
<th rowspan = "2"  width="15%">Concurrency</th>
<th rowspan = "2"  width="15%">Table Size</th>
<th rowspan = "2"  width="15%">Tables</th>
<th colspan = "2" style="text-align:center" width="40%">QPS</th></tr>
<tr>
<th width="20%">TencentDB for MySQL</th>
<th width="20%">TDSQL-C for MySQL</th></tr>
<tr><td>2-core 16 GB MEM</td><td>32</td><td>800000</td><td>150</td><td>13177</td><td>13883</td></tr>
<tr><td>4-core 16 GB MEM</td><td>32</td><td>800000</td><td>300</td><td>27935</td><td>20720</td></tr>
<tr><td>4-core 32 GB MEM</td><td>64</td><td>800000</td><td>300</td><td>30705</td><td>29914</td></tr>
<tr><td>8-core 32 GB MEM</td><td>96</td><td>800000</td><td>300</td><td>50166</td><td>58060</td></tr>
<tr><td>8-core 64 GB MEM</td><td>64</td><td>800000</td><td>450</td><td>57866</td><td>53804</td></tr>
<tr><td>16-core 64 GB MEM</td><td>128</td><td>800000</td><td>450</td><td>107923</td><td>95976</td></tr>
<tr><td>16-core 96 GB MEM</td><td>128</td><td>800000</td><td>600</td><td>107589</td><td>107180</td></tr>
<tr><td>16-core 128 GB MEM</td><td>256</td><td>5000000</td><td>300</td><td>138710</td><td>110169</td></tr>
<tr><td>32-core 128 GB MEM</td><td>256</td><td>5000000</td><td>300</td><td>165299</td><td>180335</td></tr>
<tr><td>32-core 256 GB MEM</td><td>256</td><td>5000000</td><td>400</td><td>166066</td><td>171670</td></tr>
<tr><td>64-core 256 GB MEM</td><td>512</td><td>6000000</td><td>450</td><td>208616</td><td>190824</td></tr>
</table>
